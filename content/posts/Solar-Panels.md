+++
title = "Solar Panels"
date = "2026-05-02T04:32:43-04:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Jorge L."
authorTwitter = "" #do not include @
cover = "nat.jpg"
tags = ["Energy", ""]
keywords = ["kw1", "kw2"]
description = ""
showFullContent = false
readingTime = true
hideComments = false
+++

# Notes

- Retomamos el proyecto
- En primer lugar, debemos genera un análisis de un año de datos
- Para ello debemos recordar cuál era el pipeline que desarrollamos el año pasado, el cual incluía estos pasos:
	- Desde el `log` se realiza un split por ciclos (up + down) y se reemplazan las comas por puntos
	- 

- **Periodo de análisis**: 25-10-2024 al 31-10-2024
	- En la gráfica de conteo de datos por columna notar que existen varios clusters donde faltan datos, consultar acerca de esto a Omar, principalmente por la zona centrada en marzo y la zona entre julio y agosto
		- Omar sospecha que la falta de datos de marzo se debe al cambio de acceso point donde se tuvo que reiniciar la estación varias veces.
	- Podemos reportar 2 gráficas: cantidad de datos disponibles respecto a la fecha, e histograma para dar cuenta de que la cantidad de fechas donde se dispone con los 9 valores es considerablemente mayor que el resto de situaciones donde faltan datos.

- Idea para **operativización**: el modelo (a single script) recibe como input el `log` de las celdas y un rango de fechas (periodo de análisis), luego, se ejecutan `stripFromTo.sh` y `splitCycles.sh`, esto prepara un directorio con un archivo de texto correspodiente a cada ciclo (2 barridos). Luego estos archivos son leidos por code3.2.ipynb donde se calculan los parámetros fotovoltáicos de ambas celdas y se acoplan, en un pkl, a los parámetros meteorológicos de aws_UV (datetime-index)

- Una buena noticia es que la gráfica semanal obtenida con este nuevo pipeline es idéntica a la que se obtuvo el año pasado


# Gráficas

1. **Muestra de una semana**: Parámetros fotovoltáicos y condiciones meteorológicas (aws-UV) durante una semana seleccionada desde el periodo de estudio tal que sea representativa de las diferentes curvas de irradiancia presentes en dicho periodo 
	- Eficiencia, Irradiancia, Potencia (PCE), Temperatura, Humedad relativa
	- Ambas celdas en la misma gráfica

2. **Correlaciones**: una gráfica para cada celda, mostrando las correlaciones entre parámetros meteorológicos y fotovoltáicos
	- Quizás hacerla con seaborn, lo importante es que sea visualmente amigable, porque la info está contenida en el coeficiente de correlación 

3. **Degradación (i)**: scatter potencia vs irradiancia con color indicando el tiempo (en meses) 
	- Esta gráfica no es tan directa de interpretar, quizás sería útil tener una gráfica adicional que muestre directamente la degradación en función del tiempo (para ello la siguiente gráfica)

4. **Degradación (ii)**: degradación de la celda en función del tiempo
	- Una idea es usar el PCE máximo de cada día y normalizar respecto al valor inicial, donde suponemos que la celda no tiene degradación alguna
		- Notar que debemos aplicar alguna máscara o criterio adicional para así tomar en cuenta que no todos los días tienen la misma irradiancia máxima
	- Confirmar en la literatura
	- [Gemini](https://gemini.google.com/share/e1c5b0bd04c6)

5. **Meteorología diaria**: Aggregates sobre las horas del día para visualizar el comportamiento promedio de la irradiancia, temperatura, humedad relativa y el PCE de ambas celdas


# Pipeline

1. `log`: archivo de texto con la información de cada ciclo. Uno para cada celda
	- Fecha y hora
	- Sentido: up, down
	- Voltaje y corriente

2. `stripFromTo.sh`: Genera un archivo de texto con el mismo formato de `log` pero entre las 2 fechas que son los argumento de este script

3. `SplitCycles.sh`: Genera archivos independientes para cada ciclo (barridos up y down)

4. `celda1_Ncliclos.pkl` y `celda2_Ncliclos.pkl`: Contienen las variables fotovoltáicas (PV) correspondientes a los N ciclos del periodo de estudio, para cada celda individualmente. Más la radiación solar
	- `Voc_up`, `Jsc_up`, `JMax_up`, `Vmax_up`, `PCE_up`, `FF_up`
	- `Voc_dw`, `Jsc_dw`, `Jmax_dw`, `Vmax_dw`, `PCE_dw`, `FF_dw`
	- `HI`

5. `CombinedCells.pkl`: Merge entre las variables fotovoltáicas de **ambas celdas**, más una columna para la **radiación solar** 
	- Radiación solar en unidades $10\cdot W/m^2=\text{mW}/cm^2$
	- date UTC-3
	- $\Delta T=$ 10min
	- Para un mismo ciclo, hay 20s de diferencia entre cada celda

6. `Met-PV_params.pkl`: Generado a partir de un merge entre la data de la estación y `CombinedCells.pkl`
	- Este es un merge por índice (fecha y hora) más cercano
	- `Voc_up`, `Jsc_up`, `JMax_up`, `Vmax_up`, `PCE_up`, `FF_up`
	- `Voc_dw`, `Jsc_dw`, `Jmax_dw`, `Vmax_dw`, `PCE_dw`, `FF_dw`
	- `HI`
	- `SolarRad`, `Temperature`, `rh`, `DewPoint`, `WindDir`, `WindSpeed`, `GustSpeed`, `Pressure`, `Rain`

7. `PlotMaker.ipynb`: Genera gráficas a partir del archivo `Met-PV_params.pkl`



<mark>Notes</mark>: 
- Los timestamps de las celdas están en UTC-3, pero la estación está en UTC 
	- En pandas tienes index que son UTC-aware y otros UTC-naive, incompatibles
- Recuerda que en mis códigos estamos trabajando la irradiancia en mW/cm^2 


# Website

- [OverleafProject](https://www.overleaf.com/project/69e12df80089406c7207e62b)
- Build website with react

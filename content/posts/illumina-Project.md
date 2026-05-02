+++
title = "Illumina Project"
date = "2026-05-01T21:08:31-04:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Jorge L."
authorTwitter = "" #do not include @
cover = "seasonalSet.png"
tags = ["Light pollution", "Numerical simualtions"]
keywords = ["Light pollution", "Numerical simualtions"]
description = "description"
showFullContent = true
readingTime = true
hideComments = false
showToc = true
+++

# Illumina documentation

paste doc from my personal HP laptop

## Running a simulation

## Generate plots

```python {linenos=inline hl_lines=[2] style=ashen}
source ~/miniconda/bin/activate
(illum) python3 interp_plots.py
```


## Add results to website 

```sh {linenos=inline hl_lines=[4] style=ashen}
git add .
git commit -m "added new results"
git push origin main
npm run deploy		    <- very important
```

Site should be ready within the next minute [here](https://lopez-504.github.io/simulations/)

<!-- ![seasons](/jorgelopezblog/img/seasonalSets.png "caption=killua drinking | width=800px | zoom=true") --!>
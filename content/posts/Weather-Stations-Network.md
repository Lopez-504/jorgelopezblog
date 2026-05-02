+++
title = "Weather Stations Network"
date = "2026-05-02T04:32:28-04:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = "Jorge L."
authorTwitter = "" #do not include @
cover = ""        # "remci_logo.png" # too big
tags = ["Weather", "Forecast"]
keywords = ["Weather", "Network"]
description = ""
showFullContent = false
readingTime = true
hideComments = false
+++

# Abstract

- We build a webpage to allow live and open access to all the data from our 3 aws
- Here we only develop the frontend and propose a code for data analysis, Edgar is currently working on the database and the compitibility issues that may arise from utilizing different brands of aws


# Database
Edgar's working on it...

- 

# Webpage 

- I think I'll use React for the frontend, since we need a dynamic site
- [Example 1](https://agrometeorologia.cl/)
- [Example 2](https://ifa.uv.cl/pronostico/valpo/es/valparaiso)
	- Hopefully we can upgrade this website
	- Check out these animations too [link](https://ifa.uv.cl/pronostico/valpo/es/exp)
	- Here's the website that comes with one of the AWS [link](https://www.licor.cloud/dashboards/public/edb4ddea-8f4d-4401-8479-1535407cc17a/false?filters={%22davra-timeselector%22:{%22type%22:%22relative%22,%22unit%22:%22minutes%22,%22value%22:30,%22live%22:false}})
		- Note: use the same icons in our site
- [Example 3](https://www.ceazamet.cl/index.php?pag=mod_mapa&p_cod=ceazamet)
- [Example 4](https://speclib.jpl.nasa.gov/download) ECOSTRESS Spectral Library


- [React template](https://github.com/mui/material-ui/tree/v7.3.9/docs/data/material/getting-started/templates/dashboard)
	- [ ] play around with it 
- [ ] Complete the [Tic-Tac-Toe](https://react.dev/learn/tutorial-tic-tac-toe) and check [interactivity](https://react.dev/learn/adding-interactivity)
- Maybe these components could come in handy: [link](https://ui.shadcn.com/docs/components/radix/combobox)

- Requirements: 
	1. Map showing the location of each AWS (left)
	2. Plots showing the current trends of the most important variables (right)
		- Similar to INIA
	3. Be able to easily dowload data
		- Specify variable and time interval
		- Choose format (csv, pkl, txt)
	4. Be able to download the plots the user creates
	5. Update itself every 5 or 10 minutes

## Plots section

- Ideally, I'd like to have a completely customizable plots with the following degrees of freedom:
	1. Station
	2. Variables
		- I think 4 should be plenty
		- Colors
		- Custom variable made from the original ones
	3. Time interval
	4. Plot kind
		- Independent for each variable
	5. Unit measure
	6. Style

- See Apache Echarts
	- Make some neat animation to put in the corner or something

# Tasks

- [ ] Add forest fires section 
- [ ] Reesctructure the website

- [ ] Add a brief explanation at the beginning of each section
- [ ] Add a section Forecast section
- [ ] Move the export card to tge data section
- [ ] Remove the wind plot from the station section
- [x] make the foot shorter
- [x] Add a Light Pollution section
- [ ] Check the [VIIRS](https://www.earthdata.nasa.gov/data/instruments/viirs) nasa website, it's too cool
	- I downloaded some data to my MSI
- [ ] Check [cieloschile](https://cieloschile.cl/en/light-pollution/) for some inspiration on the educational/pedagogical part of our website
- [ ] Fix the plots and station gallery to save the state they're in and not change when the user changes sections
- [x] Fix width of lightpollution section
	- It was the css for the light-things... some `max-width` parameter
- [ ] Read and follow [this](https://react.dev/learn/describing-the-ui) tutorial

## Things

- HTML to JSX (the one used by React) [link](https://transform.tools/html-to-jsx)
- **CORS**: Cross-Origin resource sharing
	- To allow files to talk to each other we need a server
- Are the Pocuro and the Ciencias UV stations identical? See pictures
- **Hero section**: the first, prominent visual block at the top of a webpage, designed to immediately grab attention, define the site's purpose, and guide users to take action.



### Backend web development (overview video)

- **Website** = frontend + backend
- **Frontend**: visual stuff
- **Backend**: what saves and manages data
- The **client** sends messages to the **server**
	- By default, computers can't receive messages form other computers, we need to program them into servers. This is done with a **backend programming language** (e.g., almost any programming language)
	- Now using a backend programming language is quite cumbersome so there are 2 tools that helps us: 
		- **Backend framework**: building our server is easier and requires a lot less code
			- Examples: ExpressJS (JavaScript), Django (Python), Rails (Ruby), Spring (Java)
		- **Package manager**: helps us install and manage our packages, pieces of code that perform common task and we reuse from other people. 
			- Example: npm (JavaScript), pip (Python), bundle (Ruby), Maven (Java)
- We also need a place to store our data: a **database**. This usually runs on a different computer than the server
	- Most popular ones: MySQL, PostgreSQL, MongoDB
- Frontend -> WWW-> Server -> Database -> Server -> WWW -> Fronend 
- Request-Response cycle:
	- **Request**: Message sent from the frontend to the backend
	- **Response**: Message sent from the backend to the frontend

#### Requests 
Parts: type of the request, domain name and URL path

```sql
POST https://amazon.com/orders

{
  "order": [
    {
      "id": "037d0156",
      "name": "Adidas Shoes",
      "quantity": 1,
    },
    {
      "id": "994c97a1",
      "name": "Amazon Essentials Socks",
      "quantity": 2,
    }
  ],
  "paymentMethod": "creditCard1"
  "deliveryAddress": "address1",
  ...
}
```

 - The domain name `amazon.com` makes sure the request get redirected to the correct server
 - The type `POST` and the URL path `/orders` **identify what kind of request this is**, and in the backend we can configure what types of request are allowed and how they should be handled
	 - For example in this case we could allow a POST '/orders' resquest and whenever we get one we will create a new order and save it in our database
	- Another examples would be a GET '/orders' or DELETE '/orders'
	- Examples of types: there's a finite number
		- GET
		- POST
		- PUT
		- PATCH
		- DELETE
		- HEAD
	- The URL path can be anything
	- All the different types or requests that the backend allows is called an **API** (Application Programming Interface)

- We have a naming convention for our requests, for this example we're using **REST** (REpresentational State Transfer)
- In REST the types have meaning, e.g., POST means to create something, GET to get something and so on. If an API uses the REST convention it's called a REST API 
	- Rest is by far the most common convention but there are others like GraphQL (uses POST /graphQL for all requests), RPC (Remote Procedure Call) which uses POST and more detailed URL paths (e.g., /createOrder, /getOrderHistory).

#### Infrastructure

- Instead of buying computers and turning them into servers, nowadays companies rent computers from a **Cloud Computer Company** 
	- The biggest ones are AWS (Amazon Web Services), GCP (Google Cloud Platform) and Microsoft Azure
	- Also known as IaaS (Infrastructure as a Service)
- These big companies divide their massive computers into **virtual machines** and we rent one of those virtual machines to run our backend and another one to run our database 
	- In case one virtual machines is not enough to handle the amount of requests our website is receiving, we can rent more virtual machines (VMs) to run the same backend and also set up a **load balancer** to distribute requests evenly across our VMs 
		- This is particularly useful during holiday season when the internet traffic rises
- But creating and setting up virtual machines is not a fast and easy job, that's why these cloud computing companies offer another service called **PaaS** (Platform as a Service)
	- A Paas allows us to just upload our backend code and it will take care of setting up all the necessary VMs and load balancer for us.
		- The most popular ones are:
			- Elastic Beanstalk (AWS)
			- App Engine (GCP)
			- App service (Microsoft Azure)

#### Microservices

- Usually the processes involved in a website require several actions: email confirmations, adding credit card, sending some code, etc; so it's wiser to split this up into smaller more simple processes (i.e., microservices)
	- This microservices are like mini-backends and they can even be written in different backend programming languages and have they're own database
	- This keeps our code base smaller and more focused
- For example **Twilio** offers an email service (microservice), which is a backend and API for sending emails, then we'd just need to send a request from our backend to Twilio's backend
	- When a company provides a backend and an API that outside applications (us) can use, this is called a SaaS (Software as a Service)
	- Pretty much everything we might need on our website is currently being offered by some company as a SaaS

- Foundations of Cloud Computing:
	1. IaaS
	2. PaaS
	3. SaaS

- **Primary Databases** are the ones we use by default for our website, but if we want to allow users to upload files, we might need another one like blob storage AWS S3 and CDN (AWS Cloudfront) to store and upload user's files. Or if we want text search, our primary's are quite slow at it so we would bring a search database like Elasticsearch. If we're getting a lot of traffic we could add a Cache (redis) to improve performance. If we want to schedule tasks for the future we'd use a job queue like **RabbitMQ**. 
- If we're doing data science we don't want to do the data anaylis using our primary database which is busy running our website, instead we'd copy all of our data into an analytical database like **Snowflake**
- And there are tons of other technologies out there that might fit our specifc needs


### Frontend 
[link](https://www.youtube.com/watch?v=WG5ikvJ2TKA&t=23s)

- HTML: HyperTextMarkupLanguage
	- We use HTML to add content to our webpage, just raw content.
	- HTML -> What to display our content
- CSS: Cascading Style Sheets
	- We use CSS to style our webpage
	- CSS -> How to display our content
#### JavaScript

- JavaScript: HTML and CSS only display things, but JS makes our webpage **interactive**  
	- The most important feature of JS is the **Document Object Model** (DOM), it allows JS to make changes in our webpage
- But using the DOM directly is cumbersome, that's why we use a **JS framework**. 
	- Popular ones: ReactJS, Angular, VueJS
- JS as a programming language does not allow us to split up our code into different files, to do this we need a **bundler** 
	- Popular ones: Webpack, Vite
	- A bundle will take all of our files and bundle them into a single JS file that we can put on our website
- Another tool that we use is a **transpiler**, which adds extra features to JS or enhance it
	- Popular one: Typescript
	- It allow us to write an enhanced version of JS and then it handles the convertion back to JS (because browser like Chrome can only understand JS)
- So to recap, the major technologies in the JS world are:
	- Language (JS of course)
	- Framework (e.g., ReactJS, Angular, VueJS)
	- Bundler (e.g., Webpack)
	- Transpiler (e.g., Typescript)
#### CSS

- CSS has similar problems as JS, namely: 
	1. We can't organize code into different files
	2. Missing useful features
	- So we also use a **bundler** and a **transpiler** for CSS, this is called a **preprocessor**
		- preprocessor = bundler + transpiler
		- The most popular one: **Sass**
- We also have CSS frameworks, a whole bunch of CSS codes that some else wrote and it helps us solve common problems, so it can save us a lot of time
	- The most popular one: **Bootstrap**

#### HTTP

- How does the frontend communicate with the backend? 
- JS has a feature called **XMLHttpRequest**. It let us send a message from the frontend to a URL which the backend is listening to (through the API, see backend concepts) 
- Now this feature is quite old and nowadays we have new technologies like `axios-http` or `fetch API` to send messages to the backend-


### React concepts

1. Declarative
2. Components
3. Single Page
4. JSX
5. Vite + React
6. States

- When the browser receives an HTML it creates a DOM (Document Object Model), a tree-like structure that represents a website, and using JS we can change anything about this DOM
- The advantage of using React is that we're only concern with describing what the UI should look like and not every step of how to build it in the DOM (as we would usign JS)
	- React --> Resulting UI  (i.e., **declarative**) --> Cleaner  
	- JS --> Building steps  (i.e., **imperative**) --> Messier

- A **component** is a reusable building block. It is a function that takes some properties (props) and returns the UI we want to render 
- The syntax we use to write components is **JSX** (JavaScrip XML) which is kinda like JS + HTML 

- In React we're only working with one HTML page (i.e., one `index.html`), and then this page will be updated dynamically by JS. 
- One of the reasons React is so fast is that it's only updating the parts of that `index.html` that need to be updated

- **Vite** is great for working with all sorts of technologies, specially React projects

- React **states** are data that can change over time, and when the data changes React updates the UI. Check this example of a button that increases a counter:

```JS
function App(){

// counter is the current value 
// setCounter is a function used to change this value
const [counter, setCounter] = useState(0)

function increaseCounterHandler(){
  setCounter(counter + 1)
}

return (
	<div>
	  <h1>{counter}</h1>
	  <button onClick={increaseCounterHandler}> click me! </button>
	</div>
)
}
```

- React hooks: like libraries or functions from libraries? read documentation

### JS needed before React

- 

### REDUX

- **Redux** is a predictable state management library for JS apps, primarily used with React
- **Reduc toolkit**: tools and conventions that simplify the development of Reduc apps by reducing boilerplate. It's design to address common painpoints in React development
	- boilerplate: standardized, reusable text or code that can be inserted into documents or programs with little or no change
- To fully understand this tool u need to have some level of understanding of hooks and states





# Tutorials

Work on these, learn and update to GitHub so the world can see!

## Build JS calculator
[link](https://www.youtube.com/watch?v=I5kj-YsmWjM&t=354s)

- 
## Buld React Tic-Tac-Toe
[link](https://react.dev/learn/tutorial-tic-tac-toe)

- 
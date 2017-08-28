# Machine Learning Engineer Nanodegree
## Capstone Proposal
Maimaitirebike Maimaiti  
August 26, 2017

## Proposal
_(approx. 2-3 pages)_

### Domain Background
_(approx. 1-2 paragraphs)_

In this section, provide brief details on the background information of the domain from which the project is proposed. Historical information relevant to the project should be included. It should be clear how or why a problem in the domain can or should be solved. Related academic research should be appropriately cited in this section, including why that research is relevant. Additionally, a discussion of your personal motivation for investigating a particular problem in the domain is encouraged but not required.

Concerns about global climate change, energy security, and unstable fuel prices have caused many decision makers and policy experts worldwide to closely examine the need for more sustainable transportation strategies. Bike-sharing system, the shared use of a bicycle fleet, is one mobility strategy that could help address
many of these concerns [1](http://tsrc.berkeley.edu/sites/default/files/Bikesharing%20in%20Europe,%20the%20Americas,%20and%20Asia%20-%20Shaheen.pdf). Although the 1st generation of bike-sharing programs began in Amsterdam in 1965, bike-sharing has received increasing attention in recent years with initiatives to increase cycle usage, improve the first mile/last mile connection to other modes of transit, and lessen the environmental impacts of our transport activities. Especially, the development of better methods of tracking bikes with improved technology gave birth to the rapid expansion of bike-sharing programs throughout Europe and now most other continents during this decade. Since then bike-sharing has had profound affects on creating a larger cycling population, increasing transit use, decreasing greenhouse gases, and improving public health [2](http://scholarcommons.usf.edu/jpt/vol12/iss4/3/). 

In 2013, Bay Area Bike Share ([Now is named as Ford GoBike](https://www.fordgobike.com/)) was introduced as a pilot program for the Bay Area region, with 700 bikes and 70 stations across San Francisco and San Jose. Similar to car sharing, "bicycle sharing" in Bay Area is a membership-based system for short-term bicycle rental. Members can check out a bicycle from a network of automated stations, ride to the station nearest their destination, and leave the bicycle safely locked for someone else to use. While traditional bike rentals are loaned out for half-day or longer, bike sharing is designed for short, quick trips. Stations connect users to transit, businesses and other destinations, often providing the "last-mile connection." To reflect system design, pricing is set to discourage trips longer than 30 minutes. Users can take an unlimited number of 30-minute trips during their membership period; however, any individual trip over 30 minutes will incur an additional fee [3](http://www.bayareabikeshare.com/faq#BikeShare101).

A crutial part of successfully operating such a BBS is the redistribution of bikes. Since the count of bikes in each station, each of which has a finite number of docks, fluctuates, redistribution operation must be performed periodically to make the bike-sharing service more efficient and environmentally friendly. However, staff moving bikes from areas of high supply/low demand to areas of low supply/high demand is time consuming, expensive, and polluting [1](http://scholarcommons.usf.edu/jpt/vol12/iss4/3/). Thererfore, predicting the number of available bikes in each station over time is one of the key tasks to making this operation more efficient. 

The modeling of bike availability using various features like time, weather, built environment, transportation infrastructure, etc., is an area of significant research interest. [Froehlich et al.](https://www.ijcai.org/Proceedings/09/Papers/238.pdf) used four predictive models to predict the number of available bikes at each station: last value, historical mean, historical trend, and a Bayesian network

In this project we model the bike availability use machine learning techniques to predict bike availability.

### Problem Statement
_(approx. 1 paragraph)_


In this section, clearly describe the problem that is to be solved. The problem described should be well defined and should have at least one relevant potential solution. Additionally, describe the problem thoroughly such that it is clear that the problem is quantifiable (the problem can be expressed in mathematical or logical terms) , measurable (the problem can be measured by some metric and clearly observed), and replicable (the problem can be reproduced and occurs more than once).

The goal of this project is to predict the number of available bikes at a bike share station. Specifically, the number of available bikes at station i at time (t + $\delta$t) denoted by $Y_{i+di)}$, where 𝑖=1,2,…,70.
the available bikes at station 𝑖 at time 𝑡, the available bikes at its neighbors at the same time 𝑡, the month-of-the-year, day-of-the-week, time-of-day, and various selected weather conditions. The predictors’ vector for station 𝑖 at time 𝑡, denoted by 𝑋𝑡𝑖, was used in the built models to predict the 𝑙𝑜𝑔 of the number of available bikes at station 𝑖 at time 𝑡 and at a prediction horizon time, denoted by log(𝑦𝑡+Δ𝑖), where 𝑖=1,2,…,70. The effect of different prediction horizons, Δ (range 15–120 minutes),


### Datasets and Inputs
_(approx. 2-3 paragraphs)_

In this section, the dataset(s) and/or input(s) being considered for the project should be thoroughly described, such as how they relate to the problem and why they should be used. Information such as how the dataset or input is (was) obtained, and the characteristics of the dataset or input, should be included with relevant references and citations as necessary It should be clear how the dataset(s) or input(s) will be used in the project and whether their use is appropriate given the context of the problem.

We use datesets provided by [Bay Area Bike Share](http://www.bayareabikeshare.com/open-data), also known as Ford GoBike. This data is provided according to the [Ford GoBike Data License Agreement](https://assets.fordgobike.com/data-license-agreement.html). They make regular open data releases, plus maintain a real-time API

#### The Data:
There are four different data files in this dataset.

_status_ data

-station_id: station ID number (use "station.csv" to find corresponding station information)

-bikes_available: number of available bikes

-docks_available: number of available docks

-time: date and time, PST

_station_ data

-station_id: station ID number (corresponds to "station_id" in "status.csv")

-name: name of station

-lat: latitude

-long: longitude

-dockcount: number of total docks at station

-landmark: city (San Francisco, Redwood City, Palo Alto, Mountain View, San Jose)

-installation: original date that station was installed.

_trip_ data

Each trip is anonymized and includes:

-Trip ID: numeric ID of bike trip

-Duration: time of trip in seconds  (trips <1 min and >24 hours are excluded)

-Start Date: start date of trip with date and time, in PST

-Start Station: station name of start station

-Start Terminal: numeric reference for start station

-End Date: end date of trip with date and time, in PST

-End Station: station name for end station

-End Terminal: numeric reference for end station

-Bike #: ID of bike used

-Subscription Type: Subscriber = annual or 30-day member; Customer = 24-hour or 3-day member

-Zip Code: Home zip code of subscriber (customers can choose to manually enter zip at kiosk however data is unreliable)

_weather_ data

Daily weather information per service area, provided from Weather Underground in PST. Weather is listed from north to south (San Francisco, Redwood City, Palo Alto, Mountain View, San Jose).
        
-Precipitation_In         "numeric, in form x.xx but alpha ""T""= trace when amount less than .01 inch"        

-Cloud_Cover         "scale of 0-8, 0=clear"        

-Zip: 94107=San Francisco, 94063=Redwood City, 94301=Palo Alto, 94041=Mountain View, 95113= San Jose"


### Solution Statement
_(approx. 1 paragraph)_



In this section, clearly describe a solution to the problem. The solution should be applicable to the project domain and appropriate for the dataset(s) or input(s) given. Additionally, describe the solution thoroughly such that it is clear that the solution is quantifiable (the solution can be expressed in mathematical or logical terms) , measurable (the solution can be measured by some metric and clearly observed), and replicable (the solution can be reproduced and occurs more than once).

### Benchmark Model
_(approximately 1-2 paragraphs)_

In this section, provide the details for a benchmark model or result that relates to the domain, problem statement, and intended solution. Ideally, the benchmark model or result contextualizes existing methods or known information in the domain and problem given, which could then be objectively compared to the solution. Describe how the benchmark model or result is measurable (can be measured by some metric and clearly observed) with thorough detail.


In this project, the results of RF moding of the bike count proposed in [Hudhaifa] is taken as a benchmark model. In this study, Random Forest (RF) and Least-Squares Boosting (LSBoost) algorithms were used to build univariate prediction models for available bikes at each Bay Area Bike Share station. However, to reduce the number of required prediction models for the entire BSS network, we also used Partial Least-Squares Regression (PLSR) as a multivariate regression algorithm. The performance of RF is the best and we will take it as a benchmard model.

### Evaluation Metrics
_(approx. 1-2 paragraphs)_


The benchmark model I have taken used mean absolute error as their evaluation metrics. Therefore, I will also take it as my evalutation metrics.

In this section, propose at least one evaluation metric that can be used to quantify the performance of both the benchmark model and the solution model. The evaluation metric(s) you propose should be appropriate given the context of the data, the problem statement, and the intended solution. Describe how the evaluation metric(s) are derived and provide an example of their mathematical representations (if applicable). Complex evaluation metrics should be clearly defined and quantifiable (can be expressed in mathematical or logical terms).

### Project Design
_(approx. 1 page)_

In this final section, summarize a theoretical workflow for approaching a solution given the problem. Provide thorough discussion for what strategies you may consider employing, what analysis of the data might be required before being used, or which algorithms will be considered for your implementation. The workflow and discussion that you provide should align with the qualities of the previous sections. Additionally, you are encouraged to include small visualizations, pseudocode, or diagrams to aid in describing the project design, but it is not required. The discussion should clearly outline your intended workflow of the capstone project.

-----------

**Before submitting your proposal, ask yourself. . .**

- Does the proposal you have written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Solution Statement** and **Project Design**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your proposal?
- Have you properly proofread your proposal to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?

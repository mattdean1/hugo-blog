+++
date = "2017-06-15T11:34:03+01:00"
image = "split.jpg"
summary = "Converting a Django monolith to microservices: a REST API and a React frontend"
title = "Bifurcate"

+++



Over the past year, whilst on placement at Lilly, my main focus was setting up on-premise platform-as-a-service (OpenShift). I worked as part of a small team on this, with a few people in the US and a few in the UK.

One of the tools we created was a metrics dashboard with charts showing usage information about the platform. For MVP we built this as a Django monolith, which was fine to get something out the door, but it was difficult to coordinate across timezones, since half the team was in the UK and half in the US. Our skillsets were also segregated, with the experienced Django developers sitting in the US whereas the UK team members were more comfortable with Node.js.

I identified that a microservices architecture would be a better fit for this project so each subteam could develop more independently. We also liked the idea of some of the other advantages of a service-oriented architecture, like independent release schedules and the ability to choose the most suitable stack for each part of the application.



## The app

### MVP 1

The Django MVP of our app was pretty basic, hitting the OpenShift API and parsing that data on every page load. We passed that parsed data into the HTML templates and rendered some tables and charts. This did satisfy the baseline requirements of showing management and ourselves the customer uptake of OpenShift, but it had some flaws, first and foremost, page load time. As more customers started checking the dashboard, we also put strain on the OpenShift API, particularly in our Proof-of-Concept environment, where resources are limited.

### MVP 2

Since a lot of the data parsing logic was already implemented in Python, we decided to keep a Django-based backend, but convert it to a RESTful API. During this period we learned a lot about the tradeoffs during API development, and why an API-centric approach to software development can be so powerful in enabling internal collaboration.

See Jeff Bezos' 'API Mandate' at Amazon in the early 2000's  - he mandated that all employees must develop services in order to share information between teams, i.e. the only way to get access to other internal data was through an API. This edict was transformational to the way Amazon employees worked, and the way the company was structured internally, arguably a big factor in enabling Amazon to go from an online bookstore to the enormous e-commerce and cloud computing platform it is today.



For the frontend I chose to go with React, hosted on a Node server. These were technologies I had a fair bit of previous experience with, and the dashboard was a good fit for the component-oriented architecture of React app, since we had a similar dataset for all 3 of our OpenShift environments, hence often 3 charts displaying the same kind of data.



## Wrangling Django

For MVP2, converting the backend to return JSON wasn't crazily difficult. We already passed some data into our templates, so we could get a basic response going by returning a `django.http JsonResponse` instead of `render`ing a template. Of course this didn't give us a true RESTful API, but for a couple of `GET` endpoints it did the job.

One issue I ran into was attempting to serialize our Django objects - when passing an object into a template file you can use Django Classes just fine, but as soon as I tried to serialize these into JSON up popped a whole bunch of errors. Fortunately, out of the box Django provides serialization into JSON as long as you use a `Model` rather than a `Class`. Converting our classes to models was relatively straightforward and essentially required me to specify some detail about each field like datatype, length, etc..

Later, as we built out our API interfacing between OpenShift and our frontend, and we needed more endpoints, especially `POST`/`PUT`, we moved to use [Django REST Framework](http://www.django-rest-framework.org/) (DRF). DRF is actually a really nice tool, and gives you a lot of features 'for free' as you build an API, like making your API browsable, and easy integration with OAuth. Next time I build an API I'd probably check out something like [Swagger](https://swagger.io/), or explore using a statically typed or functional language like Go or Elixir in the backend.



## Juggling Javascript

I built the frontend in React, using the [semantic-ui-react](https://react.semantic-ui.com/introduction) framework, and [react-chartjs](https://github.com/reactjs/react-chartjs). These frameworks made it easy to create a responsive site, and I created some nice pure chart components. The one hurdle I had to watch out for was to get the data from our API in the correct React lifecycle method - I ended up using `fetch` inside `componentDidMount`. Sadly Internet Explorer is the default browser at work, so to support that I had to import the [whatwg-fetch](https://www.npmjs.com/package/whatwg-fetch) polyfill.

### Caching
One of the main drawbacks of MVP1 was the page load time, since we fetched data from the OpenShift API on every page load. To try and address this, I decided to add some caching to our app, which happened at a few different layers. I tackled the following bullet points one-by-one, benchmarking page load times at each step.

-   Since I'm most familiar with Node, I wrote a short cron job using [node-cron](https://www.npmjs.com/package/node-cron), which regularly copied the OpenShift API responses verbatim into redis. Of course I had to edit our backend to consume the cache instead of getting data from OpenShift directly, using [redis-py](https://github.com/andymccurdy/redis-py).
-   This sped up page load times a fair bit, but the data parsing step was still happening on every refresh, since only the raw OpenShift API responses were in redis, not the collated data. So, I added to my cron job - I stored *our* Django API responses in redis too. After editing the backend again to retrieve the *parsed data* from redis where possible, this meant page load times were considerably decreased.
-   The one 'gotcha' here is that if our API returned it's values from the redis cache, how would we update the cache with new values? I set the redis expiry time to be a little lower than the cron frequency, which meant that new results would be computed every time the cron job ran.
-   Of course, if redis was down, would that bring down our entire API? No, because if a key did not exist (it had expired or redis was down), I would fall back to parsing the data and/or getting data directly from OpenShift.



## Further Improvements and takeaways
As mentioned previously, we later moved our Django API over to Django Rest Framework, which gave us a lot more reliability and the ability to plug in a Postgres database, which meant we could store historical data too.

The best part about this migration to DRF was that we didn't have to change the frontend - perhaps we changed what endpoint we hit via an environment variable, but we could pretty much leave the frontend alone since it was a separate service.

Overall this was a fantastic project which really hammered home the value of service oriented architecture and made me realise that designing an API is harder than it looks! I've been using the GitHub GraphQL API in another project, which is a lot of fun and seems especially powerful for mobile apps.

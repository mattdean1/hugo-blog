+++
date = "2017-01-17T20:39:38Z"
title = "Metamorphosis"
summary = "How I went from knowing nothing about Node.js to running a 90 minute webinar in less than a week"
image = "butterfly.jpg"

+++



This post details how I went from knowing zero Node.js to running a 90 minute webinar on it in less than a week! To summarise, I introduced a new recruitment hackathon stream using Node.js, which increased the number of applications by **25%**. The students using the new platform (all of whom I also mentored), made up **55%** of the candidates invited to interview.

The junior developer recruitment process at Eli Lilly consists of a week-long online hackathon, followed by on-site interviews. During the time I applied, the development language used for the hack was restricted to Salesforce.com.

The conversion rate of applicants was fairly low for my intake, with a number of applicants failing to submit at the end of the hackathon. After consideration, and talking to some colleagues who went through this process, I spotted an opportunity to improve the number of applicants and their conversion rate.

The key issue was the lack of flexibility - Salesforce is a useful platform, and experience with Java can transfer well, but for those with prior experience in web development the limitations could be frustrating. Any new platform added also needed to have a free trial, and be accessible to those with little/no experience.



## Choosing the platform

Node.js on Heroku seemed like a good choice of language and platform due to it's plethora of packages (allowing applicants to add complex functionality quickly), wide usage within Lilly (giving us expertise to lean on for judging), and easy integration with other free tools like GitHub.

A number of tasks had to be completed before offering this application stream to the next set of applicants:

-   An example application submission to demonstrate the quality of work expected
-   Detailed mark scheme / scoring criteria
-   Training video(s) to get those with little previous experience up to speed

I therefore decided to simulate the hackathon process end to end using our new framework. This way I could test it out and see if it would be possible for someone who didn't know Node to produce something comparable to those choosing the Salesforce path.

One of our graduate developers who had previous experience with Node created the scoring criteria, and off I went!



## Learning Node and ideation

Step one was to learn Node.js. I collected plenty of resources - software, articles, and tutorials, then began to work through them. One particularly useful tool was [express-generator](https://expressjs.com/en/starter/generator.html), which creates a barebones Node.js/Express app filestructure.

I then had to think of an idea. As part of the hackathon, we provide applicants with some 'challenges' to help with the ideation phase. These take the form of quite general problems related to healthcare, for example encouraging diabetics to exercise, or distributing food around the world.

The idea I settled on was to help distribute supplies to those affected by a natural disaster. [Quake-supply](https://github.com/mattdean1/quake-supply) intends to track supplies distributed through field outposts after an earthquake.





## Example submission

I created my sample app over a couple of days, learning more about Node along the way.

I pull live data from the US Geological Survey API to get the coordinates and magnitude of the most recent earthquakes, and use [Leaflet.js](http://leafletjs.com/) for mapping. I also used [SweetAlert](http://t4t5.github.io/sweetalert/) and [DataTables](https://datatables.net/) to help make it look presentable.

Once the app was finished, I recorded a **[video](https://www.youtube.com/watch?v=rwAduYXoO8I)** explaining the idea, the app, and how I created it.





## Webinar

I ran a live webinar to give the students more information about the hackathon, show them how to get started on the platform, and give them a chance to ask questions. There was a separate webinar run for the Salesforce stream so for this one I was on my own - after a brief introduction by the sponsor of the program, it was down to me. Here's the structure of the content I presented:

#### Tools

First, I thought it'd be a good idea to introduce the students to some of the key tooling and the platform. For this webinar I had to assume they had no previous web development experience, so it was difficult to strike a balance between being high-level and detailed.

I gave a quick rundown of GitHub, PaaS, Heroku, Atom, and express-generator.

#### CRUD through a todo app

Secondly, I introduced the Connect, Request, Update, and Delete operations on a Node/Mongo stack by creating a basic todo app. I generated the file structure using express-generator and explained each folder, then got straight into coding.

I used a pre-prepared webpage with code snippets (GitHub Gists) so those viewing the webinar could code along live or with the recording. My app was also regularly deployed and live on Heroku throughout the webinar.

The tutorial was roughly split up into four sections:

-   Setup, first push, importing a CSS framework
-   Display Todos, create new Todos
-   Add a database
-   Delete a todo, tick off a todo

#### Scoring and Submission

Lastly, I ran through what we were looking for in a successful submission, with particular attention to the format of the submission video.

I also talked about the scoring criteria and gave my final tips and tricks for succeeding in the hackathon. The webinar ended with Q and A, giving candidates valuable time to clarify anything they didn't understand.

#### Result

After the webinar, I made available on the Facebook group the list of resources I curated, the Todo app repository, the snippet webpage, and a recording of the entire thing.

I got great feedback from the applicants and my colleagues, who said it was extremely clear and everything was well explained.



## Mentoring

I was allocated all 6 students who chose to use Node/Heroku to mentor through the process. This consisted of encouraging them via facebook and email, and answering any questions they had about the application process or about the technology. Over the week I supported them as best as I could, and got some positive 'thankyou' responses, but the real feedback came when it was time for judging.

Myself, some other developers, and some more technically minded management came together to score the submissions and decide which candidates should be invited on-site for an interview.

I was unbelievably pleased that my mentees made up **55%** (5 out of 9) of the interview candidates! This is likely due to a combination of factors, but I think their use of the Node/Heroku was key, as it allowed them to quickly create advanced functionality.



## Continued use of Node.js

Learning Node.js was a key milestone in my journey as web developer, and I've gone on to use it in a number of apps at work, also becoming the nominal Node.js consultant for our internal PaaS service.

Example projects I used it in include: an [OpenID Connect accelerator](https://github.com/mattdean1/nodejs-oidc-client-example), a number of metrics dashboards (in combination with [Chart.js](http://www.chartjs.org/)), and [a reminder system for people with Alzheimer's](https://github.com/mattdean1/reMINDer).

I'm currently learning React and Webpack by using them for a couple of projects in work, and although the outcome may not be as dramatic, I hope to write a post featuring these technologies soon.

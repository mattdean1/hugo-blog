+++
date = "2017-05-02T11:27:49+01:00"
image = "cup.jpg"
summary = "Competing in the Microsoft Imagine Cup"
title = "Imagine"

+++

## The Competition

The Microsoft Imagine Cup is a competition for students ... Microsoft describes it better than I can:

>Imagine Cup is a global competition that empowers the next generation of computer science students to team up and use their creativity, passion and knowledge of technology to create applications that shape how we live, work and play. Every year tens of thousands of students from across the globe compete for cash, travel and prizes and for the honor of taking home the Imagine Cup!

My flatmate, Wilson, found out about the competition - after he told me and one of his friends from Uni, Sam, we decided to give it a go. Little did we know we'd make it all the way to the national finals!


## Our Product

After an extensive brainstorming session resulting in many crumpled pieces of paper, we drew inspiration from the then-recently released Wetherspoons app. Their app allows you to order and pay for food and drink from your table - no more waiting at the bar!

We loved the convenience and thought it'd be great to have this ability at every restaurant or bar. Some market research showed that while some large chains (McDonald's, Wagamamas) recently released apps with similar functionality, no solution existed for independent businesses, or even small to medium size chains.

So, we chose to create a customer purchase and ordering platform for independent restaurants and bars:

Onboarding businesses had to be as streamlined as possible, so we created a simple sign-up form, followed by a drag-and-drop web interface for the owner to create their menu. Each menu has a unique QR code for the owner to display e.g. on tables. The owner can log back in at any time to update prices or availability of menu items, which will be instantly reflected in the menu the customer sees.

The customer scans the QR (or enters the menu ID on our website) and is taken directly to a mobile-optimized webapp where they can see what's on offer and add items to their basket. The customer can then submit their order and pay through PayPal - performing the entire transaction without downloading an app or creating an account!

Once confirmed, the order goes straight through to a touchscreen (which could be a cheap android tablet) in the kitchen/bar for staff to fulfill. Staff can tap the screen to check orders off once they're completed and keep track of the status.

### Advantages

 - The customer receives their order without leaving their seat!
 - Restaurant can reduce front of house staff
 - Bar can reduce average wait time
 - Front of house staff can focus on what really matters - providing an exceptional customer experience

## The Tech

The frontend of the app was written in Node.js and Express. We used these technologies since we all had experience with them - for this project we decided we should focus on delivering a great product, and there was still plenty to learn since we were new to the Azure platform.

We got Azure credit as part of the competition, so it made sense to use Microsoft's platform to host our Node app - we also used an MSSQL database and Azure Redis for caching. I quite enjoyed using Azure - it's becoming difficult to see the differentiation between GCP, AWS, and Azure for basic hosting like this. I think to choose between platforms I'd probably consider pricing first, and for simplicity go with the platform on which I was already using less common functionality like AWS Lambda.


## The UK finals

We submitted a short video pitch and our business plan. After a couple of weeks we got a very exciting email: we were through to the UK finals! The final took place at Microsoft's London offices, where we were given the opportunity to present to such dignitaries as the CTO of Microsoft Accelerator, their Principal Tech Evangelist, and the Director of Azure for Research.

It was an amazing day, with sessions on entrepreneurship and tons of advice on how to start and scale a business. We got great feedback on our product - the judges highlighted our customer focus and real potential to disrupt the hospitality industry. Unfortunately we didn't make it through to the next stage of the competition, but I had a great time working with Wilson and Sam, and we all learned a lot technically, as well as about creating a startup.

Some feedback from the judges:

 - "Could definitely see this taking off"
 - "Slick presentation"
 - "You've clearly identified and addressed a real problem in this market"
 - "Solid validation from external stakeholders"

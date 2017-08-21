+++
date = "2016-10-28T23:17:39Z"
title = "Promulgation"
draft = false
image = "sing.jpg"
summary = "Why I decided to create a blog and how I set it up"

+++



## Why blog?

I decided to create this blog for three reasons:

1. **To practice writing and clarify my thinking**

    I've produced very few extended pieces of writing over the past 5 years, in part due to my subject choices at A-Level and Uni. Most would agree that writing is an essential skill to refine, and I think the best way to for me to do that is to cover topics which I'm passionate about.

    The process of writing things down requires clear thinking, so covering familiar topics will enforce a certain rigor, and perhaps expose some faulty assumptions. Writing a blog post on an unfamiliar topic will be a ideal way to explore, then codify and share my learning.

2. **To have a public platform where I can share thoughts, experiences, and learning**

    I love the idea that you could read my blog and find something useful, whether it be a tutorial for some new technology or a new technique for learning.

    I hope that my experiences will reflect yours, and my thinking will resonate with you. If you learn a fraction of what I do through writing the posts I'll judge it a great success!

3. **To display and keep a record of all the exciting things I learn about tech**

    One of the things I love about technology is that there is always more to learn. There are endless opportunities to read, practice, and use new concepts every day. It will be a sad day if I ever stop learning, so I strive to explore fresh ideas constantly.

    While this blog may serve as an impartial record of my journey through life and the tech industry, I hope it will also be useful to demonstrate my passion for technology.






## What can you expect from this blog?

At this stage, the exact contents of future posts is still undecided. Everything I write will keep the above principles in mind, so you can expect the majority of posts will be somewhat technology-related. If there's a specific topic you'd like me to cover, please feel free to reach out with suggestions and feedback!

I hope the form and tone of my writing will develop into a warmer, more conversational style over the coming months - perhaps it will change drastically as I get a clearer idea of the audience and the writing style I'm most comfortable with.

I'm planning to post at least once a month; this seems like a reasonable cadence to ensure I continue to meet the aims above.



Thanks for reading!





## Technical setup - Blog 1.0

### Static site generation

Currently I'm using [Hugo](https://gohugo.io/) to generate a static website. Hugo is a fantastic cross-platform static site generator tool built in Go. I recently dipped my toe into Django too, and I really enjoyed how my knowledge of [Handlebars](http://handlebarsjs.com/) templating  crosses over to both python and Go.

I found it incredibly easy to get up and running with a local server, and love how simply running `hugo server` sets up automatic server restarts when a file changes, and live reload  in the browser every time that happens.

I also considered GitHub's offering in this space, [Jekyll](https://jekyllrb.com/), and to be honest, there wasn't much in it. Hugo's slighly more beginner-friendly docs swung it for me. I'll definitely consider migrating in the future, especially since Jekyll is so closely integrated with GitHub pages. The technical implementation of the blog will evolve along with the writing!

Once I've learned more about Hugo I'll probably write a more in-depth post - I'm also hoping to contribute to the project on GitHub in the near future.



### Design & Writing

The look and feel of the blog is currently based on the [hugo-redlounge](https://github.com/tmaiaroto/hugo-redlounge) theme - I made a few simplifications and style modifications (for example adding a picture next to each post), but the structure is largely unedited. Using a theme has been an ideal way to get up and running quickly - I prioritised content creation over having a perfectly styled site. The design will be an iterative process, making small modifications and additions as I go along - look out for updates!



[Typora](https://typora.io/) is an amazing, minimal Markdown editor for writing posts in the flow, without distractions. The best part is it renders style **as you write**, meaning there is only a single window! All the markdown editors I've used previously have two - one for text entry and one for previewing your document.



### Build process & Hosting

I chose to use [GitHub Pages](https://pages.github.com/) to host this blog initially, mainly due to fact that it's free, but also because Git is a tool I'm very familiar with, Pages integrates seamlessly into my workflow.

[This blog post](https://blog.christophvoigt.com/setting-up-hugo-with-github-pages/) was invaluable in setting up a quick and easy CI process - I simply `git push` to the 'source' branch of my GitHub pages repository, and thanks to the magic of [Travis CI](https://travis-ci.org/), my changes are live within ~30 seconds.

Overall, hosting and CI was one of the sections that's taken the least work so far, since I was pretty happy with the setup 'out of the box'.

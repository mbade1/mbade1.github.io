---
layout: post
title:      "SINATRA Project: Mileage Tracker"
date:       2020-07-05 22:08:58 -0400
permalink:  sinatra_project_mileage_tracker
---

This was such a fun project, and it was a joy to actually create a web APP! After years of learning basic HTML and CSS, I have crafted web sites, and the idea of creating a dynamic web app terrified me! However, Flatiron helped me out so much, and I feel much more confident in being able to create a dynamic web app, capable of CRUD actions. 

For this project, I decided to use one of my new-found interests: running. Since Covid-19 started, I've started running, and in June ( for the first time ever), I was able to run over 10 miles! Running is great because of how simple it is: you simply slip on your running shoes and go. Well, what does it take to run? Sure, there are water bottles, headphones, hats, and all kinds of extra things, but everyone needs some form of a decent shoe to get started. Running equipment involves *just* running shoes, but please don't forget your t-shirt and shorts.  

Most pairs of running shoes come with a "mileage guarantee." Basically, most pairs of running shoes are guaranteed to last around 500 miles. This Sinatra App allows users to create a profile with a username, email address, and password. After their account is created, the user can then create new shoes with the following criteria: a name, date of purchase, new shoe mileage, current mileage, and price. Once the shoe is created, a user can then update their shoes with each run. The user can simply input their mileage and have it added to the current mileage of their shoes. Once the current mileage is more than the new shoe mileage, the user is notified that its "time to get new shoes!" 

While designing this web app, the major challenge I faced was ensuring that each file was collaborating with one another. For example, several controllers run the routes in this program, and as I was building the program, I realized that sessions were not being persisted through each route. After some troubleshooting, I had forgotten to inherit each new controller from the application controller. After adding inheritance to those controllers, I had another issue in the config.ru file:
```
use Rack::MethodOverride
run ApplicationController
use UsersController
use ShoesController
use RunsController
```

After moving the second line, ```run ApplicationController``` to the bottom of the controllers, everything started working fine. Always, ALWAYS set up all of the components of your enviornment and your routes (in their corresponding controller), so that you don't get frustrated later. Lesson #2: Make sure you're "running" the parent controller and "using" the children controllers. I will certainly remember this moving forward in lessons and projects. 

This was a very fun project, and it was a joy to see how Ruby logic plays into web app design. Before this project, Ruby was always a separate entity from the web page itself. Exploring and learning about ERB has totally blown my mind and changed the way I think about web programming. As I was working on this project, I thought about the many ways this app can be enhanced even further. I would love to get back into this project at some point and add other features, such as image uploads for each pair of shoes, and an individual run log. To dive even deeper, linking an apple watch app to a user account for each run would add even more detail and less human error in recording runs. With web design/software engineering, the possibilities truly seem endless!

**"Don't stop when you are tired. Stop when you are done."** - Unknown

GitHub Repo: https://github.com/mbade1/mileage_tracker

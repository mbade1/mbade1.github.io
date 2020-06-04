---
layout: post
title:      "CLI DATA GEM: Top 10 Flavors of Ice Cream!"
date:       2020-06-04 21:26:42 +0000
permalink:  cli_data_gem_top_10_flavors_of_ice_cream
---


"I'm not a great programmer; I'm just a good programmer with great habits." - Kent Beck

This quote truly reverberates through me in thinking about this project. There were times when I felt zen and understanding; and then there were moments that made me want to scream (this time, not for ice cream)! Either way, the code is written, the CLI app is working, and I'm so proud of the work that went into this first Flatiron project.

This project requires us to create a basic CLI Data Gem that goes "one level deep," meaning that the program asks the user for input, and the CLI provides information based upon that input. We were not *guaranteed* help from the Flatiron instructors, but rather we were given encouragement along this journey. However, before starting our project, I needed a plan, and it needed to encapsulate everything my CLI would do.

**Phase 1: Make a user story and an app flow diagram**

The user story for this project changed as I worked on the project (see **phase 5.0** below). However, my final user story for this project comes from a somewhat personal experience of mine as a kid. As a young kid, I grew up in two homes: my Mom's home (located in Baton Rouge, LA) and my Dad's home (located in Corpus Christi, TX). One summer I was with my Dad, and he came up with the idea to go to the Blue Bell Ice Cream Factory, located in Brenham, TX. It was a blast. We tasted TONS of flavors, and their portions of ice cream are definitely American-sized. After a full day of sugar rushes and crashes, I remember thinking, "I wonder what the best ice cream flavors are?" Fast-forward 20 years later, and this CLI Data Gem is born! 

This program prints a greeting, scrapes data from a "Top 10 ice cream flavors" article, and shows those 10 flavors to the user. The user then picks a flavor, and the CLI shows information about that flavor. The user can then exit the program or enter other flavors for more information. 

**Phase 2: NEVER FORGET ABOUT YOUR ENVIRONMENT!!!**

This is where things got tricky. I installed a gem, created a repo for my project, and started coding. I never even thought about how each file needed communicate together. After writing some basic code in two different Ruby files, I kept getting "uninitialized constant" error messages. I would delete the module's name before the name space for each class, and I would recode my (in my head) perfectly acceptable code. I would get frustrated, and wonder "Why is this not working?!?!"

After some time, I realized the environment was never set up properly. I had three different classes that would handle everything (cli, scraper, and blue_bell_final), but how can they collaborate without a phone, or connection between them? That's when I took a step back, watched and absorbed how Avi set up his environment, and started coding again.

**Phase 3: Write your CLI class**

The CLI class starts with the call method, which is used to run the entire CLI. Within this method, the scraper class gets info from the website, a welcome method prints a welcome message to the user, a product_listings method displays the flavors (after the user asks for the list), and the menu method shows more information on the selected flavor (flavor name, brand name, website to purchase, and the price). 

**Phase 4: Write the blue_bell_final class**

The blue_bell_final class takes in each instantiated flavor, including all of the information on each flavor, and stores each flavor in an array, called @@all. This class has 3 methods: initialize (which takes each new instantiated flavor and shovels each flavor to @@all), self.all (which reads the @@all array), and self.find_by_index(which takes in an argument of 'index' and reads the @@all array at that index).

**Phase 5.0: Write the Scraper class**

My CLI class was written. The blue_bell_final class was written... All I needed to do was finish out the scraper class. No problem, right? 

WRONG. This is where I had a major road block. The original website I was working with was https://www.bluebell.com/our-products/. This website displays all of the blue bell ice cream flavors, and my original plan for this project involved me scraping all of their flavors of ice cream, and returning a description for the flavor the user selected. It seemed obtainable and the website is easy to navigate. As I worked on this class, I would scrape the information needed. However, no information was being stored as a new object, meaning that no information was actually being read... So, I double checked each scraped item, quadruple checked my code, and realized there was a huge error I overlooked. The information I needed from this website is read via a JavaScript function, meaning that the only way I could access the needed information, I had to click on each individual product and scrape that new "page" of information. With 25+ flavors, this would be a huge overhaul on my code, and essentially, I would have to start over. 

After a long night of deliberation, I dropped into Flatiron's open office hours and asked about this predicament. Justin Anderson gave me some awesome ideas, and he was honest with me. He said I could scrape the id of each flavor, use an array to open each page that had the description, and then scrape those individual pages. Oh, and by the way, this would also involve the use a different form of Nokogiri (this one named poltergeist). The second option given is I could try to scrape a different web site, and redesign aspects of the CLI class to follow this new web site.

SO, I decided to keep the core of the project's user story almost the same, and scrape from a different website. Little 8 year old Michael doesn't get to see the Blue Bell Ice Cream Factory, but he will get to see the top 10 flavors of ALL TIME. Any kid who hears "top 10" of anything knows they're gonna hear something awesome.

**Phase 5.1: Rewrite the Scraper class with the new website**

Scraping isn't too bad, honestly. I got to work on this class, found the necessary items to scrape, and was able to implement it into my code. After the scraper class was finalized, I rewrote some *puts* and *if* statements in my CLI, so that it matched my new User story, and boom! Everything worked and was up and running.

**Conclusion**

To say this project was "easy" or that the code laid itself out to me would be an understatement. I'm proud of the hard work that went into this project. There were moments of understanding with my code, and moments where I was saying, "What the heck is going on?!"  I definitely learned a LOT throughout this project, and I know the habits I learned from this project has set me up for future success. Just remember, no matter what, when code gives you errors, eat some ice cream!http://)

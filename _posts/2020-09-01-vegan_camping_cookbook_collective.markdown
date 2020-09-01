---
layout: post
title:      "Vegan Camping Cookbook Collective"
date:       2020-09-01 16:02:47 +0000
permalink:  vegan_camping_cookbook_collective
---


Today I officially finished my fourth project for the Flatiron School's Software Engineering Program, woohoo! The idea for this project came from personal experience of mine. Three weeks ago, my wife and I took a camping trip to the Guadalupe Mountains and Lincoln National Forest, which are both located near the Texas/New Mexico border. As we were planning for our trip, we quickly realized that it's pretty difficult to plan out food for two vegans, who are staying in these areas (that is, unless you *want* to eat PB&J sandwiches every day...). We poured over the internet for food ideas, and it took us awhile to find some recipes that are actually sustainable for more than one meal. As soon as we got back, I started brainstorming for this project, and came up with an idea of a Vegan Camping Cookbook Collective. The idea is that users can send in recipes to the site admin, who can then post those recipes to the collective. Users can create their own cookbook by clicking on a fire icon, which represents a "like" option. The project utilized the Ruby on Rails API framework, specifically using PostgreSQL and Ruby in the backend with a vanilla JS, HTML, and CSS frontend. This SPA (Single Page Application) project utilizes JS to make fetch calls to the backend, which renders json on the frontend. So, the entire app works without having to refresh the browser!

## Step One: Planning
This project required a *lot* of planning. I wanted to make sure everything was lined up correctly, so that I could start coding with ease and without hiccups. The app has 3 models: a User which has many cookbooks, and has many recipes through cookbooks; a Recipe which has many cookbooks and many users through cookbooks; and a Cookbook which belongs to a User and Recipe. After deciding on these relationships, I started generating a resource model for each model, and moving vertically through the stack (migrations, models, seed data, controller action, and fetching). Thinking in terms of CRUD, I started with the **Read** actions, built that vertically for each model, and moved from there. Making sure everything was working was the toughest part. After building out the relationships and ensuring my frontend was communicating with my backend, it was time to move onto step 2: Styling

## Step Two: Styling
I had an idea of how I wanted this SPA to work, but I wanted to see it in a static environment, without any fetch calls. Simply the way it *should* look. So, I built out a static page, to see what the user see after they log in. Once logged in, the user is presented with an option to sort recipes by popularity, type of meal, and then "reset" or view All recipes again. I made sure the styling was correct for my static data, and came up with this static page:

![Static VCCC page](https://ibb.co/CBj92jL)

This was crucial for me, because it showed me how each recipe should be rendered to the page, how a user's cookbook will be shown, and what will be displayed/not displayed when a user wants to view their own cookbook.

## Step Three: Fetch Call to log in a User and Render all Recipes

Before I jumped into coding, I pseudocoded out the flow of what should happen from login to seeing All recipes. A user will need to fill out a form (name, email, and password) that is sent to the backend. The backend validates that user and logs them in (given all info is correct and passes validations). Then, the login page "disappears," the background image from the user login moves to the top of the window (vs. covering the entire browser window), the Sort methods are displayed, the container to view your cookbook is displayed, and finally, ALL recipes are rendered. Visualizing this flow and pseudocoding this out before coding helped so much and made coding go very smoothly. If I had jumped in without any planning, or kept all my plans in my head, this process would have been incredibly tedious. Now, over a somewhat short amount of time, everything was rendered, and my seeded data was correctly rendered to the DOM. 

## Step Four: Sorting Methods on the Backend

I wanted users to be able to sort through the recipes. The idea is that, even though there are 10 recipes right now, if in the future there happen to be 1,000+ recipes, multiple sorting methods will help with User experience in finding the recipes they *want* to add to their cookbook. So, I added each individual sort route in the backend, entered Rails C in the console, and tested them out. Once they were all working, I add Event Listeners to the frontend, so that the recipes can be sorted. This step was fairly simple and straight-forward - definitely a nice breather after Step Three.

## Step Five: Creating the Cookbook

Our recipes are on the screen **check!**, the sorting methods work **check!**, and now it's time to add recipes to each User's Cookbook. The idea of it is simple: A User clicks on the "fire" icon next to each recipe, which is similar to a "like" option, and the recipe is added to the cookbook. Easy enough, right? The logic and backend is easy to create. What wasn't so easy is determining how this would be displayed to the user. Every time the sort methods are called, the page re-renders the recipes associated with that sort method. For example, if I sorted out recipes by *breakfast*, a fetch request is made to localhost:3000/sort_breakfast. That action in the controller looks over all of the recipe's meal keys, grabs all recipes with a 'breakfast' value, and sends those recipes to the front to be rendered through the **renderRecipes()** function. The flow makes sense, and it's easy to explain. What isn't easy is how will the fire symbol actually represent each recipe put in the cookbook? 

Rather than changing the color of the fire symbol, and sending two fetch calls to render sorted recipes, alongside recipes that are in the User's cookbook, I decided to do something else. When a user clicks on a recipe they want in their cookbook, the name of that recipe appears under the "View Your Cookbook" container, alongside a red fire symbol. From here, the user can either view their cookbook or delete a recipe from their cookbook. This felt like a good way to go, and it created less stress in making this app work. 

## Step Six: Wrapping Up

After everything was working, I added some extra styling, a favicon, and "spruced up" the frontend. Also, I distributed my JS files from one large index file to several smaller JS files, utilizing the "separation of concerns" principle. One file contains all event listeners, another has functions for each User's cookbook, and a third file has the signup through renderRecipes() function flow. Looking back, I should have separated my files a long time ago, so that everything was in their designated space, making refactoring easier. In the future, I would love to add more features, such as an upvote/downvote system, so that users can see what the most voted-on recipes are. Also, I would love to add a feature for users to email their cookbooks to themselves, or other family members. That way, after a cookbook is created, their recipes can be sent and saved somewhere outside of the app. This was a really fun project, and I look forward to my assessment! 

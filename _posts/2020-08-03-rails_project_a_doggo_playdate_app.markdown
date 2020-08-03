---
layout: post
title:      "RAILS Project: A Doggo Playdate App!"
date:       2020-08-03 16:14:08 -0400
permalink:  rails_project_a_doggo_playdate_app
---

When thinking about what to base this Rails project on, I thought about how Covid-19 has affected so many areas of our lives. For many dog owners, dog parks have officially shut down in most major cities. With this app, users are able to add new Parks, new Playdates, and a Review for each Park. There are several validations with each newly created object, and users can not edit/delete other users' information. If you would like to see a walk through of this app, click here: [Doggo Playdate App](https://www.youtube.com/watch?v=R6iXLOJSrwY&feature=youtu.be).

## Making a Diagram
  
The first step to this project involved laying out a diagram of how each Model will relate to each other, and what each Model's attributes are. For instance, for the Users Model, the following relations were established:

```has_many :parks```
```has_many :playdates``` 
```has_many :comments, through: :parks```

  Four models were created in total (User, Park, Playdate, and Comment), and all of these have multiple relations with each other and *through* each other. I spent a lot of time writing out these relations and entering the console ```rails c``` to make sure each relationship was established correctly before moving forward. 

  Based off of the diagram I created for this project, I then created my schema as well. This included keeping relationships consistent (ex: the comments table has a :user_id and :park_id, since it belongs_to users and parks). This was fairly simple, since the relationships had been thoughtout and diagrammed.

## Resources and Controllers

After establishing my Models and Schema, it was time to get started with Resources and Controllers. I started with the root path, login routes, and session routes for Users. From there, I made a skeleton app, making sure each route had a corresponding view, and the route path was correct. This involved nesting resources and ensuring there was a corresponding view for each action in each Controller. At first, my routes were not nested. For instance, to see playdates for a specific park, my route would display: ```http://localhost:3000/playdates/1``` instead of ```http://localhost:3000/parks/1/playdates/1```. After nesting the playdates resources within the parks resources, everything was up correctly. 

## form_for... what's a form for anyway?

Every Model has some form associated with it - logging in, signing up, new playdates, new comments, editing comments, editing playdates... and the list continues. At first, I was having issues with these forms, because some of these forms were nested, while others weren't. I kept getting errors for these pages, because I wasn't passing in the id for each parent resource. For instance, for each new Playdate, I had:

  ```<%= form_for (@playdate) do |f| %>```
	
	This was causing errors since my route for a new playdate was nested under parks. The above form would have worked perfectly fine for a new_playdates_path. However, our form needed to line up with new_PARKS_playdates_path, taking in the argument of the park and the new playdate. So, the form needed to take in two arguments:
	
	```<%= form_for ([@park, @playdate]) do |f| %>```
	
	This was a common error I was getting with multiple nested forms, and after discovering the answer to this error, my forms were being posted correctly, without errors. These new/edit forms were also refactored into a separate form file within each view folder.
	
## views/parks/show
  
  The parks/show view started to quickly contain a LOT of code as the app grew. This page shows a table of the upcoming playdates, sorted in date order. It also shows the average review for each park. Then, it also has a reviews(comments) section with each individual user's rating of the park. To say this page started looking messing is an understatement...
	
### Refactoring to the rescue!
	
So, just like some of my forms this view needed some refactoring. I could have used a helper method for these, but within each block, I also had a good amount of HTML code. So, to keep the styling the same, I made three separate forms within views/parks: park_average_reviews, park_playdates_table, and park_reviews. These forms are there to help break up the code for this view, which makes views/parks/show move from 100 lines of code to only 17, and each form is in a smaller, digestable amount of code!
	
## Facebook OAuth
	
To add more options for a user to login/signup, I added Facebook OAuth to my app. This process was fairly simple, all thanks to the omniauth and facebook-omniauth gems! As an added level of security, I used the dotenv-rails Gem, to hide the Key and Secret from Github and users. *Always do this, otherwise you're simply handing the keys to your Facebook profile... YIKES!*
	
## Make it look GREAT
	
  After refactoring and making sure the logic and MVC structure was solid, we needed to make it *look* great. After working with just HTML for awhile, it was nice to add a fixed navbar with dynamic links, some stock images of dogs (I mean, who doesn't like looking at puppers and doggos?), Arial font family, and some styling for each table, list, and container. Even though your project may not *require* this, do it anyways.
	
## Conclusion

  In Conclusion, I learned SO MUCH from this project. This project reaffirmed my understanding of the MVC structure for Rails and modern-day frameworks. Doing hands-on projects like this let me learn and relearn code that is standard in many CRUD-based web apps. If I had to redo this project, I would have thought about the structure of my routes FIRST, before starting to add forms to views. Rails is such an amazing Framework - sometimes it's "too good" and "guesses" your paths before you've written anything! I enjoyed every step of this process, and I can't wait for my project evaluation!!
	


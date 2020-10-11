---
layout: post
title:      "Trail Run Planner"
date:       2020-10-11 01:04:13 +0000
permalink:  trail_run_planner
---


Phew! This is it - the final project for Flatiron! I can't believe I'm at the finish line for such an incredible, challenging bootcamp. For my final project, I wanted to create something that is definitely in line with the theme of other projects I've made, as well as make something that will be useful for the future. A month ago, my wife and I were hiking Guadalupe Mountain in West Texas, and we did not bring enough water. We really struggled on the final 2 miles of the descent and were so relieved to get to our car. The Trail Run Planner app will help people like us, who forget what to pack for trail runs! This app allows users to view trails in their area and add days to run specific trails to their personal running journal. Within their journal, users can then select what items they need to bring on their run, such as a cell phone, jacket, water, food, etc. Right now, the app sends an alert to the user of the items they need to bring. However, in the future, I would like to implement either an iCal or Email reminder with the information of what to bring on the hike. 

## Phase 1: Planning

Flatiron has taught me how to code, and how to PLAN before coding. We started with a user story:

*Carl is an avid trail runner who loves discovering new trails and making new paths. Carl’s excitement for the outdoors constantly makes him accidentally forget to pack everything for his runs. In fact, Carl recently went running on a desert trail and forgot to bring water! With the Trail Running Planner (TRP), Carl doesn’t need to worry about forgetting his trail running gear ever again. Carl will be able to:
1. View trails in his area.
2. See detailed information on each trail.
3. Add each upcoming trail run to his personal journal with the date and a packing list of items to bring on the trail.
*

## Phase 2: Backend

For this project I created a Rails API to handle users and their journals. Creating the API using vertical alignment is what helped make this process go quickly (plus the help of **$rails g resource**) The database only has 2 models: users and journals. At first, I thought a trails model would be necessary, but you'll see why it's not necessary in a little bit. After creating the model's relationships, enabling CORS for fetch calls, and testing models in the console, I established my routes and tested my controllers. To make sure each controller method was being hit, I used binding.pry within each controller method before moving to the frontend.

## Phase 3.1: Frontend

To get started on the frontend, our project required React, so with the useful **$create-react-app** command, I was able to get a basic app up and running. I immediately connected the top-level component, index.js, to the Redux store, to keep state in one place. I also knew, from planning, that my app would use multiple fetch calls to 3rd-party APIs and my Rails backend. So, I connected [thunk](https://imgflip.com/i/4i2u7u) middleware to the store!

## Phase 3.2: React 3rd-Party API Fetch Calls

I wanted this app to be incredibly dynamic. I didn't want to make an app that would work for *just* Austin, TX, or *just* San Francisco, CA. This app needed to be useable anywhere in the USA.

 ![](https://www.rei.com/blog/wp-content/uploads/sites/4/2016/06/hikingprojectlogo.png?resize=150%2C150)

The Hiking Project API was the perfect place to go for this. They have an API with thousands of trails in and around the US. According to their docs, in order to make a fetch call to a specific latitude and longitude, like this: 

https://www.hikingproject.com/data/get-trails?lat=40.0274&lon=-105.2519&maxDistance=10&key=example-key

So, I couldnt' just enter "City", "State" like I had wished... I had to find a way to get latitude/longitude from the name of a city, and pass that info into the Hiking Project API. Enter Geocodio!

![](data:image/png;base64,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)

With Geocodio, all you have to do is register for an API key, then pass in the city/state abbreviation, and voila! You have a latitude/longitude ready to go! Getting trails for any location in the US was now possible, by making back-to-back fetch calls to each API:

```
export const fetchCityAndTrails = (city = "Foresta", statee = "CA") => {
    return (dispatch) => {
        fetch(`https://api.geocod.io/v1.6/geocode?q=${city}%2c+${statee}&api_key=KEY`)
        .then(resp => resp.json())
        .then(coordinates => fetchTrails(coordinates))
    

        const fetchTrails = (coordinates) => {
        fetch(`https://www.hikingproject.com/data/get-trails?lat=${coordinates['results'][0]['location']['lat']}&lon=${coordinates['results'][0]['location']['lng']}&maxResults=50&key=KEY`)
        .then(resp => resp.json())
        .then(trails => dispatch({
            type: 'FETCH_TRAILS',
            payload: trails
        }))      
        } 
    }
}
```


## Phase 3.3: State, STAte, STATE!

React uses state to throughout all of its components. State can be utilized in one component, or passed around via props, or held in the Redux store. Learning how to manage state, when to setState, and do anything with state took a good amount of time for me. For instance, my app was firing a fetch call to find a User immediately upon each reload. Figuring out how to use dispatch, map it to props, etc. took a long time, filled with hours of debugging. In the future, I need to remember the Redux pattern for state:

![](https://krasimir.gitbooks.io/react-in-patterns/content/chapter-09/redux-architecture.jpg)

## Phase 3.4: Trails and Journal Container

Now that our Redux problems were fixed, it's time to actually use that information and do something with it! Both of these containers pass props to **Trails.js** and **Journals.js**, respectively, and use these props to render each item. By using the map function, rendering was simple. Plus, with some CSS magic, these components were looking great. 

## Phase 4: Backend reworking

My original thought behind the process of saving a trail was this:

1. User sees a trail he or she wants to run on.
2. User clicks save, which saves the id (from Hiker Project) of that trail and date of the User's run into the Trail table in the database.
3. When user views their Running Journal, the journal pulls each trail from the database and sends a fetch request to Hiker API's database, getting information based on the id of that trail.


Remember how I thought a Trail model would be necessary? Well, after trying to make this method work, I decided to go with a different approach that didn't involve the Trail model:

1. User sees a trail he or she wants to run on.
2. User clicks save, which saves ALL necessary information from that trail into the Rails API backend database. 
3. When the user views their Running Journal, the Journal controller matches the user_id with each designated journal for that user.
4. Each matching journal then sends their stored information about each trail to the frontend to be rendered.

This created a similar setup to my original, and while I didn't like having to renavigate my backend, this did not cause any issues and made the app work flawlessly!

## Phase 5: Sit back and look for some trails to run on

This project took about two weeks to build, and learning the power of React has been incredible. React is a fast, light-weight library, filled with endless possibilities. I loved building this app, and I can't wait to learn more JS libraries! But, for now, it's time to hit the trails! 

![](https://media4.giphy.com/media/3ohzdOMnKmZ7Vg9pbq/giphy.gif)








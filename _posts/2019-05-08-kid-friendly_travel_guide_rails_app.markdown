---
layout: post
title:      "Kid-Friendly Travel Guide Rails App"
date:       2019-05-08 19:08:31 -0400
permalink:  kid-friendly_travel_guide_rails_app
---



Initially, I planned to do my last Sinatra project in Rails. However, I found out that the next project, Rails with Javascript, will be an expansion of our Rails one. Since I want to showcase different projects in my portfolio, I decided to start from scratch instead.

**Planning**

This was one of the most challenging part, I think. Thankfully, I got the chance to meet up with Tadea and Ludmilla again in NYC (WeWork). They are also FS students, and Tadea happened to be doing her Rails project as well. It was a weekend so there weren't many people in there, and we got to use one of the conference rooms. Ludmilla, who is already in the Javascript section, willingly laid out on the whiteboard/big screen how we are going to approach the project, figure out our associations, etc.

After hours of brainstorming, I decided to build a Family-friendly Travel Guide application since I love to travel with my family. See the structure below.

![](http://i65.tinypic.com/mr2zdi.png)




**Challenges and Lessons**

Coming up with a project idea was a struggle alone, but sticking to it was another challenge! I wasted a day thinking about other project ideas only to come back to the original one. I could have used my time for something else.

I also struggled setting up my Google Omniauth. I've watched tutorials, read articles, etc. but found no solution. So I decided to try Facebook Omniauth and Tadea helped me set it up through Zoom. However, we couldn't figure out why my `session[:user_id] = @user.id` isn't setting. She suggested I reach out to the Rails section lead, Jen Hannsen, through Slack. Jen guessed that there's an issue with my validations and that I should add @user.save! before `session[:user_id] = @user.id` to find out the error. It turned out that I needed a `name` since it's one of the user's attributes that I assigned in my validations and not a `username`!

It's one of those moments where I felt a bit stupid but I know that even experienced developers still make mistakes. I've learned that there is no shame in asking for help and I wish I reached out sooner! Aside from the study groups, video tutorials, and other sources online, I can truly say that pair programming helped me get through the project. I have to add that the *#100daysofcode* challenge initiated by Meg Gutshall helped me keep the momentum and get focused!

**Future Features**

I don't know the requirements yet for the Rails JS project but here are some additions that I would like to have next: background image, more images, better ratings, add comments, more models, search feature, and probably a show page for each user.

I'll insert my github link and walkthrough here once I submit my project for review.


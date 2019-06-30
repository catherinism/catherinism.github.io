---
layout: post
title:      "Rails with JS Project Guide"
date:       2019-06-30 12:15:40 -0400
permalink:  rails_with_js_project_guide
---


No idea how to start your Rails with Javascript portfolio project? You're not the only one. I had to watch many videos and read many articles before I could begin my project. One of the blogs I read was [Christina Williams'](http://christinaxtwilliams.com/rails_and_javascript_review_and_portfolio_project) (which by the way inspired me to write this blog. Thank you, Christina!) and it tremendously helped me and a few others I  know. I must say that making the project itself helped me understand Javascript more.

Here are the steps I took for my Rails with JS project:

* I set up a meeting with the current JavaScript Project Section Coach, Dalia Sawaya, and she was very helpful in making me understand what the project requires. She also explained:

> Javascript Model Object = Javascript version of a Ruby Object
> Prototype Function = an instance method in Ruby
> Constructor Function = Initialize in Ruby

Additionally, she recommended the following videos:
[Debugging in Chrome Dev Tools with JS](https://developers.google.com/web/tools/chrome-devtools/javascript/)
[Index and Show requirement](https://www.youtube.com/watch?v=oHPM0ekV7zQ)
[Form Submission requirement](https://www.youtube.com/watch?v=Yd0nH9CWWfo&amp=&feature=youtu.be)

I would also recommend you watch this [Rails JS study group](https://youtu.be/b93S2_Hc8z8) by Brad Smith.

* Although I think I could have just continued my Rails project or create a branch, I decided to make a duplicate of that project instead.

1. Create a new repository - in my case, I named it family-friendly-travel-guide-js
2. Duplicate my Rails project repo by following [these steps](https://help.github.com/en/articles/duplicating-a-repository)

* Added these gems to my Gemfile
```
gem 'jquery-rails'
gem 'active_model_serializers'
```

Tip: Don't forget to bundle install. Also, I read that Turbolinks doesn't go well with jquery-rails. I don't know exactly why but when I removed it from my Gemfile and application.js, my project ran more smoothly and it stopped me from refreshing my index because it used to not render it via JSON but Rails.

*  Required directives to the application.js file
```
//= require jquery
//= require rails-ujs
//= require your-js-file
//= require_tree .
```

[Reread Javascript Manifests](https://learn.co/tracks/full-stack-web-development-v7/rails-and-javascript/asset-pipeline/javascript-manifests)

* Added serializer
 You can generate a serializer by runni



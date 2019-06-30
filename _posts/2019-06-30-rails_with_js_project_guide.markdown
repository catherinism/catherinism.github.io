---
layout: post
title:      "Rails with JS Project Guide"
date:       2019-06-30 12:15:40 -0400
permalink:  rails_with_js_project_guide
---


No idea how to start your Rails with Javascript portfolio project? You're not the only one. I had to watch many videos and read many articles before I could begin my project. One of the blogs I read was [Christina Williams'](http://christinaxtwilliams.com/rails_and_javascript_review_and_portfolio_project) (which by the way inspired me to write this blog. Thank you, Christina!) and it tremendously helped me and a few others I  know. I must say that making the project itself helped me understand Javascript more.

**Project Walkthrough**


<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/Wk4fen__e_w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


***Here are the steps I took for my Rails with JS project:***

**1. Meet up with your project section coach**

I set up a meeting with the current JavaScript Project Section Coach, Dalia Sawaya, and she was very helpful in making me understand what the project requires. She also explained:

Javascript Model Object = *Javascript version of a Ruby Object*

Prototype Function = *an instance method in Ruby*

Constructor Function = *Initialize in Ruby*

Additionally, she recommended the following videos:

[Debugging in Chrome Dev Tools with JS](https://developers.google.com/web/tools/chrome-devtools/javascript/)

[Index and Show requirement](https://www.youtube.com/watch?v=oHPM0ekV7zQ)

[Form Submission requirement](https://www.youtube.com/watch?v=Yd0nH9CWWfo&amp=&feature=youtu.be)

I would also recommend you watch this [Rails JS study group](https://youtu.be/b93S2_Hc8z8) by Brad Smith.

**2. Duplicate your Rails project (optional)**

Although I think I could have just continued my Rails project or create a branch, I decided to make a duplicate of that project instead.

* Create a new repository - in my case, I named it `family-friendly-travel-guide-js`
* Duplicate Rails project repo by following [these steps](https://help.github.com/en/articles/duplicating-a-repository)

**3. Add these gems to your *Gemfile***
```
gem 'jquery-rails'
gem 'active_model_serializers'
```

Tip: Don't forget to *bundle install*. Also, I read that `turbolinks` doesn't go well with `jquery-rails`. I don't know exactly why but when I removed it from my *Gemfile* and *application.js*, my project ran more smoothly and it stopped me from frequently refreshing my index because it used to not render via JSON right away.

**4. Require directives to the *application.js* file**

Mine looks like this:

```
//= require jquery
//= require rails-ujs
//= require bootstrap-sprockets
//= require activestorage
//= require guides
//= require_tree .
```

`//= require guides` is my `guides.js` file. If needed, reread the [Javascript Manifests Lesson](https://learn.co/tracks/full-stack-web-development-v7/rails-and-javascript/asset-pipeline/javascript-manifests)

**5. Add serializer**

I only added one serializer file to my serializer folder. Run `rails g serializer filename`

My serializer looks like this:

```
class GuideSerializer < ActiveModel::Serializer
  attributes :id, :title, :summary, :lodging, :itinerary, :destination_location, :airport, :baby_gear_rental, :park, :zoo, :restaurant, :luggage_storage

  belongs_to :destination
  has_many :ratings
end
```

**6. Render JSON**

I put JSON to my `index`, `create`, and `show` methods in my `guides_controller.rb` file

**INDEX**
```

  def index
    if !params[:destination_id].blank?
      @destination_id = Destination.find_by(id: params[:destination_id]).id
      @guides = Guide.where(destination_id: @destination_id)
    else
      @guides = Guide.all
    **  respond_to do |f|
        f.html {render :index}
        f.json {render json: @guides}
      end**
    end
  end
```

**CREATE**

```
def create
    @guide = current_user.guides.build(guide_params)
    @guide.user_id = current_user.id
    if @guide.save
    **  render json: @guide**
    else
      flash[:message] = "#{@guide.errors.full_messages.to_sentence}."
      render :new
    end
  end
```

**SHOW**

```
def show
 **   respond_to do |f|
      f.html {render :show}
      f.json {render json: @guide}
    end**
  end
```

**7. Start coding in your JS file**

Although I had to make some changes to my layout, views, and other files, I spent more time coding in my guides.js file. Following along the videos I mentioned above really helped me finish this project.

```
$(document).ready(function() {
  // console.log('hello')
  guidesIndexClick()
  showGuide()
  newForm()

})

function guidesIndexClick() {
  $('.all-guides').on('click', (e) => {
    e.preventDefault()
    // console.log('hello again')
    history.pushState(null, null, 'guides')
    fetch('/guides.json')
      .then(response => response.json())
      .then(guides => {
        $('.container').html('')
        guides.forEach(guide => {
          // console.log(guide)
          let newGuide = new Guide(guide)
          let guideHtml = newGuide.formatIndex()
          // console.log(guideHtml)
          $('.container').append(guideHtml)
          // console.log(newGuide)
        })
      })
  })
}

function showGuide() {
  $(document).on('click', '.show_guide', function(e) {
    e.preventDefault()
    $('.container').html('')
    let id = $(this).attr('data-id')
    fetch(`/guides/${id}.json`)
    .then(response => response.json())
    .then(guide => {

      let newGuide = new Guide(guide)
      let guideHtml = newGuide.formatShow()
      $('.container').append(guideHtml)
      })
  })
}

 function newForm() {
  $(document).on('submit', '#new_guide', function(e) {
    e.preventDefault()
    console.log('event preventend')

    const values = $(this).serialize()

    $.post('/guides', values).done(function(data) {
      $('.container').html('')
      const newGuide = new Guide(data)
      const guideHtmlToAdd = newGuide.formatShow()
      $('.container').html(guideHtmlToAdd)
    })
  })
}

function Guide(guide) {
  this.id = guide.id
  this.title = guide.title
  this.destination_location = guide.destination_location
  this.summary = guide.summary
  this.airport = guide.airport
  this.lodging = guide.lodging
  this.restaurant = guide.restaurant
  this.park = guide.park
  this.zoo = guide.zoo
  this.baby_gear_rental = guide.baby_gear_rental
  this.luggage_storage = guide.luggage_storage
  this.itinerary = guide.itinerary
}

Guide.prototype.formatIndex = function() {
  console.log(this)
  let guideHtml = `
  <div class="col-md-4">
  <a href="/guides/${this.id}" data-id="${this.id}" class="show_guide"><h2 class="guide-title">${this.title}</h2></a>
  <p class="guide-destination">${this.destination_location}</p>
  </div>
  `
  return guideHtml
}

Guide.prototype.formatShow = function() {
  console.log(this)
  let guideHtml = `

  <div class="col-md-12">
    <h3>${this.title}</h3>
    <p class="guide-destination"> <i class="fas fa-globe-americas"></i> ${this.destination_location}</p>
  </div>

  <div class="col-md-6">
    <p class="guide-summary"> ${this.summary}</p>

    <hr class="my-4">
    <h2 class="guide-destination">Itinerary</h2>
    <p><i class="fas fa-map-signs"></i> ${this.itinerary}</p>
  </div>

  <div class="col-md-6">
    <h2 class="guide-destination">Details</h2>
    <p><i class="fas fa-plane-departure"></i> ${this.airport}</p>
    <p><i class="fas fa-bed"></i> ${this.lodging}</p>
    <p><i class="fas fa-utensils"></i> ${this.restaurant}</p>
    <p><i class="fas fa-tree"></i> ${this.park}</p>
    <p><i class="fas fa-hippo"></i> ${this.zoo}</p><br>
    <h2 class="guide-destination">Nearby</h2>
  </div>

  <div class="col-md-3">
    <h2 class="guide-destination"><i class="fas fa-baby-carriage"></i> Baby Gear Rental: ${this.baby_gear_rental}</h2>
  </div>

  <div class="col-md-3">
    <h2 class="guide-destination"><i class="fas fa-suitcase-rolling"></i> Luggage Storage: ${this.luggage_storage}</h2>
  </div>
  `
  return guideHtml
}
```

> I wanted my images to show just like in my Rails project, but I realized that it's more important to understand and finish this project first then go back to it at a later time.

![](http://i66.tinypic.com/2i93w5f.png)

![](http://i63.tinypic.com/124x84w.png)


Hope this can help other students who are about to do their Rails with JS projects. Can't wait to start React!








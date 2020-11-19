---
layout: post
title:      "Rails - Associations (and Nested resources)"
date:       2020-11-19 19:51:54 +0000
permalink:  rails_-_associations_and_nested_resources
---


In this blog post I’m going to discuss associations and then briefly touch on how they can affect your nested resources in your routes.rb file, if you have chosen to use them that is. 

When I first transitioned to Rails it’s intuitiveness or “magic” made me jubilant in comparison to the “not-so-intuitive” Sinatra. Nevertheless, the associations and how they relate to nested resources, along with nested resources themselves, had my head in a spin. My hope as the author of this blog is to bring clarity to a subject which I found very unclear to begin with.

# Associations:

The crucial thing to do before anything else is to sit down and work out which models you need to build out and then how they relate to each other. This will effect the nested resources so it is key to get your associations in your models crystal clear from the get-go!

I had four models for my project:

**User:**
```
    has_many :posts
    has_many :comments
    has_many :commented_posts, through: :comments, source: :post 
    has_many :categories, through: :posts
```

**Post:**
```
  belongs_to :user
  belongs_to :category
  
  has_many :comments, dependent: :destroy
  has_many :users, through: :comments
```

**Comment:**
```
    belongs_to :post
    belongs_to :user
```

**Category:**
```
     has_many :posts
     has_many :users, through: :posts
```

I always start with the user model and go from there, it seems to be the best way for me to keep track in the beginning. Once the User model is built out I moved on to the Post model because they are the two main tables which need joining by another table/model. In my case I joined them with the Comment table/model, which as you can see from my code joins them both rather nicely just by “belonging” to them both. Now ActiveRecord knows how these models relate to each other.

I added Categories as an additional design feature for my app but it could have worked just as easily as the join table.

You may also notice that in my Post model there is a line which reads “has_many :comments, dependent: :destroy,” this association is slightly more complex, but what it means is that if a User deleted a post all of the comments for that post would be deleted from the database too. Feel free to use that lovely little association if you so feel.

Now that all the Associations are all set up nicely I am going to explain how this all works in relation to nested resources. 

# Touching on Nested Resources:

```
    resources :users do
      resources :posts, only: [:new, :create, :index, :edit, :update] do
      resources :comments, only: [:new, :create, :index, :edit, :update]
      end
    end 
```

Above is my nested resource for this Rails project, this took some time to implement. Essentially what the above code means is that the browser will keep track of/follow along where the user clicks and expect the route for the user to travel along whilst they are using the apps features. For example if the User wanted to comment on a post they would travel a route that looked like this: 

http://localhost:3000/users/2/posts/1/comments/new?

The User followed by their Id. Then the chosen Post followed by its id. Then the user arrives at the Comments/new? Page, which is means that the user is faced with the option of adding a “:new” comment. The route would look similar for “:create, :index, :edit and :update” if the user travelled along that pathway/route.

If the associations hadn’t been set up properly in the first place it would be impossible to nest any resources or routes because both Rails and the browser would have no idea how they associate/relate to each other.

Once I started visualising the routes and resources as actual routes on a map it all became a lot clearer!



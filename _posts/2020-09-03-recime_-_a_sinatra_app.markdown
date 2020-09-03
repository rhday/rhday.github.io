---
layout: post
title:      "Recime - a sinatra app!"
date:       2020-09-03 05:18:43 -0400
permalink:  recime_-_a_sinatra_app
---


I thoroughly enjoyed building this application and learned how to implement features I had really wanted to know about, namely how to 'like' and 'un-like' a post! This function is not as straight forward as it sounds. I had to programme this function so that the User can only like an individual post once and that they can only unlike a post if they have previously liked it. 

``` 
post '/posts/:id/like' do 
        @post = Post.find(params[:id])
        
        if already_liked?
            flash[:error] = "You can't like the same post twice!"
        else
            @like = Like.create(user: current_user, post: @post)
        end 
        
        @likes = @post.likes 
        
        redirect "/posts/#{params[:id]}" 
    end 
		```
		
		In the above piece of code, we start by creating the relationship between the User, Post and Like by creating an instance of a new like. We then enter our logic and the like just created's validity is checked. If the User has already liked this post an error message will show telling them that they have already liked this post! If the User hasn't already liked this post then we enter our 'else' statement, where we assign the instance of that like to an instance variable. Now to be able to display the post's likes we assign each instance of a specific like to the "@likes" instance variable to be displayed in our view/show page. It then redirects the user to the updated page.
		
		The 'unlike' function, shared similarities with the 'like' function but was altogether a different request to the server - a 'delete' request!
		
		```
		delete '/posts/:id/unlike' do 
        
        @post = Post.find(params[:id])
        
        @like = Like.find_by(user: current_user, post: @post)
				
        @likes = @post.likes
        
        if @like
            @like.destroy
        end 
				
        erb :"posts/show"
				
    end 
		```
		
		Our delete request, or 'unlike' function, starts by finding the correct post. We then find and grab hold of the specific instance of the like in question in order to delete it. Assign this to an instance variable "@like" and then we use the "@likes" instance variable again to communicate the change of likes to our show page. Now that our function has grabbed the specific instance of a like it checks whether or not the instance of the like exists because if it does exist then our function can delete it. However if there is no instance of a like then there is nothing to unlike and the show page stays unchanged.
		
		```
		<form class="" action="/posts/<%= @post.id %>/like" method="post">
    <input type="submit" name="" value="Like this Post!">
</form>
<form class="" action="/posts/<%= @post.id %>/unlike" method="post">
    <input type="hidden" name="_method" value="delete">
    <input type="submit" name="" value="Unlike this Post!">
</form>
<p>Likes:<%= @likes.count %></p>
```

This final snippet of code is from our show page and is how we render our 'like/unlike' function to the user. At the bottom of the function we can see our "@likes" instance variable in use displaying the ever changing tally!


		

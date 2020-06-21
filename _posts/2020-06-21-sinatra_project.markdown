---
layout: post
title:      "**# sinatra project**"
date:       2020-06-21 13:09:03 +0000
permalink:  sinatra_project
---


"# This  sinatra project has been very difficult. I have struggled with the relationships between the views and controllers resulting in a lot of NoMethodErrors,  like this one:"

```
NoMethodError at /ringers/2

undefined 
```

I got my app functioning but it wasn’t restful at all. The relationships between the MVC, coupled with the using html forms for the first time was really challenging. It took a lot of time, work on patience on both my side and that of my cohort lead - thank you Micah.

Now that I feel my knowledge of forms is much more proficient, I have managed to see what it was that was confusing me to begin with. I just have to match up the html form in the view with the relative controller like so:


`<form action="/ringer_teams" method="post">
        <input type="hidden" name="_method" value="delete">
        <input type="hidden" name="ringer_id" value="<%= rt.ringer_id %>%">
        <input type="submit" value="Terminate contract">
</form>`

`delete "/ringer_teams" do
        rt = RingerTeam.find_by(ringer_id: params[:ringer_id], team: current_user.team)
        rt.destroy
        redirect to "/dashboard"
 end`
 
 Now that I have a much better grasp on how forms work, my app’s user experience has got much better!

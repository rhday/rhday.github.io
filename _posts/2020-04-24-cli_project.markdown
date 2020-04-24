---
layout: post
title:      "cli project."
date:       2020-04-24 13:17:10 +0000
permalink:  cli_project
---


This project has been quite tough from start to finish. Learning how objects collaborate was difficult and getting to grips with scraping was so fiddly! I have to say though, scraping is fun and this project has started to make me feel like a real programmer!

In the beginning it was all Labs and ReadMe docs; being able to put that into practice was exciting, although certainly not without its challenges. Getting the skeleton code set up, whilst being time consuming did help make me feel more “connected” to my project. 

An error I seemed to keep getting close to the end was that my function was not printing out what I had scraped to the screen. In the first case it was because the url that ‘nokogiri’ was accessing needed to be changed to dynamic code, which follows the users pathway, scraping as it goes. The other was more me not seeing the problem, it required a bit of thinking and help from other programmers. Going back over the code I had already written, step by step helped me isolate and thus fix it. Now that I have finally fixed it and the CLI is finished, I realise that it was so simple and I just couldn’t see it, with a fresh pair of eyes and a well rested brain I made short work of it in the morning!

This tiny snippet of code is all I was missing: 

recipe.method.each do |method|
                puts "\n#{method.name}.\n"
            end 

Something so small caused such an issue. It made me feel great that I solved it myself.

The project taught me to relax a little bit more when it comes to doing the work, if something isn’t going in…it will, just give it time! I just built my first computer program!

R.

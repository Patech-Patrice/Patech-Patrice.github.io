---
layout: post
title:      "Building my first CLI Application"
date:       2019-01-31 16:11:15 +0000
permalink:  building_my_first_cli_application
---


I’ve always prided myself on never taking the easy way out.  I work hard and never back down from a challenge.  Since beginning my coding journey, every day there is a new obstacle to overcome.  After all, learning any new language is challenging, and Ruby definitely had its share.  My very first project as a student at Flatiron School was to build a Ruby Gem that provided a Command Line Interface to an external data source and had to be composed of an Object Oriented Ruby application. 

 Requirements of the project were to:

* Provide a CLI
* scrape data from a website using Nokogiri and Open-URI 
* provide data that was at least one level deep  
A “level” generally shows what choice a user can make, and then gives detailed information about that choice to the user. From there, we are able to drill down to a specific item or request.

I was really nervous starting out.  This was the very first time that I actually had to write code from scratch! No tests to help point out errors, no notes in the code to tell me what should go where.  I even had to give permissions in the terminal for the user to be able to interact with the application, which was always a given in lessons on Learn.  After spending many weeks going through the lessons and doing the labs, I was confident that I was ready to tackle the task before me.  I decided that I needed to first figure out what I wanted my project to be about.  I chose movies because I am a huge fanatic, and there are many websites dedicated to that topic.  The next step was determining what the users would be doing and how I wanted them to interact with the application.  I wanted it to be as simple as possible, so as not to confuse anyone.  

Once I had those steps figured out, I needed to choose a website that was scrapeable, which was not easy! Four websites into my search, I finally found one deemed worthy to the Ruby gods. Without the right site, I would not be able to write a lick of code.  The site determines what your application does by the information that it provides.  

Now we’re off to the races! I know what my application will do and how I want it to interact with users.  Time to write some code! 

First things first, you have to create an executable file.  This file is located in the bin/, and code here relates to actually running our program.  Without this directory, we are unable to run our program from the command line, nor will users be able to interact with it.  File permissions must also be given in order to execute a file via command.  Since my project was based on movies, I gave it the name of  top_movies.  The code I would write to interact with the interface would be located in the lib/top_movies/cli.rb, and would be called in the executable file bin/top_movies.   I created a scraper.rb and a movie.rb class, and used the bin/ command to test out my intended code, looking particularly for expected behavior.

My movie.rb class would house all the code about my movie object that I wanted to share with the user.  The categories that will be scraped are listed as attributes of the movie class.

I began by writing the code for a user interface that would mirror the behavior of my app.  I wanted the user to be greeted with a welcome message, and then asked to choose a number from the list of movies that populate.  A nice thing about this process is that you are free to play around with your code as much as you would like.  Functionality and flow are totally up to you, and it was that freedom that made it even more exciting to write.  The data I provided, would go one level deep, giving the user an option to view more information on a movie if they chose to do so.  

The scraper.rb class would gather the data from the website of my choice, and use that data to output information back to the user.  Once I successfully scraped the data I needed from the website, it was time to implement that data into my code.  Boy was that fun! Creating variable names, which you wouldn’t think is difficult, actually can be at times.  I scraped data from a list of 100 Top Hollywood Rated Movies, and these movies were accompanied by their year of release, genre, cast, director, a brief synopsis, and the critic review from Timeout.com.  With all of this information, this website proved to be a good fit for what I needed.  In order to scrape the website, I used an HTML Parser called Nokogiri, and Open-URI, a Ruby easy-to-use wrapper for net/http, net/https and net/ftp, and is considered the most popular way to read URL content, as well as make a request to get information or download a file from a particular site.  Nokogiri is a gem library that serves virtually all of the HTML scraping requirements.  To install Nokogiri, one must simply enter gem install nokogiri  in their terminal, and let the rest happen.  This process can take a few minutes, and may or may not be seamless, so patience is key.  It makes sense to install nokogiri, as it is a tool that all developers will likely use the remainder of their career.  If you do find yourself running into issues installing Nokogiri, follow the  official Nokogiri installation guide here.  This guide will walk you through the installation from start to finish.

With Nokogiri installed, I now have the means to search documents using CSS selectors.  A CSS selector is the section of a CSS rule set that literally selects the content you want, which allowed me to drill down on the specific HTML elements containing the data or information that I desired to portray to the user.  With all of this information, I was able to create a scraper method inside of the scraper class, that scraped the website, iterated over each instance of a new movie that was created, then add the desired information to the new instance, and return the results. 

Once that was complete, I returned to focus on my CLI class, which is where the scraper.rb and movie.rb classes are combined to produce movie objects, that would mimic individual movies filled with information about that movie.  Here is where the  scraper.rb  and movie.rb  classes transfer data from the scraper class to the movie class, giving them the ability to work together, while simultaneously being independent.

I included some methods that enabled easy navigation from option to option, by implementing some if else statements in my CLI class.  Voila! I know have a fully functioning Ruby command-line-application! 

Before I could officially claim victory, I had to make sure everything was working correctly.  I took care to package, install, and test my gem and made sure to include instructions in the Readme.md on how to package and install the application locally.  You can view my code here.

Building this application was truly a test of the skills and knowledge that I have acquired up to this point as a student at Flatiron School. In the midst of the fear, the long hours, late nights, and arm and back spasms from spending 10-12 hours straight at the computer, I had accomplished a major feat, and it was all worth it!  I am genuinely proud of what I achieved and am looking forward to building more applications in different languages in the future.

Thank you for reading my blog.  I hope you enjoyed reading it and learned something as well!


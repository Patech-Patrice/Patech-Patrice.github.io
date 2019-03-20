---
layout: post
title:      "Sinatra Application from Scratch"
date:       2019-03-20 17:40:42 +0000
permalink:  sinatra_application_from_scratch
---



For my Flatiron School Sinatra Portfolio project, I created a shoe inventory application.  As an avid collector of all types of shoes, I  wanted to be able to keep them well organized and easily accessible at any time. Throughout the years, shoes have taken on attitudes of their own, becoming an extension of a person’s personality.  Just like with coding, shoes give you the ability to be creative.  With code, you are the creator, and as a creator, you have the freedom to make your canvas look any way you choose. 

**What is Sinatra?**

Sinatra is a domain specific language, written by Blake Mizerany,  implemented in Ruby, and is used for writing dynamic web applications.  The language is Rack-based, meaning it can fit into any Rack-based application stack, including Rails.  In lamens terms, Sinatra is simply a bunch of pre-written methods that developers can include in applications to turn them into Ruby web apps.

The requirements for this project were:

Build an MVC(models, views, controller)  in Sinatra 
Use multiple models with at least one has_many and belongs_to relationship
Have user accounts- users must have the ability to sign up, sign in, and sign out
Validate user login and input 
Once logged in, a user must be able to CRUD(create, read, update and destroy) their own resources and not those of another user

**Building an MVC**

Before beginning to code, I needed to have a clear idea of what I was going to build to determine what my project would look like, as well as how many models, views, and controllers (MVC) I would need in order for the user to be able to interact with the application.  MVC is a framework for web applications that provide a separate group of files that have specific jobs and interact with each other in clearly defined ways.  I decided to create a user and shoe_entry model, which is where the logic of the app lives and data is manipulated and saved.  These models would both inherit from Active Record and Sinatra Base. Our user model has a has_many relationship with the shoe_entry model, while the shoe_entry model has a belongs_to relationship with the user model.  The views directory is considered the “front-end”, user-facing portion of a web app.  Here, is where the HTML, CSS, and Javascript code live and is the only part of the app the user interacts with directly.  The controller's directory communicates data from the browser to the app, as well as from the app to the browser, and is the go-between for models and views.  The app directory is the heart and soul of the Sinatra app, holds our MVC directories, handles all incoming requests to the application, then sends back the appropriate data responses made by the user.  


```
├── Gemfile
├── README.md
├── app
│   ├── controllers
│   │   └── application_controller.rb
│   ├── models
│   │   └── model.rb
│   └── views
│       └── index.erb
├── config
│   └── environment.rb
├── config.ru
├── public
│   └── stylesheets
└── spec
    ├── controllers
    ├── features
    ├── models
    └── spec_helper.rb
		
```

**Creating an Environment**

Creating an environment for any application is very important.  Here is where the environment database will connect to whatever it is that you specify.  The config directory holds an environment.rb file that connects all of the files in the application to each other and it’s corresponding gems.  A config.ru file is also required when building Rack-based apps.  After all of the code is loaded, the config.ru file stipulates which controllers to load as part of the app using run or use.   
 

```
require_relative './config/environment'
if ActiveRecord::Migrator.needs_migration?
raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
end
use Rack::MethodOverride
use UsersController
use ShoeEntriesController
run ApplicationController

```

**User Input and Validations**

```
configure do
    set :public_folder, 'public'
    set :views, 'app/views'
    enable :sessions
    set :session_secret, "password_security" 
    register Sinatra::Flash
  end
```

In order to give users the ability to sign up, sign in, and sign out, a session must first be created, validated, and then securely processed.  A session stores data on the server then passes that data to the client as a cookie, in order for the data to later be accessible.  Sessions are enabled within the application controller, along with a line of code that validates and encrypts a user’s password:  set:session_secret, “secret”.  This encryption key, which is provided by the gem bcrypt,  is used to create a session_id unique to every user’s session, and stores the data in the browsers’ cookie.  In order to ensure that the user’s input is valid, parameters are put in place, and error messages are given when an input is invalid. Once a session is created, a user has the ability to create a new entry, read(or preview) all entries created,  or update and delete any entry in their collection.  

**Conclusion**

Sinatra is a great framework to use for any developer at any programming level.  The code is clear, concise, and easy to understand. The use of such gems as Active Record, Sinatra Base, and brcypt, with its built-in methods, make implementing functionality quick and simple.  If you would like to check out my code, you can do so [here](https://github.com/Patech-Patrice/True_Shoe_Lovers_Haven.git).














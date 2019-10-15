---
layout: post
title:      "Using Ruby on Rails to build a CRUD Application"
date:       2019-08-20 11:56:02 -0400
permalink:  using_ruby_on_rails_to_build_a_rails_application
---


After completing my Sinatra application from scratch, my next project was to build a complete Ruby on Rails application.  The app must be able to manage data that is related to one another through complex nested forms and RESTful routes.  The requirements for the project where to use the Ruby on Rails framework, include associations and reasonable validations in models, have at least one chainable ActiveRecord scope method and a third-party login authentication system. I will briefly discuss some of these fundamentals I learned while building my Rails portfolio project.

# Rails Framework 
Rails is an open source, full-stack web framework, written in Ruby,  that was designed to make programming more productive and efficient.  It allows you to spend less time configuring an application, giving you more time to write good, DRY( Don’t Repeat Yourself) code, as well as it creates a directory structure for your application that includes every file you will need to accept user requests, query databases, and respond with data rendered in templates.  In order to get started with creating a Rails app, you must first make sure rails is installed in your editor.  In your terminal enter the below command to be sure that rails is installed:

$ rails --version

If it is not installed, enter the following command in your terminal to install rails:

$ gem install rails

Once rails is installed, you are then able to create a new project using the $ rails new  command. This prompt creates all of the necessary files needed for your application.

 To view your app, you must open a server.  This is done by typing $ rails s or $ rails server  in your terminal.  Once started, go to the address http://localhost:3000, and your application will be rendered to you in your browser.


# Rails Principles and Architecture
Rails is based on two important philosophies; convention over configuration and Don’t Repeat Yourself (DRY).  Convention over configuration is simply Rails’ way of deciding what conventions will work best for you when you create your app, including which web server and database server to run in development mode.  The DRY principle means to avoid duplicating knowledge and code within your app, ultimately leading to less errors. 

Like Ruby apps, Rails apps are structured using models, views, and controllers (MVC), which is designed to separate an app’s data from user interaction, known as separation of concerns.  The model holds all of the apps data or state, and rules or logic for manipulating that state.  The models also contain code for validations and associations between models.  The view is the user interface of the app which consists mainly of HTML since it is a web application, and it uses Embedded Ruby (ERB), a template system by default.  ERB allows the inclusion of Ruby code to access data within an HTML template.  The controller is the glue that holds the model and the view together.  It accepts requests from the user, gathers necessary data from the model, and then renders the correct view. All of these components work together in order to create an app that is easy to understand and maintain.


# Associations and Validations
ActiveRecord associations are used to describe relationships between models, and are important because they make  frequent operations more straight-forward, and are implemented using macro-style calls.  When an association is created in a model, Rails automatically defines several  methods for that model. There are six types of Rails associations:


* belongs_to
* has_one
* has_many
* has_many :through
* has_one :through
* has_and_belongs_to_many


These complex associations allow our applications to mimic real-world behavior, enabling more robust apps that can handle large amounts of data and logic. Below is an example of an association inside of a review model in my Rails project:

```
class Review < ApplicationRecord
	belongs_to :user
	belongs_to :designer , optional: true
end 

```

Validations are sets of rules that you create to protect your data from invalid input and information, making sure that only good data persists to the database, and they are implemented as class methods:

```
class Review < ApplicationRecord
	validates :title, presence: true
	validates :stars, numericality: {only_integer: true, greater_than_or_equal_to: 0, less_than: 6}
	validates :designer, uniqueness: { scope: :user, message: "has already been reviewed by you" }
end

```

This validates the presence of a title, stars, and designer.  The :presence validator ensures that there is text inside of the title field, while the :uniqueness validator ensures that a user cannot review the same designer more than once, and provides an error message when a user makes an attempt to duplicate.  

# Conclusion
Rails is a great framework for any developer at any programming level who would like the ability to quickly start an application with everything you will need in the beginning.   Equipped with a large community of developers who are constantly working to make the features better, Rails has plenty of support if you run into issues in development.  If you would like to view my Rails portfolio project, you can do so [here](https://github.com/Patech-Patrice/luxcloset).




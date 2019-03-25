---
layout: post
title:      "A Brief Synopsis of Ruby Sinatra Methods"
date:       2019-03-25 22:07:36 +0000
permalink:  a_brief_synopsis_of_ruby_sinatra_methods
---


After completing my Sinatra project, I decided to dive a little deeper into some of the methods, operators, and relationships I used in order to build my shoe collection application. Below, I will briefly discuss a few of these in hopes that it may help someone else on their journey to Ruby Sinatra greatness.

**The Bang Operator**

The logical negation operator (!), commonly referred to as the bang operator, reverses the meaning of its operand. The operand must either be a number or an expression that evaluates to be either true or false. The operand is then converted to a boolean value(true or false). The result is true if the converted operand is false, and false if the converted operand is true. Simply put, (!) will convert the argument to a boolean and return the opposite of the boolean value of the operand(e.g. true if it's nil or false, and false otherwise.) When two (!!) are placed together, the second operator negates the first, providing you with a boolean value of the argument(e.g. false for nil or false, true for pretty much everything else). In the examples below, you can see how these operators are used and what the expression evaluates to:
* 
* !!current_user: this helper method returns true or false if a user is logged in or out. 
* 
* !!logged_in?: this helper method returns true or false based on a session created by a user.  In Ruby, the convention is to attach a (?) or (!) when the value you are returning is a boolean.
* 
* Current_user != @shoe_entry.user: this line of code states that the current user is not equal to the user of that instance of a shoe entry.  This line would be used in order to protect a user’s entries and make them uneditable by others.
* 
* 

** Authenticating Users by Securing Passwords**

Making sure that a user’s data is secure is one of the most important jobs of being a developer. Although people are warned against using the same password across many platforms, some will still do so. For this reason, we developers use an open-source gem called bcrypt.  Bcrypt allows us to run a user’s password through a hashing algorithm that manipulates data so that it can not be un-manipulated. ActiveRecord, a Ruby gem, gives us access to a macro method has_secure_password, that works with bcrypt to give us the ability to secure passwords in the database, and is applied in our user model.

```
class User < ActiveRecord::Base
  has_secure_password
end
```

The line @user.authenticate(params[:password]) authenticates or verifies the user password making sure that it is the correct password that is securely saved to the database.  We call the authenticate method on a new instance of a user, and pass in the param argument [:password], to ensure the user’s password is correct. The authenticate method validates the password and matches it to the database. If the versions match each other, the authenticate method will return the instance of that user.  It is important to note, that once the password is encrypted, the only one with access to it, is the user who created it.

**Associations**

 The purpose of setting up has_many and belongs_to relationships, or associations, are so that apps can mimic real-world behavior.  In my Sinatra app, I created two models, user.rb and shoe_entry.rb. The users model has a has_many relationship with shoes, and the shoe model, a belongs_to relationship with users.  ActiveRecord provides the macros belongs_to and has_many , and below you can find an example of what an association looks like in Ruby:
 
```
class Cat
 belongs_to :owner
end


class Owner
 has_many :cats
end

```

 In order to showcase these associations,  I had to create a database table using ActiveRecord.  This table was created by running rake db:create_migration NAME="create_users" and rake db:create_migration NAME="create_shoe_entries".  This created an empty migration table in the db/migrate/ folder, and I added the attributes that I wanted my table to have.  With these tables and attributes, I was able to identify my primary key values, which uniquely identify each record in the table. Once I created my tables, I needed to tell them how to relate to one another.  This is where the foreign key comes in.  A foreign key points to a primary key in another table.  In ActiveRecord, the tablename_id convention is used.  With foreign keys, they always sit on the table of the objects that they belong to.  

```
class AddColumnToCats < ActiveRecord::Base
 def change
   add_column :cats, :owner_id, :integer
 end
end

```

In the example above, cats belong to an owner, so the owner_id becomes a column in the cat's table.  We now have the ability to create a new instance of our object, and save that instance to our database.

These are just some of the terminology and methods used by Sinatra and Ruby to build functional, beautifully well-executed applications. I hope you have enjoyed learning a little bit more, and that you will be inspired to seek out your own resources to expand your knowledge.







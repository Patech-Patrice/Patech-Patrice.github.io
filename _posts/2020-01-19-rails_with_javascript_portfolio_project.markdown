---
layout: post
title:      "Rails with Javascript Portfolio Project"
date:       2020-01-20 00:58:52 +0000
permalink:  rails_with_javascript_portfolio_project
---


The Javascript portfolio project proved to be the most challenging project to date at Flatiron School.  I wanted to build something that I would be able to expand on down the line, and decided on a winery management system that keeps track of all the wineries I have visited or plan to visit in the near future.  The requirements for this project seemed simple, however, implementing the fundamentals proved otherwise.  The tasks were to:

* Build an application with a  HTML, CSS, and JavaScript frontend and a Rails API backend
* All interactions must be asynchronous and use JSON as the communication format
* The javascript application must use Object Oriented JavaScript or classes to encapsulate related data and behavior
* The backend must include a resource with at least one has-many relationship
* The backend and frontend must collaborate, and your app should have at least 3 AJAX calls
* Must use Fetch with the appropriate HTTP verb on the frontend, and the backend should use RESTful conventions

#  The Backend:

First I needed to generate a new project, making sure to include the   --api  flag so rails knows to set up the project as an API.

```
rails new <my_app_name> --database=postgresql --api
```

I also needed to include the database I was using inside the creation of my project, which is Postgres.  I needed to ensure that I used RESTful conventions.  A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. Inside of my controllers lives the code that renders the wineries in the form of JSON data. 

```
class Api::V1::WineriesController < ApplicationController
    before_action :find_winery, only: [:show, :edit, :update, :destroy]

    def index
        @wineries = Winery.all 
        render json: @wineries 
    end 

    def show
        @winery = Winery.find(params[:id])
        render json: @winery.to_json(include: [:wines]), status: :ok
    end 

    def create
        @winery = Winery.create(winery_params)
        render json: @winery, status: 200
    end


    def destroy
        winery = Winery.find_by(id: params[:id])
        winery.destroy
        render json: winery
    end

    private

    def winery_params
        params.permit(:name, :year_founded, :types_offered, :location, :affordable)
    end

    def find_winery
        @winery = Winery.find(params[:id])
    end
end
```


Parameters must be created for the winery because those same parameters must be included in the POST and PATCH requests of the fetch method.  I will provide more details about the Fetch API when I talk about the front-end.  For the representation of the has-many relationship, a winery has many wines they carry at their vineyards.  Since PostgresSQL was the database of choice, I had to make sure to create the database before migration by running rails db:create & then rails db:migrate.  I am now able to run the rails server in my text editor terminal, and access my application which is hosted at localhost:3000.  Since this is an API, my url looks like this ` http://localhost:3000/api/v1/wineries`.

#  The Frontend

My single page app had to include the use of javascript classes, or object oriented javascript in order to encapsulate data and behavior. Object-Oriented JavaScript is prototype-based so it does not utilize or support class statements. Instead, functions are used to represent a class as well as new objects are derived by using a prototyping technique and by calling the object’s native constructor.  

```
class Winery {
    constructor(data) {
        this.id = data.id
        this.name = data.name 
        this.year_founded = data.year_founded
        this.types_offered = data.types_offered
        this.location = data.location 
        this.affordable = data.affordable
        this.wines = data.wines
    }
```

With my objects created and my parameters specified, I am to now implement the fetch method in my single page app.  The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. It also yields a global fetch() method that lends a simple, logical way to fetch resources asynchronously across networks.  I implemented a getWineries function that would fetch the wineries and the data associated with them, and render the contents to the DOM without redirecting to another page.  This method fires off an AJAX request to the index route in api/v1/wineries.


```
function getWineries() {
    
    fetch("http://localhost:3000/api/v1/wineries")
    .then(resp => resp.json())
    .then(data => {
    renderWinery(data)
    addWineriesClickListeners()
    getWines()
   })
}
```


# Conclusion

My app also makes AJAX calls using fetch to create a new instance of the Winery object, as well as to delete an entry, which satifies the requirements of the 3 AJAX calls.  Overall, this project required a lot of effort to complete.  Everything that we have learned so far at Flatiron School is starting to come together, and it makes the challenges that much more rewarding.  I look forward to building my final portfolio project and graduating from the program.




 

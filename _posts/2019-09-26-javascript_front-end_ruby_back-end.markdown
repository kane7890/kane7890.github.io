---
layout: post
title:      "JavaScript front-end + Ruby back-end"
date:       2019-09-26 17:49:05 +0000
permalink:  javascript_front-end_ruby_back-end
---


This latest portfolio project has proven to be a big challenge in terms of learning and using JavaScript to build  -- and display a web page on the user interface, while at the same time using Ruby to communicate with a database.   This marks a further evolution in building an application.  

1. Component 1: JavaScript "front end"

A few weeks ago, we started learning JavaScript, a language that I had heard about and that vaguely looked like C or Java (which, despite the name, is NOT JavaScript).  One new feature of JavaScript was that it permitted the developer to more intelligently control what was appearing on screen in HTML.  The developer could write JavaScript(JS) code that created <div>'s, <form>'s, buttons, <p>'s, etc. on the fly, rather than having to hard code the HTML display code in either HTML or ERB.   Text or HTML inside these tags could also be added JS also allowed for developers to capture/read what was on the forms.   At the same time, having this flexibilty also meant that the developer had to be careful to see what was actually displayed, because the JS code might not be so self-evident as to what was being displayed.  Using the debugger and the browser console were very useful in trying to figure this out...as was Node.js on the command-line interface for first learning JS.

Another big feature of JavaScript was event handling.  JS functions could be written that would essentially listen for events like a mouse click on a given button (e.g. a Submit button).  So the developer could use a function called addEventListener to, say,. listen for a click on the Submit button of a form, and read/capture the data that was in the form, and then send that data to be displayed, persisted to a database, or further transmitted to other parts of the application.

2.  Component 2: JSON (JavaScript Object Notation) and Fetch

Well, how do we transmit this data to other parts of application.  The main way to transmit/communicate data with other parts of the application is to use JavaScript Object Notation (JSON) and a function called fetch().   One would fetch() from another URL (often a server) and take the result and further process or perform additional instructions with the result.  Fetch() is a little trickier, though, because it returns an object -- but not exactly-- in an asynchronous manner to reflect how requests to a server may have a delay.   For example, to fetch a list authors using a GET request from a server:

fetch("http://localhost:3000/authors")
.then (resp=>resp.json())  //promise returned, then puts the result of that response in JSON format
.then (resp =>this.renderAuthors(resp)) // calls this.renderAuthors on the now JSON-formatted response.

Technically fetch returns a *promise*  -- which means that *eventually* an object will be returned, but you cannot just take the result of a fetch and necessarily return it.  One difficulty is that the code part of the "arrow function" after the arrow (e.g. this.renderAuthors(resp) in this case) runs in its own scope, so one can't just use the "arrow function" to make changes to variables in the function calling that fetch() or simply pass the result of the arrow function back.  One needs to use the result of the response completely in the function to the right of the arrow.   In this case, the response is an array of authors, and the this.renderAuthors is used to render the Authors in HTML (in my app, they were used to create a <select> list).

The fetch request can also be used to POST an object to a server...in this case it is usually necessary to call fetch() with an additional argument, which is an object that (a) specifies the fetch is a POST method request; (b) gives the format the section with "Content-Type"... and  (c) the data to be passed to the server (in the "body" section):

var fetchObject = {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Accept": "application/son"
    },
    body: JSON.stringify ({
      trainer_id: trainerId
    })

  }

  fetch(POKEMONS_URL, fetchObject)
    .then (resp => resp.json())
    .then (resp => renderPokemon(trainerUl, resp))
		
	The fetchObject tells fetch() to send a POST request to POKEMONS_URL with the variable trainer_id set to variable trainerId in JSON format.  fetch(POKEMONS_URL, fetchObject) will return the promise to response, convert it into a JSON response with the first .then function, followed by taking the result of the first .then and rendering the object that was returned by the Fetch.
	
3.  The third major component of this app is the Rails "backend."  

The final component in this app is a Rails backend server was generated as an API.  This is still pretty much the same Ruby/Rails interface to the database files using ActiveRecord.   There are RESTful routes to get data to and from the server much as in the prior project app, only this time these interface and communicate with the front two components via the JSON format.   Instead of using an ERB view to render/display the data resulting from a Show or an Index route after running the respective methods, the developer tells the method to render the results using JSON format (which ends up being plain text delineated by commas and often braces).   

  def index
    authors = Author.all
    render json: authors
  end
	
	The authors instances (which would be an array) are then rendered in JSON format that our JS front end can read.   It also works in the other direction in POSTing data to a server on the Rails server for persisting data to the database.   Rather than reading data from an ERB/HTML generated form view, the Rails server reads data that is passed to it by the JS front end.
	
  def create
    post = Post.new(author_id: params[:author_id], title: params[:title], body: params[:body])

    post.save
    render json:post, include: [:author]
  end
	
	All one needs to do , then, is to build the Rails server as a back-end as an "API" (I suppose there is nothing preventing someone from building one version using full Rails /ERB and another version using a JS front end, though each version might prove to be more optimal at certain tasks), and then buiild a front end using JavaScript.




---
layout: post
title:      "Rails, RESTful Routing and Keeping Stuff Straight"
date:       2019-08-23 17:24:19 +0000
permalink:  rails_restful_routing_and_keeping_stuff_straight
---


While building this Rails Portfolio Project, I found it challenging to keep straight the different routes, controllers and views, although i found the Rails framework to be fairly useful.  In Rails, the application developer can simply tell the server to create routes, which are similar to map instructions telling where the server to go when navigating a web page.  These routes are implemented as "actions" and each action is further specified using a Ruby method in a Ruby controller files.  More complex servers could have multiple controllers. So when a user navigates to a Rails server, the server could be enabled to perform the following actions with an underlying database or databases (via ActiveRecord); these are called RESTful actions.  (REST stands for Representation State Transfar and is a somewhat standard architecture for structuring how the user moves between web pages and underlying logic when a user clicks on pages and links in a web-based app).  The RESTful routes and actions are as follows:

*  Creating a new instance (ActiveRecord effectively uses an instance to interact with a row of a database) through a web interface, editing that instance/row,  (New and Create actions)
*  Editing that instance/row (Edit and Update actions)
*  displaying that instance/row (Show action)
*  displaying all instance/rows (Index action)
*  destroying/deleting that row (Destroy action)

in Rails, by default, every action will have a "view".  The combination of views is essentially the web pages that the user of the application sees and interacts with, usually with a web browser.  Rails provides a fairly simple way to implement these views using embedded Ruby (.erb) code or a combination of HTML and embedded Ruby code.   Not all actions will need a corresponding view...typically one does not use a create view AFTER going to the create action of a controller, though it can be done and may be useful in some applications.

It may be helpful to note that there are some of the actions are "paired"--.e.g New and Create, Edit and Update.  (These pairings also help one remember the names of the different RESTful actions, along with show and index--show is singular and index is "plural")  That is because the controllers provide Ruby methods (and the programming logic) but do not interact in a user interface with the user, while the views do.  So when  a user selects "signup" (create new user), the application will first go to the New controller action to prepare a new user instance/row in the database, then go to a new view (new.html.erb -- embedded Ruby) to get the information from the user, then return to the Create action in the controller to actually create and persist the new instance (which saves the user data into the database as a new row)

The flow diagram between the new action, the new view and the create action is as follows:

*New Action (controller logic in Ruby) -->New view (new.html.erb) --> Create Action (controller logic in Ruby)*

The user is often redirected or routed to a home page or a Show view page(see below) after the Create Action instructions/code has been executed. 

Editing a instance/row has a similar flow as the flow for creating a new instance/row .  There is an Edit action, which usuallyfinds and prepares the instance/row  to be edited in a edit.html.erb view, a edit view (edit.html.erb) view for receiving editing changes from the user, and an Update action for saving and persisting the changed instance/record into the database.  

*Edit Action (controller logic in Ruby) --> Edit view (edit.html.erb) --> Update Action (controller logic in Ruby)*

The user is also often redirected or routed to a Show view page (see below) after Update Action code has been run.

Two other routes (and their correspomnding controller actions) are more for displaying data to the user.  The Show action routes to a Show view (show.html.erb) for displaying the data for a single row in the database (again through the use of ActiveRecord to create an instance).  The Index action routes to a Index view (index.view.erb) for displaying a set of records -- and often, all of the records -- in a given database.  

*Show Action (controller logic in Ruby) --> Show view (show.html.erb):  this displays a single record from the database, usually found by using the primary key :id for that database.*

*Index Action (controller logic in Ruby)-->  Index view (index.html.erb)*

(To help create flow between pages, I put a link to Home in all of my views via an application layout view)

The final action is to *Destroy*, which would delete a given record.   

Rails provides "shortcut notations" for routing to these different actions.  One can find out which routes in the folder that the rails app is in by typing "rails routes".  (An easier way 

These actions can be used not just for entering, editing and displaying records in a database but for implementing a system for logins and logouts.  A user login could be implemented by checking for login information -- using the New and Create Action-- to creat a new session.  The logout would be implemented by the Destroy action and clearing the session.  I used a Session controller to implement logins and logouts in such a way.

In summary, Rails routing allows the developer to implement a web app with editing, reading, creating, updating and deleting from a database, as well as other routing in a fairly simple straightforward manner.







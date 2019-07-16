---
layout: post
title:      "Building and Debugging a Sinatra App "
date:       2019-07-16 06:05:38 +0000
permalink:  building_and_debugging_a_sinatra_app
---


Building and debugging this web-based Sinatra app and ActiveRecord to store and persist data was kind of an challenging but interesting process, but it was a process made much easier by using Tux and also some other features to look into the data being stored.  

I built an app for tracking basketball players on different teams, where each team was basically represented by a user.  This was designed as a fairly straightforward pair of data tables:  each user (team) had many players but each player belonged to only one team.   Each table was implemented using ActiveRecord, an ORM (object-relation-mapping) system that turns each SQLite table into a Ruby Class and turning each row of the database into a Ruby object. ActiveRecord thus provided developers with Ruby methods to access and interact with the underlying SQLite database.  The players table (Player model) would have the foreign key that linked each player row with the a row in the users table through a field called user_id. 

The developer had to specify that each model (Class) inherited from ActiveRecord::Base.  The underlying tables would be created and possibly modified using a Rake migration, which also included writing Ruby code for creating tables.  The underlying tables could also be seeded using Rake, so one could basically write all the test data in one file for loading once.

Using ActiveRecord, building the relations between the two models and thus the corresponding tables in SQL was done fairly simply--one just had to specify the model/class whose elements belonged to the other model/class and which one had many.  In my case, I had to specify in my User model that each user had many players  (has_many :players) and that each player belonged to (belongs_to :users).   

Sinatra also allowed for implementing some good design principles in building this web app.  Each model had a corresponding set of Views files -- which provided the code for implementing the web interface with ERB -- Embedded Ruby, which was a combination of HTML and Ruby, and each model also had a corresponding Controller file, each of which had logic for multiple HTTP routes for routing the web page end-user to different views and using logic to interact with the databases through the Model classes.  There was also a general Application Controller, and in smaller, simpler apps, one could simply use one Application Controller file for all of the routing.   

This architecture for organizing different app functions/tasks into different files in a certain file structure is called Model-View-Controller or MVC.  Each data table/Model has its own Model, its own View and its own Controller.  In terms of how these three functions/tasks interacted, though, MCV might be more accurate -- the Model interacts with the Controller, which in turn provides the View to the user in this sequence:

Database <--> Model <--> Controller <--> View <--> User on the Web

We used Shotgun to serve the Views to the users.  To make monitoring and debugging simpler, I would open a second Terminal window of a different background color to run Shotgun so that I could see the error (and other verbose) messages while being able to execute shell commands in the other Terminal window.  

Actually writing and debugging the code for implementing this MVC architecture was a little more challenging.  One challenge was because databases are for long term and persisting data, correcting errors could be a challenge.  For example, if a table was incorrectly created missing a column, one would have to write a migration to add a column to that table.   We were using Bcrypt for storing passwords as a hash in the database.  I did not write code for users to change their passwords, so if I had forgotten a test password, there was no way in the app to change that test password and I wouldn't be able to login as the user.  

Using Tux in addition to the usual Pry definitely helped the debugging process.  I used Tux to view all the objects in each Class (i.e. all the rows in each table, either users or players).   More importantly, in Tux I was able to experiment with Ruby methods for setting and changing parameters and saving objects.  I was also able to add a new user to the users table on the fly, instead of needing to having to create a data migration.   I was able to change user passwords as wellm and reassign players to different users.  Of course, I had to be careful modifying the database independently of the app.  Sometimes the app would think a user with id=8 was still logged in, but I could delete that user from the users table in Tux and the app--which tracked the logged-in user using sessions--might still think that user was not only still in the table, but logged in.  That could and did result in some odd errors.

In the end, using Sinatra and Ruby app was a good learning experience. 






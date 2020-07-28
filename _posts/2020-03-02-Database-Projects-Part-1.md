---
layout: post
author: Tom Fynes
title: Database Projects Part 1
date: 2020-03-02T09:00:00.000Z
thumbnail: /assets/img/posts/DatabaseProjects/DBProj.png
category: Database Projects
summary: Database projects for beginners
---

We have all been there, someone has designed a databases which is used in production - this database is always changing but how is it stored in a single SQL file or a few SQL files with thousands of lines of code...Insert disappointed meme here.


The problem with this is when you need to make a change you have to scroll through the file and find the line/lines you need to edit.  You hope that it is not some dynamic SQL wrapped in multiple apostrophes, make the edit and hope this does mess anything else up. Well there is an easier way and that is to use SSDT database projects.


For this example I will use the adventure works database which you can download from [here](https://docs.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver15&tabs=ssms),


You will also need visual studio installed along with SSDT (SQL Server Data tools)

To create a new database project open visual studio, new project and select database project.

![alt text](/assets/img/posts/DatabaseProjects/DBProj.png "Create New Project")

Give this an appropriate name and select create. This will then take you to an empty solution where we can import our database schema. Now when we look at importing the database schema it is worth noting there are three ways to do this.


1. Dacpac - Use a Dacpac file to import the schema.
2. Databases - Connect to a database and take a copy of the database schema.
3. SQL files - Select the SQL files you would like to build the database schema from.


Although all three are ways to import a database schema if you use option 3 there is a change some objects could be missed if they are created using dynamic SQL, on this occasion we will use option 2 and connect to a database.


To do this right, click on the project file, import and then database:

![alt text](/assets/img/posts/DatabaseProjects/Import.png "Import Database")


You will then be presented with a window to input your connection details (Start connection):

![alt text](/assets/img/posts/DatabaseProjects/Connect.png "Connect Database")

Once this has been done you can  proceed with the import:

![alt text](/assets/img/posts/DatabaseProjects/IMportas.png "Import as")

For this example I am un-ticking the options for importing referenced login and import application-scoped objects only but when this is done press start. It should only take a few seconds to import adventure works however the larger the database the longer this process can take. When this has finished press the finish button. 


Now on the right hand side in the solution explorer you will see the new schema:

![alt text](/assets/img/posts/DatabaseProjects/Structure.png "Structure")

As you can see in the above image everything is now organised neatly under the schema they belong to, making changes easier to manage. 


In the next part I will cover adding your database project to GitHub.


Thanks for reading.


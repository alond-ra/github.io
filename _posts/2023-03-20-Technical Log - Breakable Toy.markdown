---
layout: post
title:  "Technical Log for Breakable Toy: To Do App"
date:   2023-03-20 15:00:56 -0600
author: "Alondra Galvan"
tags:
categories: technical-log
---

**Overview:**


The client has requested a task management application that allows for the creation, modification, filtering, sorting and pagination of tasks. The app should include a user interface for adding tasks with metadata such as name, priority, and due date. the user should also be able to edit existing tasks. The app should have filtering and sorting features that enable users to find and organize tasks easily. Specifically, the filters should allow users to search by name, priority, and due date, and the sorting feature should sort by due date and priority.

Additionally, the system should provide a checkbox to enable the user to mark tasks as done or not done, and the list of tasks should be paginated for easier navigation. Additionally, the application should include performance analysis features that calculate and display the average time between task creation and completion in general and grouped by priority. By providing these features, the application can help the client organize and complete their tasks more effectively, leading to increased productivity.

The app design should adhere to a specific markup that includes the following features:

<ol>
  <li>Search/Filtering Controls</li>
  <li>New To Do Button. This should open a modal to type the “to do” data.</li>
  <li>Priority column should show in the header the classic up and down arrows to allow the user to sort.</li>
  <li>The due date column should show in the header the classic up and down arrows to allow the user to sort.</li>
  <li>Action column to show actions (links/buttons) to allow the user to delete or edit a “to do”. </li>
  <li>To Edit is ok to show a modal similar to the one to create a “to do”.</li>
  <li>Pagination control. Showing the pages, their number and the next and previous page is enough.</li>
  <li>Area to show the metrics.</li>
</ol>

![Markup to design the app](/assets/post_imgs/tododesign.jpg)



**Context:**



**Solution**

As required, the front-end part was implemented with React and Javascript. However, this part is incomplete, I could not test it. I created part of the structure for the front end. Just like the table for the to-do's in CSS and the Javascript code for getting the information to it. The idea was to have all table-related classes and methods in front-end\src\ToDoTable\List.css and front-end\src\ToDoTable\List.js and the code for the actions (create a new to-do, update or delete elements) in the front-end\src\ToDoTable\newToDo.css and front-end\src\ToDoTable\newToDo.js.

In the meantime, I was running the front-end by npm start.

the backend part was implemented with Java, Maven and Spring Boot. In the back-end folder, specifically in \demo\src\main\java\com\todo\demo have the most relevant files.

The model folder contains the todo.java file, which contains the structure of the to-do's; it is a class with the required attributes (ID, name, due date, status, priority, creation date and end date). The duration attribute was added for the area of the metrics. 

The todoRep folder contains four "layers" for the structure that will contain the to-dos: a list; it also contains the classes for the methods to create new to-dos and update and delete elements. I made some tests with Postman and it seemed to be working correctly.

In the meantime, I was running the project with the Spring Boot Dashboard Run command.



** Alternative Solutions **

The four-layer for the back-end was really good in a didactic way. But the implementation is not the clearest, there is a straight way of implementing those methods.



---
layout: post
title:      "Using new skills to create something for an old job."
date:       2019-07-22 13:26:11 +0000
permalink:  using_new_skills_to_create_something_for_an_old_job
---


I have been a teacher for 8 years.  I teach a wide variety of classes and average about 12-15 class groups a school year.  One of the most challenging things with having that many classes is making sure that students have feedback on what their work.  I've gone through a lot of different systems to try and maximize the feedback that they are getting.  When it came time to do a project with database management, creating a tool to help me with this just made sense.

There are lots of quiz websites out there, but nearly all of them you have to pay for once you reach a certain number of students.  They can also be fairly difficult to use, especially if you aren't willing to shell out the extra money to get the "premium" features.  So I wanted to create something that allowed me to operate for free and give students immediate feedback without having to pay an arm and a leg.

The biggest portion of this came down to database management.  In a project like this there is a alot of information floating around and keeping everything straight is of the upmost importance.  There had to be two separate user accounts with different permissions.  Students couldn't be allowed to edit tests and teachers didn't need to be able to take tests.  I also needed to ensure that each teacher had their own unique set of questions and quizzes along with their own unique courses.  I had to come up with a way for teachers to assign a quiz to a course, but in doing so, also assign a quiz to each individual student.  In all I ended up with 10 separate tables and 13 models to separate and relate the data.

When creating routes and managing pages, I tried to keep as close to RESTful routes as I could.  Since everything was tied to the user I prefaced every route(except login pages) with "/(student or teacher)/(student or teacher slug)"
this enabled me to easily separate the two different kinds of users and by setting up helper methods that checked if a user was a teacher or a student it secured the two different sides from being accessed by the other.

The biggest challenge that I ran into was storing the student data after they took the quiz.  I initially started with just a table to assign a quiz to a course.  It didn't take me long to figure out that wasn't going to work as that gave no way for a student to take a unique quiz and get a grade back for it.  The way that I worked through this was by using the join tables as more than a simple join.  I created a student-quiz table and a student-question table to store data.  The student-quiz table acted as a join table between the student, course and individual quiz, but also stored the score that students got on the quiz.  The student-question table acted as a join table between the student-quiz and the questions on it, but it also stored the student response.  By doing this it allowed me to access both the quiz and question information, as well as the student input in order to give the feedback that I wanted them to have in the first place.

In the process of creating this page, I've learned a great deal about managing data, but also displaying unique information on pages based on who is logged in and what input they have given.

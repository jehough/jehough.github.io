---
layout: post
title:      "Roles in ASP.Net core"
date:       2020-03-28 00:24:20 +0000
permalink:  roles_in_asp_net_core
---


As I began looking for a new job in the coding world a very stark reality struck me.  There weren't many entry level jobs available for Ruby developers in my  area.  After talking to a couple of recruiters I discovered that .Net was the most prominent platform being used in my neck of the woods.  Since that was the case, I decided it was time to learn .Net.  So far the journey has been pretty fruitful.  I still have a ways to go with C# as a language, but I have enough to get me started in the framework and I have enjoyed the process of building new apps with it.

One of the biggest problems I ran across though was how to set up roles using ASP Identity.  Identity is a fantastic framework for setting up authentication and really makes getting user login very easy.  There are a couple of problems though.  First of all, the documentation is a little sparse on details in how to get it set up.  Second, when ASP.Net Core changed from 1.0 to 2.0 to 3.0 some pretty significant configuration changes happened.  That means that tutorials that worked for 1.0 and 2.0 would only get you part way with 3.0.

While I was setting up Identity for a gradebook app that I am putting together, I wanted to include roles of Student, Teacher and Administrator.  Roles are a part of Identity, but it was difficult to figure out exactly how to set it up.  I found some really helpful advice [here].  (https://gooroo.io/GoorooTHINK/Article/17333/Custom-user-roles-and-rolebased-authorization-in-ASPNET-core/28352#.XnyCu4hKjcc)

Roles seem like they are something that you have to set up as a configuration, and all of the questions that I was seeing seem to think the same way.  What I discovered though is that Roles are automatically set up as a table when you create the Identity.  All you have to do is create the roles just like you would any other data...by seeding it.  The link above goes through the process of seeding the data very well.

I followed this example closely except in one part.  In 3.0, it appears that the services that were in the program file are no longer there.  Since that is the case, I kept them in the startup file.

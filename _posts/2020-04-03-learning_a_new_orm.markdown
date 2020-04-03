---
layout: post
title:      "Learning a new ORM"
date:       2020-04-03 20:26:19 +0000
permalink:  learning_a_new_orm
---


In the process of learning the .Net Core framework, one of the most challenging things that I have run across is learning how the database is set up.  In Rails, the database ORM is set up through ActiveRecord and in .Net it is run through Entity Framework.  While both setups use a class as the foundation for a table, there are some pretty signficant differences in setup.

In ActiveRecord, in order to create the columns in the table you create migrations.  Any data that would be saved in the table will be put here and then the Model in a sense inherits those properties.  I suppose in some sense this could be considered what .Net Framework people call a DB first approach.  In other words, creating the database first and then the models follow.  While there are avenues in .Net framework to do this, when you move to .Net Core and EF Core, that ability then goes away.  

Instead you must use a code first approach.  This means that you must build the models with their properties first, then add them to a DBcontext class.  The DBContext class is what connects the models to the database and tells EF Core to make the necessary migrations.

The problem with this approach for someone coming from a Ruby background is that ActiveRecord really takes care of most of this for you.  Most of the time that can be convinient, but it does limit how much understanding you need to actually create complex database systems.  In EF Core you have to understand what the models will do to each other in order to build them correctly.  When you start adding multiple One-to-Many and Many-to-Many relationships, this can get complicated.  Having that understanding helps you to get predictable outcomes.

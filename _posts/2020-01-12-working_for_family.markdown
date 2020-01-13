---
layout: post
title:      "Working for Family"
date:       2020-01-13 00:53:20 +0000
permalink:  working_for_family
---


Recently I wrapped up my final project for the Learn Software Engineer Course.  It was easily the most fun project that I have completed through the course and I have to say that I have really learned a lot through the process.  I have enjoyed using bootstrap and several other packages that expand the use of react.

My father-in-law is considering opening an aquarium shop that will have an online store component.  After talking to him about it, I felt it would be a perfect thing for me to do as a final project.  Something he can use as he sets up his store and it gives me a way to be involved with it as well (I have my own aquarium and love keeping fish).

There are a lot of things that this web page would need.  First of all it would need the 'storefront' that would allow people to visit and browse through the different available products.  I wanted to give a couple of options for this, so I created a categories page and a search bar.  I had a difficult time working through the routes using react-router.  I attempted to use the nested routes by passing router props, etc to the different containers, but it had several issues that I could not figure out.  I was able to put all of the routes in the main folder and use the exact prefix with great results.

In the process of putting the search together, I had to decide whether to keep the search function on the front end with js, or use the backend with ruby.  I chose to keep the search on the frontend, using javascript to search through a list of all the items.  That may be something i choose to change in the future depending upon the volume of items that must be sent.

The other big piece of this project was to create a cart and checkout.  Using redux I created a store to keep track of the items that users want to buy.  I chose not to send that info to the server until the actual checkout when a user is actually signed in.


I do have one more piece that I want to add to this, an orders page.  It will require another controller on the backend and another few components on the front end that create the lists, but it won't be much different from the items or checkouts lists.

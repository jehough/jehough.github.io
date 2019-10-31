---
layout: post
title:      "Not Reinventing the wheel"
date:       2019-10-31 00:45:59 +0000
permalink:  not_reinventing_the_wheel
---


Sometimes when you think you are doing something that is more convenient you really aren't.  Sometimes I'll ignore google's driving advice and go a way I think is going to be quicker and end up taking more time.  Sometimes you will make a single page application thinking that it will cut down on loads, but the way you write it defeats the purpose.  Fortunately the second problem is much easier to fix.  Once you have gotten off the interstate, there's no turning back, but code...that we can refactor and adjust.

As I was building a single page budget application I had a realization.  I had written a series of functions in order to fetch the budget information and display it on the page after the initial log in.  When I got to writing the code for updating the budget with transactions, adding money to categories, etc.  I had initially just run the response back through the initial display function.  This is where the realization comes in.  It dawned on me that I was reloading everything on the page each time I made a change.  With the tiny amount of data that I was sending back and forth it was no big deal, but if I were sending a tremendous amount of data, that would be a problem.

So, I needed to change this.  In my initial creation of the display function, I thought I had done a pretty good job of dividing out functions so they had only one responsibility.  For the most part I was able to reuse most of the functions in an update budget function that drastically reduced what I needed to load on each update.  Because of the nature of what I was changing (a single number in a single line on a card) I had to refactor a couple of functions to split up some of the functionality.  The whole exercise was helpful in seeing just how important SRP is and how small your functions can go.

After reworking the page, I was able to adjust the data sent back and forth by the api as well.  In the end, I went from sending all the budget info on each call, and updating the entire page, to sending a single category and updating 2 nodes.  That is a drastic change in data exchange.

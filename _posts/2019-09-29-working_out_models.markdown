---
layout: post
title:      "Working out models"
date:       2019-09-30 00:49:02 +0000
permalink:  working_out_models
---


  This week I have been working on a Rails application that imitates an electronic medical record.  It was a fun project because it gave me a chance to work with my wife who is a nurse.  She explained what kind of things she thought were necessary for the program and I set about putting it together.
	
  The most challenging part of the project was getting the appointment form together.  Inside this single form I had to include 2 models that did not have a specific relationship to each other.  For each appointment there is a lot of information that has to be gathered by the doctor or nurse to be put into the form.  In addition to this, a doctor needs to adds medications for the patient as well.  In this app, I wanted the medications to specifically belong to the patient in order to get a full medication list.  

  This created an issue as there was no way to create a form directly relating the two objects without going through another model and table.  A new model didn't make sense as it would clutter up the database and create an extra instance to describe the same medication and prescription.  The better option turned out to be associating them through the patient model.
	
	I created a patient form and nested both the appointment and medications within it.  This connected the two models without creating excess data taking up space.  It also allowed me a feature that I believe most doctors would appreciate.  It allowed me to include a patients full medication list in the appointment form.  This way a doctor can see what  medications a patient has quickly and easily before prescribing anything else.

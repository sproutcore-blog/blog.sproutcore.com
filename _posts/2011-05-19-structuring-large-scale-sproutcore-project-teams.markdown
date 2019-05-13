---
author: pbergstr
comments: true
date: 2011-05-19 19:21:52+00:00
layout: post
link: http://blog.sproutcore.com/structuring-large-scale-sproutcore-project-teams/
slug: structuring-large-scale-sproutcore-project-teams
title: Structuring Large-Scale SproutCore Project Teams
wordpress_id: 1123
tags:
- IRL
---

Writing large desktop-like applications in SproutCore comes with a unique set of challenges that you wouldn't encounter writing a smaller application. A smaller project with one or two contributors is a lot more flexible and requires less planning; a large project with many contributors and moving parts is a completely different beast.

I've worked on many SproutCore applications, both large and small, since 2007 and I've seen where a project can get into trouble when it grows larger both in scope and in team size. The goal of this post is to share some of my personal experience developing a large SproutCore application.


## The Bliss of Smaller Projects


The benefits of smaller projects with one or two developers are relatively obvious. A small team makes it easy to stay on task for the limited scope of the project. Everyone knows what is going on because communication is easy and each developer has the opportunity to wear every hat in the project. Also, the developers working on the project know the code well throughout, mainly because two developers can transfer knowledge and be most effective if they are pair programming.



## The Challenge: a Large Application


If you are given the task of creating a larger SproutCore application, such as a calendaring client, one or two developers cannot possibly deliver the application in the required time frame. In some cases, more than 100,000 lines of code may be required, much more than a small group of developers can manage.

In this case, the team must grow to a size where you can meet your timelines while not adding so many people that the project slows down. Since there is so much to do, you need to split up responsibilities; instead of having developers wear all the hats in the project, developers wear one or two hats, and act as the person the rest of the team can trust to deliver their specialized part of the code or functionality.

This is true of working in any large team; the goal of this post is to highlight the particular roles that need to be filled when creating a SproutCore project in particular.
<!-- more -->
Imagine that your company, Initech, a typical software company, is tasked with creating a employee management application using SproutCore. The first aspect of the application, called TPS, is that a user can search for an employee and see employee's contact information and location in the org chart. A user can navigate around the org chart using various methods such as list, tree, and grid views.

The second aspect of the application is of the management of employees; a manager can edit employee information as well as add and remove employees from their organizations.



## What are the needed roles?


The roles that are needed vary from one SproutCore project to the next, and assigning them isn't an exact science by any means. Over the past several projects that I've been involved with, as an individual contributor as well as lead, I have found that certain roles have benefitted the development effort the most. Let's see how these roles map to the needs to the fictional TPS application by Initech.

How would Initech structure the team to create the SproutCore application? First, they would designate one of their most experienced SproutCore developers to be the technical lead/architect.



## Technical Lead/Architect


In a large project, is it especially important to have a person who is an expert in SproutCore development and can act as the technical lead or architect. This person can start on the TPS project first; they will create the basic structure of the application in the forms of state charts and main view components as the rest of the team continues work on other projects.

As the technical lead, this person would have to figure out what different roles are needed for the project and also communicate that need to the stakeholders such as management, QA, system administrators, and designers. This person will still write code in addition to his or her management tasks, but most often their role will be to triage issues that the team needs help with.



## The Data Modeler


 The second developer that needs to be brought on is the person who will own the implementation of the data models, data source, and interface with the server. For a large project, this person will be fully engaged from the beginning to the end of a project. First, the developer needs to determine what the data model needs to be for the SproutCore-based application.

In the case of the TPS application, there needs to be several model objects such as Employee, Manager, Organization, and more. Once the model has been fleshed out, it's the job of this developer to work on creating a client-server interface by creating a SproutCore data source; it's also their role to work with the server team, if possible, to create a JSON specification that maps easily to SproutCore data model objects. This is crucial to ensure that data loads into the application quickly and without a significant amount of client side processing of the JSON before it is loaded into the data store.



## Performance and Dev Tester



There needs to be a person that can own the integration testing of the SproutCore application; there also needs to be a person who can be dedicated to ensure that the application achieves the performance benchmarks laid out by the stakeholders. Performance is especially important when dealing with mobile applications. In the case of large projects, such as the TPS application, it is important that the various pieces that the different developers work on integrate correctly to create the overall product.



## CSS, Spiriting, and Visual Stylist


On projects that are heavily design-focused, it is important to have a person that is designated to manage CSS styling and image spiriting. This person is in change of ensuring that the design vision of the project is correctly implemented. This person does not necessarily style the individual components that developers work on, but ensures that the global theme of the application is consistent and efficiently implemented.

As the individual developers work on their various application modules, they may style it inefficiently. It is the job of the CSS and visual styling person to go through and optimize as the project progresses.



## Individual Module Contributors


The rest of the development team can be flexible and more fluid. Depending on the size of the application, you may need to have from one to five developers that contribute to different modules of the application.

In the case of the TPS application, you would have one or two developers creating the list, tree, and grid views as well as a group of two or three developers that can take care of the creation of different popup panels. Most of the popup panels in the TPS application will be things such as a preference panel, create/edit employee panel, create/edit organization panel, employee and/or organization inspector, and more.

The separation of the popup panels is important. More often than not, you do not want to load them up front and have them be lazily loaded as a module from the server. Therefore, it is vital to use a module loading scheme with a proper API to fetch and run the module as it is loaded from the server. You can have developers work on each of these, and if the API is correctly implemented in a loosely coupled manner, they can be replaced with an improved UI in the future without breaking the application.

SproutCore's MVC structure comes in handy when allocating resources to each of these smaller modules; it allows people to work on different parts of an application without stepping on each other's toes too much.

Also, if you have less experienced developers, making them start on a popup panel is a good way of giving them a limited starter project where they can learn SproutCore. If the code needs to be re-factored later, as long as the module API is properly implemented, it will not affect the rest of the application.



## Conclusion



The largest takeaway from the projects that I've worked on is that you need to have a very strong developer work on the data model, data source, and client-server integration. If you don't have that person, your project will run into trouble quite easily. When it comes to a SproutCore app, it is relatively straightforward to create the various user interface components, but without data flowing in and out of your application, all the hard work on the views do not matter at all.

While there isn't a definitive answer as to how to structure a team of developers, this is the approach that has been the most successful for me in the past. Every project has different needs and it is important to take that in account when structuring the team. Also, it is important to take in account the talents and skills of the developers that will be working on the project.

It is important to give the developers the opportunity to pick what role interests them most and, if possible, put them in that role. For the most part, a happy developer is a productive developer.

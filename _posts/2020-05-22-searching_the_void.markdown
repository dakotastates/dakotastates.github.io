---
layout: post
title:      "Searching the Void"
date:       2020-05-22 19:55:40 +0000
permalink:  searching_the_void
---


We all know the existential threat of not knowing where something is located. We search and we search but there is just too much junk. Our human brains allow us to sporadically search for something without any real guidance. Sure, it helps to have a vague idea as to where something is but it’s not entirely necessary as a lot of the time we find things by chance.  However, in the world of programming, something is either there or it isn’t. The cold, inhospitable machine bluntly does what we, the programmer, tell it to do, so that a user can find a virtual object quickly and defiantly. There is no coincidence or chance involved with machines. The programmer must strategically decide how to accept an input and search a database for an object and then return said object to the page. Once everything is set it the machine does the exact same remedial task over and over again. It does not know better or worse. It only knows the code. And so, let’s think like a machine and follow the flow of a search function. 

The first thing within a search function a user deals with is obviously the search form. Here is an example of such a form. 

![](https://i.imgur.com/if4ds9q.png)

As you can see, We have a basic cold and empty text field unknowing of it’s true potential to help a struggling user find what they are looking for on the page. But creating just the form does not mean anything will work. In fact, nothing will happen if it’s just a form. And so, we need to work with the controller. But before we look at a controller, we must make sure our form code is doing what we want it to do.

Most programmers are familiar with forms; however, at the beginning stages of learning how to code we are usually using a form to post information to a database. But with a search function we are not submitting anything, we are retrieving information. 

![](https://i.imgur.com/lcGpEwu.png) 

In the code above we are using a get method as opposed to a post method. The get method lets the controller know what we are retrieving the information from the database. 

Now if we will need to use the input provided from the form. But where do we use it? The answer is the controller. Within the controller we will use ‘strong params’ to prevent code tampering, such as SQL injection. 

![](https://i.imgur.com/aKjF1HU.png)

We place the ‘:search’ from our form into the strong param so in the future all we will need to do is call ‘problem_params’ to utilize the forms input. 

Next up we will use the ‘:search’ within out index method of the controller. The index works traditionally by setting a variable for all of the data within the database. Usually something along the lines of  ‘@problems = Problem.all’. This will allow us to view all of the items if we iterate over them within the view’s page. However, for a search function, we want to narrow what is being listed on the page to our search query.  

![](https://i.imgur.com/4bem6jL.png) 

Above we can see the entire index method within the problems controller. In order for the search function to work we need to use the params of the search query to find what we are looking for. And so, instead of having ‘@problems = Problem.all’, which displays all of the problems on the index page, we will use ‘@problems = Problem.search(params[:search])’. 

Let’s break this code down a bit. The ‘Problem’ is accessing the Problem model, which accesses the database. The ‘.search’ is a method within our model where we tell the model what it means to search for something. This method accepts an argument of ‘(params[:search])’ which is the input of what we typed into our search form.  

Please note: I included the search query assigned variable within an if statement of it’s other queuing variables. This is set up like this to accommodate other search and filter option within my model scope. If I were to establish the search scope in a different if statement it will not read the search query. Placing it with all of the other scopes it allows us to have many ways to query our database. Or if we do not want to query the database it will display all of the data within the database table.  

Now let’s look at the ‘.search’ scope method within our Model. 

![](https://i.imgur.com/zPjsm3p.png)

We keep the ‘.search’ scope method within out Model because of the concept of separation of concerns; which essentially tells asks us ‘who is responsible’ for a particular concern. All scope methods are the concern of the model, not the controller. Within the model, we have our scope method ‘self.search(search)’ 

Let’s break down the model line by line. 

The ‘self.search(search)’ is the name of the method which accepts an argument. The argument in this case is the ‘search’ query we eluded to when calling this method in the controller. 

The ‘where (‘title LIKE ?’, “%#{search} %”)’ will do the actually querying of the database. ‘Where’ is a sql search query method which narrows down the search results. We want to compare the search argument and find all title’s which are like the argument. 

Note: there are a few ways to create a scope method. We could also write the method as ‘scope :search, -> (search){where(title LIKE ?’, “%#{search} %”)}’ Basically this is one line code as opposed to multiple lines. It utilizes a lambda ( ->). 

Anyways, once the database is queried, the controller knows what to set the value of ‘@problems’ to  and then the view page only displays the queried data. 

![](https://i.imgur.com/XOvs2hl.png)

 Now if we search for ‘tacos’ it will find only the data where the title has the word ‘tacos’ within it. 

This is basic search functionality for a rails application but that does not mean there are not challenges associated with it, especially if you have other querying methods. It took me a while to figure out why my code was not working but then my human brain decided to just add it to my other if statements of queried code, which makes sense to do, and then it’s works. Image if my database was filled with millions of problems. It is absolutely unfeasible to search each entry one by one so we use programming to make our lives easier. Although we do take our machines for granted, it’s comforting to know, as a struggling programmer, that I have control over my data. I know how to manipulate it and to find what I need. The inhospitably cold machine is blunt for a reason. If it were human it would be searching for an item for a long time if there are hundreds or thousands of records to go through. It would be hoping for some luck or chance in order to find something in a timely manner. Luckily machines aren’t human and they do not experience the existential threat of not knowing where something is located. 

I hope you find what you are looking for. 



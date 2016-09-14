# re-frame-url-fx
Experimantal fx handler for re-frame

## URL Routing in re-frame

When building a web application, defining a set of URL routes that 
make sense is one of the requirements that is hard to avoid. When 
building a single page app, it is generally more difficult to do 
it right than in a traditional server based application. 

Here are some of the common issues that may need to be considered
when determining how to do URL routing in a re-frame application.

* What actions require a defined URL route? 

* What is going to be the primary driver of your application navigation?
    * Will re-frame be expected to update the URL as part of a `dispatch`?
    * Will your actions follow a link which is then expected to `dispatch` something in re-frame?

* What needs to happen to make sure there is consistency in the user
experience across the different methods of navigation?
    * In most re-frame apps, when the application is first loaded it 
        must populate `app-db` with some default value. How does that 
        initial data load differ when entering from your base URL
        compared to some other URL?
    * When a user starts at the base URL, and navigates using re-frame
        so some other URL, the expectation of their `app-db` is that
        it will contain a combination of data from their previous
        actions as well as new or modified data as a result of 
        that navigation. 
    * When a user manually enters a non-base URL, the expectation of
        the app-db is that it will contain only the data that is 
        appropriate to that URL. 

In my past work integrating Secretary with re-frame, most of the trouble
I encountered was ensuring that the data was correct for all the different
ways the user was able to get to a specific page. I think a huge part of 
those issues were in how I wanted navigation to work - I wanted re-frame
to be in charge of everything, but I ran into trouble getting Secretary
to work properly when it wasn't the primary navigator.

The concept I am planning to look into is having the URL become an effect
of my re-frame handlers, so that I can just plug in the URL that I want
as part of my normal application handling. I'm not sure how to do that 
initial data load quite yet, but I think it makes sense to make the URL
navigation a concern that can easily be added on to an existing 
re-frame application without having to do a significant amount of work.
In my ideal world this would also include a story for server-side rendering
of the initial page load, but that's a little further down the line.

 The best examples of URL routing with re-frame that I am aware of are:

  https://github.com/Day8/re-frame/blob/master/docs/External-Resources.md

  https://pupeno.com/2015/08/26/no-hashes-bidirectional-routing-in-re-frame-with-bidi-and-pushy/

  https://pupeno.com/2015/08/18/no-hashes-bidirectional-routing-in-re-frame-with-silk-and-pushy/


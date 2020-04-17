---
layout: post
title:      "Building A Single-Page Application With JavaScript and Rails"
date:       2020-04-16 20:13:15 -0400
permalink:  building_a_single-page_application_with_javascript_and_rails
---

### A single page application is an web application that requires the browser to load just a single page. The web application or website interacts with the browser by dynamically rewriting the current page with data from the web server.

I am currently developing a single-page application that is a game  of sorts for multiple people to play that picks the players most voted-for Yelp search result. It uses the Yelp "Fusion API" and gets Yelp results for the user, creates player names and asks the users to each vote one at a time for each result. Each result that was voted for by all players is then shown in a list of matches with information and links to the results Yelp pages.

Throughout developing many  apllications and projects I had not yet built anything that was as engaging or enjoayable to work on as a this most recent project using Rails back-end to generate an API that I used to service  the front-end. I previously had experience with Rails but found the fininshed project lacking the dynamic and interactice nature that one craves in any final product. What I was lacking was the core of all interactive and dynamic web apps and that is JavaScript. 

#### Ruby and JS together?
Early direction and planning of a project like this is essential. Because there are two parts working together it is important to decide which parts will perform which actions and responsibilities. An important step in this process is deciding which models will exist on the front and which wil exist on the back. I used an external API created by Yelp called "Fusion API". I used this generate a game for mutliple users to take turns voting 'like' or 'dislike' for each result. Because the search results are only relevent to one game I create a JS class for the Yelp results. However, to save users and likes to a database, I use  ```fetch()``` to add users and the Yelp Fusion id of each result that each player likes. The users and the id's of the Yelp Fusion resutls they liked. This also allows the construction of each instance of the class to only add attributes that are relevent to our app.

Rails has the option to optimize your app to be used to generate an API.  API is short for application programing interface. In the context of my application it contains JSON format objects that refer to models on the server-side.  I used a JS function called ```fetch()``` that takes an argument of the url to request and a configuration object that defines the http verb and headers.  Perfoming action on the recieved data is what allows us to update the DOM (document-object-model)
without rendering a new page. The function ```fetch()``` is defined by [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) as such--<br><br>
"The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses."<br><br>
"This method returns a Promise that you can use to retrieve the response of the request. The fetch method only has one mandatory argument, which is the URL of the resource you wish to fetch"

One of the challenges that faces any new-comer to Fetch is its ascynchonous nature. Here is an example from my code in which I had to work around with this. 

```
function getAllLikes() {
    const allLikes = []
    USERARY.forEach( (user, i) => {
        fetch(`http://localhost:3000/users/likes?name=${x}`)
                .then(response => {
                    return response.json()
                    })
                .then(json => {
                    json['data']['attributes']['likes'].forEach( like => {
                        allLikes.push(like.yelp_id)
                    })
                    return i
                })
                .then(i => {
                    if (i === USERARY.length - 1) {renderMegamatch(allLikes)}
                })
                .catch(err => {
                    console.log(err)
                    }); 
    });
};

```
You can see in this example that I have a function ```getAllLikes()``` that itterates through an array of users and fetch calls to a url that corresponds to a controller in the backend in order to recieve each of those users likes. I am using ```.then()```  which takes a function as an argument and uses the return value of the function ```.then()``` was called on as the argument to the ```.then()```  inner function. I wanted to pass each like into an array called ```allLikes``` and then call another function ```renderMatch()``` with the array of likes as an argument. You can see that I placed the ```renderMatches()``` call inside of a ```.then()``` function that is inside the ```fetch()``` so that it only calls the function after the ```forEach()``` method has completed. 

Due to the asynchronous nature of Fetch if the call to ```renderMatch()```  is outside of this fetch call it would call ```renderMatch()``` before completing itteration through the user array because fetch must wait for a response from the server so the JS reader skips over it and continues through the function.


 





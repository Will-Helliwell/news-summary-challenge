# Will's Readme - News Summary challenge

## Context

A challenge to create a small single-page web-app that retrieves data from an external API. For me this was a first time for a number of things:
* connecting to an API myself
* doing so using vanilla JS
* using any form of CSS to give even basic consideration to the presentation

## Screenshot of Use
![screenshot of app in use](https://github.com/Will-Helliwell/news-summary-challenge/blob/master/images/The%20Daily%20Will%20-%20screenshot.png)

### API details
* Requests sent to the Guardian API (via a heroku-hosted app, which assigned an API key)

## To Run

The one dependancy is HttpServer (for installation instructions, go to: https://www.npmjs.com/package/http-server).

To run via HttpServer:
* Navigate to root/views
* Run the command `npx http-server`
* Navigate to one of the URLs indicated in the terminal using your browser

## Completed
* User story 1
* User story 2
* Created a very basic article preview area for user story 3

## Still to do (next steps)
* Refactor existing JS before continuing
* Refactor CSS - create classes in separate css file
* Change article preview to a more convenient pop-up window that can be closed (perhaps bootstrap modal?)
* Connect to second API to create article summary. Insert into preview area
* Extract backend logic into separate classes and files. Unit test these with homemade test framework 'Bob'
* Implement feature testing
* Complete remaining user stories
* Create my own account fior the Guardian API and learn how to implement extra security steps

## What I learned
* Learned and used some basic CSS and HTML for the first time
* Read the documentation for an external API and used to pull out the data I needed
* Hosted the app on a local server (and now know how to get around caching issues preventing refresh for HTTP-Server)

## Steps Completed for each User Story
### 1
```
As a busy politician
So I know what the big stories of the day are
I can see all of today's headlines in one place
```
* Create static index.html
* Add index.js logic to:
  * Connect to Guardian API and return all JSON data (on document ready)
  * Convert JSON data, extract article titles, display on separate lines as links

### 2  
```
As a busy politician
So that I have something nice to look at
I can see a relevant picture to illustrate each news article when I browse headlines
```
* Extended API request to include thumbnail, then insert this as an HTML image tag below the headline anchor tag

```
As a busy politician
So that I can get an in depth understanding of a very important story
I can click a news headline to see a summary and a photo of the news article
```
* Create a basic article preview area at the top, showing image and title

```
As a busy politician
So I can get a few more details about an important story
I can see click a news article summary title which links to the original article
```

```
As a busy politician
Just in case my laptop breaks
I can read the site comfortably on my phone
```

```
As a busy politician
To make my news reading more fun
I can see whizzy animations in the app
```

-------

# Original Readme (Challenge Specification)

* Feel free to use Google, your notes, books, etc. but work on your own.
* If you refer to the solution of another coach or student, please put a link to that in your README.
* If you have a partial solution, **still check in a partial solution** and send in a pull request.
* You must submit a pull request to this repo with your code by 9am Monday morning.

## Challenge

As usual please start by forking this repo.

You'll create an app that summarises the news.

### Guidance

Make sure to look at this [guidance](https://github.com/makersacademy/course/blob/master/further_javascript/frontend_single_page_app_guidance.md)!  It'll help you point yourself in the right direction when you're figuring out how to implement some of the trickier things.

## Project overview

Your app will grab all the headlines from the Guardian newspaper API and display them on a page.  Clicking on a headline will show a summary of the article.

### Technologies

You'll write a single page web app.  You'll write your code in frontend JavaScript, CSS and HTML.  You won't use Ruby or backend JavaScript.

**And, as is the theme for this week, you won't use any libraries or frameworks!**

But, feel free to use the test framework you wrote during the week!

### Serving your app

You'll use a static web server (e.g. [http-server](https://www.npmjs.com/package/http-server)) to serve your HTML, CSS and JavaScript files.  You'll send requests to an API to get data from the Guardian and to summarise text.

> The API is hosted on an external server that you don't have to worry about.  You only need a static web server.  That's why this type of architecture is called "serverless".

## User Stories

Some of these stories will need decomposing if they seem too large.

```
As a busy politician
I can see all of today's headlines in one place
So I know what the big stories of the day are
```

```
As a busy politician
I can see a relevant picture to illustrate each news article when I browse headlines
So that I have something nice to look at
```

```
As a busy politician
I can click a news headline to see a summary and a photo of the news article
So that I can get an in depth understanding of a very important story
```

```
As a busy politician
I can see click a news article summary title which links to the original article
So I can get a few more details about an important story
```

```
As a busy politician
I can read the site comfortably on my phone
Just in case my laptop breaks
```

```
As a busy politician
I can see whizzy animations in the app
To make my news reading more fun
```

## Mockups

### Headlines page

![Headlines page mockup](/images/news-summary-project-headlines-page-mockup.png)

### Article summary page

![Article page mockup](/images/news-summary-project-article-page-mockup.png)

## API

### API authentication

So that this project can focus on the front-end, we've provided an API that you can use to talk to the Guardian API and the Aylien text summarisation API.  This API's only job is to take your request and add an API key.  This way, you don't have to store API keys in your front-end app.

> Why is it bad to store API keys in your front-end?  If we hadn't provided this API for you to use, how would you avoid this?

### API request rate limits and stubbing

The Guardian and Aylien text summarisation APIs are severely rate-limited.

**Please stub your tests so we don't exceed the daily limit.  Otherwise, all requests will be rejected and everyone's apps will stop working!**

### API Overview

The basic idea is to send an `apiRequestUrl` query parameter to the News Summary API.  The value of this parameter is the URL of the request you *would* have made to the Guardian or Aylien API, minus any API credentials.

### Guardian API example

**Please stub your tests to avoid exceeding the API rate limit**

If you wanted to get the content of an article from the Guardian API, this is the cURL request you might make.  Notice how it has a query parameter for `api-key`.

```
curl "http://content.guardianapis.com/politics/blog/2014/feb/17/alex-salmond-speech-first-minister-scottish-independence-eu-currency-live?show-fields=body&api-key=SECRET_API_KEY"
```

To make this request via the Makers News Summary API with cURL, you could do something like this:

```
curl "http://news-summary-api.herokuapp.com/guardian?apiRequestUrl=http://content.guardianapis.com/politics/blog/2014/feb/17/alex-salmond-speech-first-minister-scottish-independence-eu-currency-live?show-fields=body"
```

Note how the `apiRequestUrl` parameter value is just the request you would have made to the Guardian API, minus `api-key`.

### Aylien text summarisation API example

**Please stub your tests to avoid exceeding the API rate limit**

If you wanted to use the Aylien API to summarise an article by Bret Victor, this is the cURL request you might make.  Notice how it has headers to authenticate with the Aylien API.

```
curl "https://api.aylien.com/api/v1/summarize?url=http://worrydream.com/MediaForThinkingTheUnthinkable/note.html" \
  -H "X-AYLIEN-TextAPI-Application-ID: APPLICATION_ID" \
  -H "X-AYLIEN-TextAPI-Application-Key: SECRET_APPLICATION_KEY"
```

To make this request via the Makers News Summary API with cURL, you could do something like this.

```
curl "http://news-summary-api.herokuapp.com/aylien?apiRequestUrl=https://api.aylien.com/api/v1/summarize?url=http://worrydream.com/MediaForThinkingTheUnthinkable/note.html"
```

Note how the `apiRequestUrl` parameter is just the request you would have made to the Aylien API.  Notice how you don't have to send authentication headers.

### Code

If you're interested, you can see the code for the News Summary API in this repo: https://github.com/makersacademy/news-summary-api

## Resources

* [Guardian newspaper API homepage](http://open-platform.theguardian.com/documentation/)
* [Aylien text summary API docs](http://docs.aylien.com/docs/summarize)
* cURL [man page](https://curl.haxx.se/docs/manpage.html)
* [Hurl](https://www.hurl.it/), a web interface for sending HTTP requests

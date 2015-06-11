# API Interview Questions

### RESTFul API
The most important feature of RESTful API is stateless.

The notation of stateless is defined from the perspective of server. The constraint says that the server does not remember the state of the application. As a consequence, the client should send all information necessary for execution along with request, because the server cannot reuse the info from previous requests as it didn't memorize them.

For example, if you are browsing an image gallery and the server has just sent you image23, your client cannot simply say next to the server. Instead, it asks for image24 to advance the gallery. Indeed, your client has to supply all information necessary to execute the request, such as hypermedia links, since the server does not remember that you were viewing image23.

On the other side, you don't need to know the image you were viewing was image23. Because, along with the representation of this image, the server can send you links labeled 'previous' and 'next', leading to corresponding images. e.g.
```
{
  imageId: 23,
  url: 'some/url',
  next: 'some/url/to/next',
  previous: 'some/url/to/previous'
}
```
To ask for image24, client just needs to call the 'next' link. Didn't we say server does not know about information about previous request? Isn't that a contradiction? No, it's not; at the time the server was generating the representation of image23, the server was in the middle of processing your request, so it knew which image you requested and what the previous and next images were.

Stateless makes the web better.

It increases visibility, every request contains all context necessary to understand it. Therefore, looking at a single request is sufficient to visualize the interaction.

It increases reliability, since a request stands on its own, failure of one request does not influence others.

It increases scalability, the server does not have to remember the application state, enabling it to serve more requests in a short amount of time.


### What is JSONP?
JSONP is a method commonly used to bypass the cross-domain policies in web browsers(you are not allowed to make AJAX requests to a webpage perceived to be on a different server by the browser).

JSONP requests are not dispatched using the XMLHTTPRequest (and the associated browser methods), instead a *\<script\>* tag is created, whoese source is set to the target URL. This script tag is then added to the DOM (normally the *\<head\>*).

**JSON Request:**
```
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function() {
  if (xhr.readyState == 4 && xhr.status == 200) {
    // success
  }
}

xhr.open('GET', 'somewhere.php', true);
xhr.send();
```

**JSONP Request:**
```
function foo(response) {
  document.getElementById("output").innerHTML = response.bar;
}

var tag = document.createElement('script');
tag.src = 'somewhere_else.php?callback=foo';

document.getElementByTagName('head')[0].appendChild(tag);
```

The difference between a JSON request and a JSONP request, is that the JSONP response is formulated such that the response object is passed as an argument to a callback function.

**JSON**
```
{
  'bar': 'Bar'
}
```
**JSONP**
```
foo({
  'bar': 'Bar'
)};
```
This is why you see JSONP requests containing the *callback* parameter; so the server knows the name of the function to wrap the response around.

This function must exit in the global scope at the time the *\<script\>* tag is evaluated by the browser (once the request has completed).

The usefulness of using jQuery to make JSONP requests, is that jQuery does alllllllll of the work for you in the background.

jQuery requires (by default), for you to include &callback=? in the URL of your AJAX request. jQuery will take the success function you specify, assign it a unique name and publish it in the global scope. It will then replace the **?** in **&callback=?** with the name it's just assigned the function.

### JSON vs XML
JSON Pro:
  1. Simple syntax, which results in less 'markup' overhead compared to XML.
  2. Easy to use with JavaScript as the markup is a subset of Javascript object literal notation and has the same datatype as Javascript.

JSON Con:
  1. Only a handful of different datatypes are supported.

XML Pro:
  1. XPath/XQuery for extracting information (which makes getting information in deeply nested structures much easier than with JSON).
  2. XSLT for transformation into different output formats.
  3. XML Schema for datatype, structure validation. Makes it possible to create new datatypes.

XML Con:
  1. It's wordy compared to JSON(result in more data for the same amount of infomation).

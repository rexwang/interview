# API Interview Questions

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

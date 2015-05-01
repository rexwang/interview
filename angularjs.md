# Angularjs Interview questions

### Angular executing order
1. app.config()
2. app.run()
3. directive's compile functions (if they are found in the dom)
4. app.controller()
5. directive's link functions (again if found)

[example link](http://jsfiddle.net/ysq3m/)

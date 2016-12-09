# CTF Tactics

This guide describes a basic workflow on how to approach various web CTF challenges.
Throughout the CTFs that I have participated in this year, there has been alot of moments where I would spend too many hours on an easy challenge mainly because of oversight, or insufficient recon.

This guide tries to cover these oversights, in order to get gain as much relevant info as possible before charging into exploitation.

## Recon

### What web server/programming language/backend is used?

This part will help determine what vulnerabilities you're most likely to see... For example, template injections are more likely to occur in python web apps than in PHP apps.

We can test what programming language is used by changing the extension on the main page of the app. Try various extensions like : 
  - `index.php`
  - `index.cgi`
  - `index.html`
  - ...
  
If none of these work, we're most likely dealing with technologies using action dispatchers like `RoR` and `Django`.
To validate this, we can take a look at what `404` page is generated. This will also be useful to determine what server is being used.

Try to browse to a non-existant URL like `/THIS_PAGE_DOESNT_EXIST` to see what comes up. On Apache/NGINX servers, default 404 pages can leak which OS is used, as well as the server's version.

At this point, if we still don't know what backend is running, we can check the headers of the HTTP responses for the `Server` header.

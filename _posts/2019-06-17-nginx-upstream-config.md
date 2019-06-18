---
layout: post
title: "Nginx upstream (tricky) configuration [SD]"
comments: true
description: "Nginx upstream (tricky) configuration [SD]"
keywords: "Nginx upstream self documentation"
---

# Nginx upstream (tricky) configuration [SD]

Some days ago I was working with Nginx upstream rules to redirects some request to an API. I was facing one problem with the following Nginx rules I wrote.

```
    upstream xyz_service {
      server myremoteserver.xyz:1234
    }

    location /api_xyz/ {
      proxy_pass http://xyz_service;
    }
```
Those rules were adding the location rule to the redirected url.

```
    https://myremoteserver.xyz:1234/api_xyz/  <=== Like this one
```
But I needed make the `proxy_pass` without adding that stuff at the end of the redirection.


I found something to have in account about upstream rules.
Do you need to **remove** the location rule included at the end `proxy_pass` redirection ?. If so,
 you have to **add** an slash **/** at the end of the `proxy_pass` redirection, as shown below.

```
Original
    location /api_xyz/ {
      proxy_pass http://xyz_service;    <==== This add api_xyz at the end of the request
    }

Solution
    location /api_xyz/ {
      proxy_pass http://xyz_service/;   <==== This doesn't add the location rule (Little trick)
    }
```

Resource(s):
* https://stackoverflow.com/a/32543398

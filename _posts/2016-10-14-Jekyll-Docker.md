---
layout: post
title: Jekyll on Docker
---

So as my main machine is on Windows and I already have Docker for Windows installed, I thought I would
attempt to do update my site offline before checking it in to GitHub pages.

Turns out it was very easy to do.

* First I cloned a copy of my site  
```posh
git clone https://github.com/scotta01/scotta01.github.io
```

* Then run the Official Jekyll docker image mounting the git repository to /srv/jekyll  
```posh
 docker run -it --rm `
        --name=mysite `
        --volume=$(pwd):/srv/jekyll `
        -p 4000:4000 `
        jekyll/jekyll
```

* Open up the browser to http://localhost:4000   

![alt text](/images/docker_jekyll_browser.png "Jekyll in Docker ")


And there we have it. I can restart the docker machine after each change, check in my changes and push to GitHub when I'm happy with them.

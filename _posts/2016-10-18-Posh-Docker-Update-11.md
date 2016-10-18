---
layout: post
title: Docker PowerShell update
---

The latest version of open sourced PowerShell is available on [Github](http://github.com/PowerShell/PowerShell/releases)

I have updated my docker image with this latest version. It appears the new version requires libcurl3, so you may notice the image is quite a bit bigger
where all the dependancies have been installed.

If you wish to take a look and try it for yourself, you can find the image on the Docker hub [scotta01/powershell](https://hub.docker.com/r/scotta01/powershell/)

Alternatively to dive right in, fire up docker and run

```
docker run -it --rm scotta01/powershell
```


![alt text](/images/ps_docker.png "PowerShell on Docker ")
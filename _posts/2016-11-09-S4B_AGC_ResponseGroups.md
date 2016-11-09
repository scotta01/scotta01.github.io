---
layout: post
title: Skype for Business Response Group distortion
---

Today I had a call logged that one of our customers IVR Response Groups, the audio was choppy and distorted.
This was unsual nothing for this particular site had changed and the audio files are the originals from 6 months ago.  

After alot of digging around in call logs something popped up I had never noticed on a Response Group before.

> Callee AGC Metrics
> 	 	Received noise level:	-72 dBov	AGC signal:	-90 dBov
> 	 	AGC gain:	0 dB	 	 


It appears that Skype has started applying Automatic Gain Control (AGC) to response group audio files.  

![Low Volume Audio](/images/low_volume_s4b.png)

Sure enough after opening the file in Audacity the sound levels are very low. I added some gain to the files and straight away the distortion stopped. I am not sure if this is something
that has been added to Skype in the latest CU or if just the thresholds have changed.

Hopefully this will help someone else out and save them the time I wasted on it.
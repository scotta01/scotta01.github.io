---
layout: post
title: Polycom CX phones and Root CAs
---

Today I renewed our Skype for Business server certificates. All seemed fine, for a couple of hours.

We started seeing our Polycom CX600 phones logging out and unable to log back in. They were showing an error _"Cannot download the certificate because the domain is unavailable"_

A quick google led me to [Jeff Schertz blog](http://blog.schertz.name/2014/10/lync-phone-edition-and-public-certificates/)

It appears the older Aries based devices have a limited list of Trusted Public Certificate Authorities. It appears our certificate provider have changed their root certificate chain.
I checked and the correct certificates were in their respective container, however Skype still needs to know which ones to trust. To do this the following needs to be done.

* Find each certificate in your certificate chain
![Skype Cert Chain](/images/Skype_CA.png)

* Open each certificate and note down the thumbprint
![Skype CA Thumbprint](/images/Skype_CA_Thumbprint.png)

* Repeat this for each certificate in the chain.

* With the all the thumbprints we can run a PowerShell command to add them to the list of CAs the Skype Web Service trusts

```powershell
$rootthumbprint = "ca3afbcf1240364b44b216208880483919937cf7"
$intermediatethumbprint = "6036330e1643a0cee19c8af780e0f3e8f59ca1a3"

$rootcert = New-CsWebTrustedCACertificate -Thumbprint $rootthumbprint -CAStore TrustedRootCA
$intermediatecert = New-CsWebTrustedCACertificate -Thumbprint $intermediatethumbprint -CAStore IntermediateCA

Set-CsWebServiceConfiguration -TrustedCACerts @{Add=$rootcert,$intermediatecert}
```
* Make sure to mark the correct cert for TrustedRootCA for the root certificate or IntermediateCA for any further subordinates.


After a couple of minutes, the phones were able to sign in again fine.
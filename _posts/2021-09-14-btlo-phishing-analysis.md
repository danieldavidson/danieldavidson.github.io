---
layout: post
title:  "BTLO: Phishing Analysis"
date:   2021-09-14 22:30:00
description: "Blue Team Labs: Phishing Analysis Writeup"
toc: true
tags:
 - blueteamlabs
 - SOC
 - security operations
comments: true
---

Reading Time: 7 minutes

---

This is my write-up for [Phishing Analysis](https://blueteamlabs.online/home/challenge/16) on Blue Team Labs.

<p align="center">
  <img src="https://i.imgur.com/ig5AkZP.png">
</p>

**P.S: I highly encourage you to try solving the challenges on your own first then check this writeup if you are stuck.**

**Scenario**

>A user has received a phishing email and forwarded it to the SOC. Can you investigate the email and attachment to collect useful artifacts?

To solve this challenge we are required to download the task file, extract the zip file using the password provided, and open the `.eml` file in any text editor you want. I will be using `gedit`.

## **Q.** Who is the primary recipient of this email?

**A.** kinnar1975@yahoo.co.uk

```
________________________________
From: Mail Delivery System <Mailer-Daemon@se7-syd.hostedmail.net.au>
Sent: 18 March 2021 04:14
To: kinnar1975@yahoo.co.uk <kinnar1975@yahoo.co.uk>
...
```

## **Q.** What is the subject of this email?

**A.** Undeliverable: Website contact form submission

```
________________________________
From: Mail Delivery System <Mailer-Daemon@se7-syd.hostedmail.net.au>
Sent: 18 March 2021 04:14
To: kinnar1975@yahoo.co.uk <kinnar1975@yahoo.co.uk>
Subject: Undeliverable: Website contact form submission

This message was created automatically by mail delivery software.
...

```

## **Q.** What is the date and time the email was sent?

**A.** 18 March 2021 04:14

```
________________________________
From: Mail Delivery System <Mailer-Daemon@se7-syd.hostedmail.net.au>
Sent: 18 March 2021 04:14
To: kinnar1975@yahoo.co.uk <kinnar1975@yahoo.co.uk>
Subject: Undeliverable: Website contact form submission

This message was created automatically by mail delivery software.
...
```

## **Q.** What is the Orginating IP?

**A.** 103.9.171.10

```
--_004_VI1PR0102MB31679BEF784B62C41CDAEDB282689VI1PR0102MB3167_
Content-Type: message/rfc822
Content-Disposition: attachment;
	creation-date="Thu, 18 Mar 2021 04:14:19 GMT";
	modification-date="Thu, 18 Mar 2021 04:14:19 GMT"
Content-ID: <5A9638EA6676A449B32643CFC62AAB5F@eurprd01.prod.exchangelabs.com>

Received: from c5s2-1e-syd.hosting-services.net.au ([103.9.171.10])
	by se7-syd.hostedmail.net.au with esmtps (TLSv1.2:AES128-GCM-SHA256:128)
	(Exim 4.92)
	id 1lMk2r-0007vB-6O
	for kinnar1975@yahoo.co.uk; Thu, 18 Mar 2021 15:14:06 +1100
Received: from markgard by c5s2-1e-syd.hosting-services.net.au with local (Exim 4.94)
	id 1lMk2m-002w3b-NT
	for kinnar1975@yahoo.co.uk; Thu, 18 Mar 2021 15:13:56 +1100
To: kinnar1975@yahoo.co.uk
Subject: Website contact form submission
...
```

## **Q.** Perform reverse DNS on this IP address, what is the resolved host?

**A.** c5s2-1e-syd.hosting-services.net.au

Used [https://whois.domaintools.com](https://whois.domaintools.com/103.9.171.10) to perform reverse dns query.

![](https://i.imgur.com/UIAh6Im.png)

## **Q.** What is the name of the attached file?

**A.** Website contact form submission.eml

```console
# ls
'Website contact form submission.eml'
```

## **Q.** What is the URL found inside the attachment?

**A.** https://35000usdperwwekpodf.blogspot.sg?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o=0hnd

```
...
<p>Good earnings from $6500 per day &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt=
;     https://35000usdperwwekpodf.blogspot.sg?p=3D9swghttps://35000usdperww=
ekpodf.blogspot.co.il?o=3D0hnd   &lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt;&l=
t;</p></body>
</html>
```

This was a little tricky as you need to remove the URL encoding. See example below.

>BEFORE

```
https://35000usdperwwekpodf.blogspot.com/?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o%3D0hnd
```

>AFTER

```
https://35000usdperwwekpodf.blogspot.sg?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o=0hnd
```

## **Q.** What service is this webpage hosted on?

**A.** Blogspot

Answer is contained within the URL

## **Q.** Using URL2PNG, what is the heading text on this page? (Doesn't matter if the page has been taken down!)

**A.** Blog has been removed

Go to [https://www.url2png.com](https://www.url2png.com) and paste the URL found inside the attachment.

**References:**
- [https://blog.joshlemon.com.au/analysing-malicious-email-files/](https://blog.joshlemon.com.au/analysing-malicious-email-files/)

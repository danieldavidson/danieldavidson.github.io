---
layout: post
title:  "BTLO Writeup: Phishing Analysis 2"
date:   2021-09-14 23:30:00
description: "Blue Team Labs: Phishing Analysis 2 Writeup"
toc: true
tags:
 - blueteamlabs
 - SOC
 - security operations
comments: true
---

Reading Time: 7 minutes

---

This is my write-up for [Phishing Analysis 2](https://blueteamlabs.online/home/challenge/24) on Blue Team Labs.

<p align="center">
  <img src="https://i.imgur.com/jXgKJPc.png">
</p>

**P.S: I highly encourage you to try solving the challenges on your own first then check this writeup if you are stuck.**

**Scenario**

>Put your phishing analysis skils to the test by triaging and collecting information about a recent phishing campaign.

To solve this challenge we are required to download the task file, extract the zip file using the password provided, and open the `.eml` file in any text editor you want. I will be using `gedit`.

## **Q.** What is the sending email address?

**A.** amazon@zyevantoby.cn

```
From: Amazn <amazon@zyevantoby.cn>
To: saintington73 <saintington73@outlook.com>
Subject: Your Account has been locked
Date: Wed, 14 Jul 2021 01:40:32 +0900
Message-ID: <000756bf516d$9bad2034$6e61f7fb$@vinuqou>
...
```

## **Q.** What is the recipient email address?

**A.** saintington73@outlook.com

```
From: Amazn <amazon@zyevantoby.cn>
To: saintington73 <saintington73@outlook.com>
Subject: Your Account has been locked
Date: Wed, 14 Jul 2021 01:40:32 +0900
Message-ID: <000756bf516d$9bad2034$6e61f7fb$@vinuqou>
...

```

## **Q.** What is the subject line of the email?

**A.** Your Account has been locked

```
Subject: Your Account has been locked
Date: Wed, 14 Jul 2021 01:40:32 +0900
Message-ID: <000756bf516d$9bad2034$6e61f7fb$@vinuqou>
...
```

## **Q.** What company is the attacker trying to imitate?

**A.** Amazon

```
From: Amazn <amazon@zyevantoby.cn>
...
```

## **Q.** What is the date and time the email was sent? (As copied from a text editor)

**A.** Wed, 14 Jul 2021 01:40:32 +0900

```
Date: Wed, 14 Jul 2021 01:40:32 +0900
...
```

## **Q.** What is the URL of the main call-to-action button?

**A.** https://emea01.safelinks.protection.outlook.com/?url=https%3A%2F%2Famaozn.zzyuchengzhika.cn%2F%3Fmailtoken%3Dsaintington73%40outlook.com&data=04%7C01%7C%7C70072381ba6e49d1d12d08d94632811e%7C84df9e7fe9f640afb435aaaaaaaaaaaa%7C1%7C0%7C637618004988892053%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=oPvTW08ASiViZTLfMECsvwDvguT6ODYKPQZNK3203m0%3D&reserved=0

```
<TD align="center" class="mcnButtonContent" valign="middle" style="padding: 20px; font-family: Arial; font-size: 16px;"><A title="Review Account" class="mcnButton" style="text-align: center; color: rgb(255, 255, 255); line-height: 100%; letter-spacing: normal; font-weight: bold; text-decoration: none;" href="https://emea01.safelinks.protection.outlook.com/?url=https%3A%2F%2Famaozn.zzyuchengzhika.cn%2F%3Fmailtoken%3Dsaintington73%40outlook.com&amp;data=04%7C01%7C%7C70072381ba6e49d1d12d08d94632811e%7C84df9e7fe9f640afb435aaaaaaaaaaaa%7C1%7C0%7C637618004988892053%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&amp;sdata=oPvTW08ASiViZTLfMECsvwDvguT6ODYKPQZNK3203m0%3D&amp;reserved=0" originalSrc="https://amaozn.zzyuchengzhika.cn/?mailtoken=saintington73@outlook.com" shash="Fs6cig8SRUo6Yy/pwwp7bmc4QzHa7mipEFApeNMEIJLHvXJD9hfKyBwuC15cZyvTqeMhxfySpUVyqi3LJVJRYmYealKld7FRPW8cYeBFLrZb+qOcKx3Po2WpFWyOukDUKStz+9k7dXejUhmw3WGJuyIz8OCD12wPagtFXHYyHJk=" target="_blank">Review Account</A></TD>
```

## **Q.** Look at the URL using URL2PNG. What is the first sentence (heading) displayed on this site? (regardless of whether you think the site is malicious or not)

**A.** This web page could not be loaded.

Go to [https://www.url2png.com](https://www.url2png.com) and paste the URL found inside the attachment.

![](https://i.imgur.com/1F6b4MU.png)

## **Q.** When looking at the main body content in a text editor, what encoding scheme is being used?

**A.** base64

```
------=_NextPart_000_0232_018D8931.1E363E20
Content-Type: text/plain;
	charset="utf-8"
Content-Transfer-Encoding: base64
...
```

Decoding base64 into plain text

```console
# base64 --decode btlo-pa2-text.encoded > btlo-pa2-text.decoded
# cat btlo-pa2-text.decoded

Hello Dear Customer,

Your aϲϲount access has been limited. We've noticed significant changes in your aϲϲount activity. As your payment process, We need to understand these changes better

This Limitation will affect your ability to:
Ρay.Change your payment method.Buy or redeem gift cards.Close your aϲϲount.
What to do next:

Please click the link above and follow the steps in order to Review The Account, If we don't receive the information within 72 hours, Your aϲϲount aϲϲess may be lost.


                                     











Review Account


Yours Sincerely, 

Amazon Support Team
Copyright © 1999-2021 Amazon. All rights reserved.
```


## **Q.** What is the URL used to retrieve the company's logo in the email?

**A.** https://images.squarespace-cdn.com/content/52e2b6d3e4b06446e8bf13ed/1500584238342-OX2L298XVSKF8AO6I3SV/amazon-logo?format=750w&amp;content-type=image%2Fpng

```
... src="https://images.squarespace-cdn.com/content/52e2b6d3e4b06446e8bf13ed/1500584238342-OX2L298XVSKF8AO6I3SV/amazon-logo?format=750w&amp;content-type=image%2Fpng" 
      border="0" hspace="0"> 
```

## **Q.** For some unknown reason one of the URLs contains a Facebook profile URL. What is the username (not necessarily the display name) of this account, based on the URL?

**A.** amir.boyka.7

```
...originalSrc="https://www.facebook.com/amir.boyka.7"
```

**References:**
- [https://www.url2png.com/](https://www.url2png.com/)
- [https://blog.joshlemon.com.au/analysing-malicious-email-files/](https://blog.joshlemon.com.au/analysing-malicious-email-files/)
- [https://www.encryptomatic.com/viewer/](https://www.encryptomatic.com/viewer/)

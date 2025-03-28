---
title: "Open Redirect to XSS: Chaining Vulnerabilities for Maximum Impact"
datePublished: Tue Dec 17 2024 08:28:10 GMT+0000 (Coordinated Universal Time)
cuid: cm8slmr6g001f09ju1ddi412g
slug: open-redirect-to-xss-chaining-vulnerabilities-for-maximum-impact-36ae8dd9f198
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743155253903/0e244640-68ce-42fe-801e-e4be9cc9a647.png

---

*Hello guys! I’m back again with a real-life example of how I turned a simple open redirect vulnerability into a reflected XSS exploit.*

*At first glance, an open redirect might not seem like much of a big deal. However, when paired with the right tricks, it can lead to something much worse, like Cross-Site Scripting (XSS).*

### Discovery

While poking around a target application, I noticed an endpoint that looked suspiciously vulnerable. It was used to verify user accounts and had a parameter named `targetpage`.

https://redacted/account/verify?targetpage=/account-settings.htm

The `**targetpage**` parameter decided where users would be redirected. It didn’t seem to validate the input, so I thought, "What happens if I mess with it?"

### Confirming the Open Redirect

To test my theory, I created a URL that pointed to a random external site:

https://redacted/account/verify?targetpage=https://evil.com

Sure enough, when I visited the URL, the app redirected me straight to `https://evil.com` without any checks. Bingo! The open redirect was confirmed.

### Turning It Into XSS

Finding an open redirect is cool, but I wanted to see if I could take it further. I hosted a simple JavaScript payload on my own server and then created this URL

https://redacted/account/verify?targetpage=http://attacker-server/test.html

When someone clicked the link, the app redirected them to my malicious page. The JavaScript I placed there ran instantly in their browser, proving the reflected XSS was possible.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743155250683/2b344d88-8ffd-4493-b845-e99c84e69da2.jpeg)

I reported the vulnerability. Although it came back as Dup, I was still glade I found that.

#### **Take Away:**

*What seemed like a minor open redirect vulnerability turned out to be a gateway for much more serious exploits. This shows how important it is to validate user input and think critically about how small flaws can escalate. Always keep an eye out for these hidden risks. Happy Hunting! : )*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743155252182/b9b8adf6-ebdd-4078-bc7a-7c42b75bcd86.gif)
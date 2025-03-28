---
title: "Session Hijacking Vulnerability in Password Reset Flow Leading to Cross-Account Access"
datePublished: Tue Dec 31 2024 19:00:19 GMT+0000 (Coordinated Universal Time)
cuid: cm8slmind001g09jog49k73rg
slug: session-hijacking-vulnerability-in-password-reset-flow-leading-to-cross-account-access-4823d88e680a

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743155238546/f93dc641-4e8d-496a-8f6a-abbef53b8808.gif)

### Hello guys! I’m here again with another vulnerability, last one for the year 2024. Let’s get started : )

Imagine trying to reset your password on one account, only to realize you’ve inadvertently gained control over another. That’s exactly what happened here. A session and OTP vulnerability allowed one account’s reset process to affect another, exposing a significant security flaw.

### The Discovery

It all started when I made an attempt to reset the password for one of my accounts (let’s call this Account A) . The process seemed straightforward. Initiate a reset, get an OTP, and proceed. However, things took a turn when the email associated with the reset was swapped from Account A to Account B during the session.

Surprisingly, using the OTP sent to Account A, the password for Account B was successfully reset *(H@ppynewy3@r!).* But here’s the kicker. Both Account A and Account B ended up with the exact same new password *(H@ppynewy3@r!)*.

At no point was the reset process for Account A explicitly completed. Yet, somehow, both accounts were affected simultaneously.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743155240450/bf2677c6-81c7-4644-8a48-91302a9c88c4.gif)

### Why Is This a Big Deal?

This vulnerability suggests a fundamental flaw in how password reset sessions and OTPs are managed. Sessions and OTPs, which should be tightly bound to a single account, were instead loosely validated, allowing cross-account interference.

In simpler terms, if you can manipulate the session or account reference mid-reset, you can essentially gain unauthorized access to accounts you shouldn’t have control over.

### The Fix

*Addressing this vulnerability would require*:

1\. Session Binding: Ensure sessions are strictly bound to the initiating account.

2\. OTP Validation: OTPs must validate against the original account and expire if context changes.

3\. Session Invalidation: Any mid-process changes (like switching emails) should invalidate the active session.

4\. Additional Checks: Double verification on sensitive operations, such as email or password resets.

### Final Thoughts

Password resets are often overlooked as simple, routine actions, but they’re also critical entry points for security vulnerabilities. This bug serves as a big reminder of how a single oversight in session and OTP management can lead to cascading security failures.

Lastly, Incase you’re reading this from the future, Happy Hunting and Happy New Year! 🎊…….: )

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1743155242227/890bde0e-ca44-4fea-a5da-971bd15ea491.gif)
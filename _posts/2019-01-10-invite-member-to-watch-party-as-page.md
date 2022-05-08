---
title: Inviting group member to join watch party as page analyst on behalf page
date: 2019-01-10 14:20:21 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---

# Description

It is possible for page analyst to invite another group-linked-page member to watch party on behalf the page itself.

# Impact

This would allow a group-linked Page Analyst to be able to invite Group members to join the watch party as the Page instead of their normal user.

# Steps to reproduce 

1. As page analyst create a watch party in group and you will redirect to https://www.facebook.com/groups/<Group ID>/wp/<Watch Party>
2. Once you redirect, change the url to https://www.facebook.com/groups/<Group ID>/wp/<Watch Party>/?av=<Page ID>
3. Now go to invite menu and invite any group member and they will receive the notification from the page.


## Video 

<iframe width="560" height="315" src="https://www.youtube.com/embed/_3I46T2Eswo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Timeline

- Aug 22, 2018 - Report sent
- Aug 25, 2018 - Triaged
- Sep 06, 2018 - Fixed
- Sep 23, 2018 - Send information (still incomplete fix)
- Oct 04, 2018 - Bounty awarded $500
- Jan 10, 2019 - All Fixed
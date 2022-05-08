---
title: Adding video to the watch party on behalf page as page analyst
date: 2019-01-10 11:12:24 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---


# Description

When the page is linked to the group and the page analyst is the member of the group, the page analyst can add a watch video on behalf the page. But to do that, the page analyst should be a Host / Co-Host to the watch party.

# Impact

This bug could allow a page analyst to add a video to a watch party on behalf of a linked page, when they should not be able to do so.

# Steps to reproduce 

1. Attacker create a watch party in the group-linked page (https://www.facebook.com/groups/GROUP_ID)
2. Attacker will redirect to the watch party with the following url like this (https://www.facebook.com/groups/GROUP_D/wp/WATCH_PARTY_ID
3. Attacker added a video by clicking the Add Video > Click a video to be added > Intercept the request using burp/ any http intercept.
The following request and response > https://pastebin.com/SbKRnWtV
4. Attacker modifying the Creator_actor_id to Page ID.
5. Attacker then send the request.

## Video 

<iframe width="560" height="315" src="https://www.youtube.com/embed/W0HqU74wDR8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



# Timeline

- Nov 02, 2018 - Report sent
- Nov 07, 2018 - Triaged
- Dec 20, 2018 - Bounty awarded $500
- Jan 10, 2019 - Fixed
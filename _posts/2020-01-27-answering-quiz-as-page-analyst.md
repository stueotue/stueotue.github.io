---
title: Answering group quiz on behalf page as page analyst
date: 2020-01-27 11:12:24 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---


# Description

When the page is linked to the group and the page analyst is the member of the group, the page analyst can answer the quiz on behalf the page.

# Impact

A page analyst is able to take a group quiz on page's behalf.

# Steps to reproduce 

1. Attacker go to the unit tab which had a quiz. (https://web.facebook.com/groups/GROUP_ID/learning_content/?filter=UNIT_ID)
2. Attacker answer the quiz and intercept the requests (using Burp suite or another http interceptor)
3. Attacker change the value of av parameter to page_id
4. Attacker Forward/Send the requests

- When victim download the quiz results, it will appear as the page that answer the quiz.

## Video 

<iframe width="560" height="315" src="https://www.youtube.com/embed/IFviNS76th4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



# Timeline

- Dec 15, 2019 - Report sent
- Dec 18, 2019 - Triaged
- Jan 26, 2020 - Fixed
- Jan 27, 2020 - Bounty awarded $750
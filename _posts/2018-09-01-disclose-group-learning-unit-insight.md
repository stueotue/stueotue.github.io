---
title: Disclose group learning unit insight
date: 2018-09-01 14:20:21 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---

# Description

There is an IDOR issue in a feature called learning unit which lead to disclose the Group Insight. If the targeted group privacy is public, then attacker can disclose the group insight without become a member and for closed/secret group privacy, attacker need to become a member.

# Impact

This could have allowed a group member to add Learning Units to their own Group, which would have then allowed them to download the Group Insights for those Learning Units.

# Steps to reproduce 

1. Bob go to Victim Group and started to browse to Victim Group learning unit.
From here Bob collect the Unit Name/Unit ID from the Victim Group:
* HTML/10
* Javascript/20
* Python/30
* Test Section/40
2. Bob go to his group (Attacker Group) and open his Social Learning Unit (https://www.facebook.com/groups/2/learning_content/)
3. Bob click on the Settings, open his burpsuite and turn on the intercept.
4. Bob Click the Save button and capture the request using burpsuite.
Request :
POST /groups/learning/edit_units_dialog/submit/
group_id=298905900874017&description=&unit_ids[0]=5
5. Bob edit the request by adding the Victim Group unit_ids
Editted Request :
POST /groups/learning/edit_units_dialog/submit/
group_id=298905900874017&description=&unit_ids[0]=10&unit_ids[1]=20&unit_ids[2]=30&unit_ids[3]=40
6. Bob forward the request. 
From here the Victim Group Learning unit is shown up in Attacker Group.
7. Bob go to "Group Insight" from his group (Attacker Group) and can see the Victim Unit details.
8. For more detail, Bob click the "Download Details" from his group insight (Attacker Group), wait for the notification from Facebook.
To download the insight the url is : https://www.facebook.com/groups/GROUPID/completions_export/
9. After get notification Bob open a new tab from his browser and entering this url :
https://www.facebook.com/groups/2/completions_export/

Finally Bob can see the Victim unit progress, which member already complete the learning unit etc..

## Video 

<iframe width="560" height="315" src="https://www.youtube.com/embed/cX-Vms519Sk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Timeline

- Aug 18, 2018 - Report sent
- Aug 23, 2018 - Triaged
- Sep 1, 2018 - Fixed
- Sep 1, 2018 - Bounty awarded $1500
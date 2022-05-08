---
title: Report a content as page analyst on behalf a page
date: 2021-04-16 13:00:24 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---

# Description

In Facebook pages, page analysts roles can only view insight, view page quality and view who published a post as page (https://web.facebook.com/help/289207354498410).
I've found a privilege escalation which can make page analyst report a post/comment on behalf the Page.

# Impact 

A page analyst able to report a post comment on behalf of the page.

# FBDL Run

```
[setup]
User PageOwner
User PageAnalyst
User PageLiker
Page PageOne with {owner: PageOwner, analysts: [PageAnalyst]}
[action]
PageLiker like_page PageOne
PageOwner as PageOne make_post_text TextPost with {place: PageOne}
PageLiker make_comment CommentOne with {place: TextPost}
PageLiker like_post TextPost

Results:
PageOwner => 100063478280307
PageAnalyst => 100063829416094
PageLiker => 100063944491179
PageOne => 104618658339393
TextPost => 104618881672704
CommentOne => 104618955006030
```

# Steps to Reproduce 

1. Log in as PageAnalyst
2. Go to PageOne Post (https://web.facebook.com/104618881672704)
3. Report the PageLiker comment by clicking the Three Dots -> Give feedback or report this comment
4. Use Harrasment as the report problem and click Next.
5. Check the "Yes, I'd like to continue filling this report" and click Next
6. Go to page support inbox (https://web.facebook.com/104618658339393/settings/?tab=support_dashboard) and you'll see the report from the PageAnalyst goes there.

## Video 

<iframe width="560" height="315" src="https://www.youtube.com/embed/aTTMfFlTHXw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
</iframe>


# Timeline

- Feb 17, 2021 - Report sent
- Feb 23, 2021 - Triaged
- Apr 13, 2021 - Fixed
- Apr 16, 2021 - Bounty awarded $525
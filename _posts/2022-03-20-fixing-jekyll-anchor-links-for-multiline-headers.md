---
title: Fixing Jekyll Anchor Headings links for multiline headings
image: /assets/images/2022/jekyll-header.png
tags:
    - Jekyll
    - CSS
---

As [mentioned a few weeks ago](/blog-v2-1-with-table-of-contents-and-anchor-links/) I'm now using the `jekyll-anchor-headings` scripts to add links to each header. This works great, but... unfortunately has side effects if the header is more than one line. Time to fix that!

## The problem 

When the header is multiline, all lines after the first have an incorrect indent making them appear misaligned with the rest of the post:

| Before | After |
| -- | -- |
| ![](/assets/images/2022/header-old.png) | ![](/assets/images/2022/header-new.png) |

Obviously this isn't a *big* deal, but it was annoying enough that I decided to fix it! Luckily, the fix was relatively simple, converting the existing `padding-left` & `margin-left` solution to a `text-indent` solution.

## The fix

<table>
<tr><td>Old</td><td>New</td></tr>
<tr><td>

<pre>
h2 {
    margin-left: -18px;
    padding-left: 8px;
}
</pre>

</td><td>

<pre>
.post-content h2 {
    text-indent: -10px;
}
</pre>

</td></tr>
</table>

The previous solution used `margin-left` which applied a margin to the *entire* header, and `padding-left` which applied padding to *every line* of the header. This was fine for single line headers, but caused issues when the header spread over multiple lines, as only the first line is affected by the added `<a>` permalink. 

The end result is additional header lines not being affected by the margin, and being offset too far to the left.
The solution was to use `text-indent`, which only indents the first line, where the added permalink is included.

Additionally, I noticed the indentation was applying to the homepage (which didn't include the anchor heading plugin), so changed the CSS to only apply on a post by adding the `.post-content` selector. 

[Here's the full CSS change](https://github.com/JakeSteam/blog-programming/commit/4e7c6b6a7509324389c8a8d70cd184cc0a0bff4e), but essentially you're just replacing all of the `hX` CSS classes in [the example](https://github.com/allejo/jekyll-anchor-headings/wiki/Examples#github-style-octicon-links) with:

```
.post-content h2 {
    text-indent: -10px;
}

.post-content h3 {
    text-indent: -8px;
}

.post-content h4 {
    text-indent: -6px;
}

.post-content h5 {
    text-indent: -4px;
}

.post-content h6 {
    text-indent: -2px;
}
```
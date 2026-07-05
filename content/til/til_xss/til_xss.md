---
title: "XSS is way simpler (and scarier) than I thought"
date: 2026-06-28
# weight: 1
# aliases: ["/first"]
tags: ["XSS", "Web Security", "JavaScript", "Cybersecurity", "Web Development", "TIL"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: false
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Edit" # edit text
    appendFilePath: true # to append file path to Edit link
---

So today I came across Cross Site Scripting or XSS which honestly sounds like a Counter Strike mode but is actually one of the oldest and most annoying vulnerabilities on the web. Once I understood it, I felt a little unsafe about every comment section I've ever used lol.

## What is it actually

XSS is when a website lets someone sneak their own javascript into a page, and your browser just... runs it. no questions asked, zero trust issues, straight up "sure i'll run that." The browser assumes any JavaScript that's part of the page came from the website itself, so if the site accidentally treats user input as code instead of text, it'll execute it. It's not movie hacker stuff, it's just a website not checking what a user typed before showing it to everyone else.

## Example that made it click

if a site does this to show your comment:

```javascript
element.innerHTML = userComment;
```

and someone comments:

```html
<script>alert('u got XSSed')</script>
```

now everyone who opens the page gets a random popup. swap the alert for something stealing session data or cookies that aren't protected with HttpOnly and it stops being funny real quick.

the fix is one line:

```javascript
element.textContent = userComment;
```

this makes the browser treat it as text, not code. that's genuinely most of the fix for simple cases.

## The incident that made me go "wait, WHAT"

In 2005, some guy named [Samy Kamkar](https://en.wikipedia.org/wiki/Samy_Kamkar) found a stored XSS bug on MySpace and turned it into a self replicating JavaScript worm. Anyone who viewed his profile automatically added him as a friend, got the phrase "but most of all, Samy is my hero" added to their profile, and unknowingly copied the worm to their own profile too.

result: **over 1 million infected profiles in under 20 hours.** MySpace had to shut the whole site down. he also got an FBI visit after, so respect the execution, not the outcome.

## The takeaway

Any time you build something that displays user input comments, usernames, profile bios, search results you're one careless innerHTML away from turning text into executable code. It's a tiny mistake with surprisingly big consequences and I finally understand why "never trust user input" is one of the first rules of web security.

## Try it yourself

If you want to actually *see* XSS in action, check out [The XSS Game by Google](https://xss-game.appspot.com). It walks you through real scenarios in a safe environment.
If you're curious, here are the solution for the XSS Game levels: https://pastebin.com/hv0h73eC

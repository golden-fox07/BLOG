---
title: "Managing Multiple Git Identities on One Machine"
date: 2026-02-05
# weight: 1
# aliases: ["/first"]
tags: ["Git", "configuration", "version control system", "tech"]
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

**TL;DR: Want separate Git emails per project? Just don't use `--global`.**


**The Problem:** So I ran into this situation where I needed one project folder to use my university credentials while keeping my personal Gmail for literally everything else in VS Code. Classic identity crisis, but make it Git.

Honestly thought this would be a nightmare to set up, but Git actually makes it pretty straightforward once you know the trick.

### Solution: Local vs Global Git Config

Here is the thing I wish someone had told me earlier: **stop using `--global` for everything.** I know it is tempting (one command and you are done!), but global configs apply to every single repository on your machine. Not ideal when you are trying to keep things separate.

**For personal identity  (global):**

```bash
git config --global user.name "personal username"
git config --global user.email "personal email"
```

**For uni project (local: run this inside that specific folder):**

```Bash
git config user.name "uni username"
git config user.email "uni email"
```

See the difference? No `--global` flag means the config only applies to that one repository. Problem  solved.

**Paranoid and want to verify?** I found this super helpful command to check which email was actually used for your last commit:

```bash
git show -s --format='Author: %ae%nCommitter: %ce' HEAD
```

This shows you both the author and committer email from your most recent commit. Saved me from some potential embarrassment when I wasn't sure if I had configured things correctly!

### Bonus Learning: Git Reset Flags (Proceed with Caution)

I also learned about `git reset` and honestly it is Kind of terrifying.

- **`git reset --soft HEAD~1`**: Removes your last commit but keeps all your changes staged. Perfect for those "oops, typo in the commit message" moments. Very forgiving, 10/10 would use again.
    
- **`git reset --hard HEAD~1`**: Deletes the last commit AND all your changes. Like completely GONE. Forever. No take-backs. (Yeah... never gonna try using `--hard` unless I am absolutely certain and have sacrificed the appropriate offerings to the Git gods.)
    

**Real talk:** Always double-check before using `--hard`. Your past self worked hard on that code, and your future self will definitely not appreciate having to rewrite everything at midnight.

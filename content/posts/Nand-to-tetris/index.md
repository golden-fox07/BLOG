---
title: "My Nand to Tetris Journey"
date: 2025-05-09
# weight: 1
# aliases: ["/first"]
tags: ["Nand-to-Tetris", "Coursera", "Blog","Logic-Gates"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "From NAND Gates to Computer Systems: My Nand to Tetris Journey."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "" # edit text
    appendFilePath: true # to append file path to Edit link
---

---
## Introduction

In March 2025, I signed up for the Coursera course [**From Nand to Tetris: Building a Modern Computer**](https://www.coursera.org/learn/build-a-computer) by Shimon Schocken and Noam Nisan. I thought "Why not learn how computers work from the basics?" Spoiler:- It’s not as easy as it sounds. The course promised to turn me into a computer-building wizard, and I got pretty far completing four out of six projects. 

## Logic Gates from NAND 

The course starts with a simple idea: using only the elementary NAND gate, you can construct all other logic gates necessary for a modern computer. This concept blew my mind, the idea that complex systems ultimately reduce to this simple building block.

I started by implementing basic logic gates in the [**NAND2Tetris Hardware Simulator**](https://nand2tetris.github.io/web-ide/chip/) using hdl:

- NOT gate
```
 CHIP Not {
    IN in;
    OUT out;

    PARTS:
    Nand (a = in, b = in, out = out);
 }
```
- AND gate
```
CHIP And {
    IN a, b;
    OUT out;

    PARTS:
    Nand (a = a, b = b, out = aNandb);
    Not (in = aNandb, out = out);
}
```
- OR gate
```
CHIP Or {
    IN a, b;
    OUT out;

    PARTS:
    Not (in = a, out = nota);
    Not (in = b, out = notb);
    And (a = nota, b = notb, out = and);
    Not (in = and, out = out);
}
```
- XOR gate
```
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Not (in = a, out = nota);
    Not (in = b, out = notb);
    And (a = a, b = notb, out = temp1);
    And (a = nota, b = b, out = temp2);
    Or (a = temp1, b = temp2, out = out);
}
```

**Pro Tip**: Use [**NAND Game**](https://www.nandgame.com/)! to understand how theses gates are formed using NAND. 

As It transforms theoretical concepts into visuals that make implementation much easier than it seems.

## From Gates to Chips
Once I had a grip on basic gates, it was time to get serious and build some chips. Enter the realm of multiplexers and demultiplexers. These allow you to:

- MUX (Multiplexer): Choose which input signal to use.
- DMUX (Demultiplexer): Route signals to different outputs based on selection bits.

I thought the difficulty would skyrocket when I started with the 16-bit and multi-way chips, but once I built the first 16-bit chip, the rest were a breeze, just a bit of grunt work, really.

**Arithmetic Components**

Next came the exciting part which is creating chips that can actually compute! I implemented:

- Half Adder (adding two bits)
- Full Adder (adding three bits with carry)
- Multi-bit Adder (for 16-bit )
- The ALU (Arithmetic Logic Unit) 

## From Bits to Storage

The next phase took me into the realm of computer memory, where I designed:
- Registers: Flip-flop based storage units that hold data temporarily
- RAM8: A small 8-register memory unit
- RAM64: A memory unit of 64-register
- RAM512, RAM4K, and RAM16K: Increasing memory units
- Program Counter (PC)

This hierarchy of memory components taught me how computers are organized. 

## Challenges and Limitations

While I successfully completed four projects, the two modules focused on assembly language programming were... let’s just say, less successful. I realized I’m a visual learner who prefers tools like simulators. Still, the struggle was part of the fun—sort of.

## Resources That Helped Me 
- The  NAND game (seriously, don’t skip it!)
- Course forums where students swapped war stories about their challenges (misery loves company).
- Drawing chips designs on paper before implementation

## Conclusion

While I didn't complete all six projects, the four I finished gave me a solid foundation in computer architecture that I'll build upon. 

If you're curious about how computers really work from the ground up, I highly recommend this course. It’s tough, but incredibly rewarding. After all, who wouldn’t want to say, “I built a computer from scratch with just a NAND gate”?







---
layout: post
title:  "powerline custom segment"
date:   2015-10-20 13:41:25
categories: terminal python powerline
---
[powerline]("https://github.com/powerline/powerline") is a better way to manage your prompt. It is a great replacement for the PS1 hacks I had before to include git branch name in my prompt. I also had a script to add a character to the prompt and wanted to reimplement it as a powerline segment.

To do this I copied [powerline-gitstatus]("https://github.com/jaspernbrouwer/powerline-gitstatus"), a segment for more detailed git information, and cut it down to practically nothing. The only problem I had was it expected a highlighting group with the same name as the segment to exist but the error message in the log was talking about a missing color scheme, the language was a bit confusing.

Here's the high quality end result.

![Custom segment](/assets/custom-segment.png)

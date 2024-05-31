---
title: "Job Hunting and Morale"
date: 2024-05-31
---

## Preface
I HATE business fluff, I can't, I just can't. I hate getting rejection emails, they always go on and on about "oh we had so many good candidates, which weren't you".

I'd honestly rather get ghosted than deal with all this BS, all it does is lower my morale, unless you actually include something personable about who you're rejecting its worthless, HR just clicked a button and it sent out some lifeless emails telling applicants they suck dirt.

So, I decided to do something to put a barrier between me and the machine that is trying to get a job in 2024.

## The Idea

Since I hate reading business fluff about how terrible of a applicant I am, I'll just get someone else to read it for me!
The easiest way to do this is just running all the emails contents through chatgpt, getting a summary, and telling my browser to just back out.

## The implementation

I put $5 into my chatgpt account, got an api key, and created a very simple tampermonkey extension. The workflow is as such:

1. I press a button to start the script
2. The email contents is passed to chatgpt
3. The prompt tells chatgpt to summarize the email
4. And based on the email chatgpt responds with IGNORE if the sentiment is negative
5. Finally I do a simple string search on the reply and find IGNORE
6. And then I simply tell the browser to go back

Nothing super complicated, but the amount of emotional sorrow it alleviates is immersurable.

## Future plans

Turning this into an extension rather than a simple script would be much better, also possibly having it so the scanner runs immediately once it starts reading email contents?
But that would be possibly a tad intrusive, on the off chance I'm reading some email with sensitive information, the way I have it setup to only run on a user pressing a button better

## Github Link
https://github.com/puzzledShark/Tampermonkey-Scripts/blob/main/Job%20Application%20Email%20Checker-0.1.user.js
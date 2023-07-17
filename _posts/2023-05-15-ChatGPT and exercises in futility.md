---
title: "ChatGPT and Exercises in Futility"
date: 2023-07-17
---

## Preface
I'm starting to use ChatGPT more and more, but today I had my first incursion with it blatently lying to me.

## The Problem
To start of with, I'll explain what I was trying to do.

I translate comics in my free time as a hobby, one of the steps in translating comics is that I need to erase all the text the source image, I could do this manually in photoshop but that takes effort, and its 2023 theres bound to be a tool out there.

And well there are tools for this, the one I use is called [PanelCleaner](https://github.com/VoxelCubes/PanelCleaner).
It has many options on what is outputted but effectively it outputs plain images.
Below you can see what the difference between a cleaned, and uncleaned image is.

![Difference between cleaned and unclean image](/blogBoi/docs/assets/images/cleaned.gif)

Now ideally when I'm translating comics I'd have the source text in photoshop, with the cleaned image to overlay once I'm done translating but this is a lot of busywork when theres 50 pages to be translated.

This is all too needlessly busy for me, having to load 2 images onto the same workspace, laying out everything, and then repeating this 50 times.

Ideally I would tell panelcleaner to just export a PSD, with 2 layers, one with the mask, and one with the source image.

Now here is where I ran into my problem.

## The chatGPT Problem

I'm still relatively inexperienced with python, I know its on my resume but I'm still pretty green with it.
So I go to chatGPT a lot to clarify things for me.

I had told my problem to it, and it mentioned a library called PSD-Tools, now, in my hubris, I assumed the best, it had even given me an example close to what I wanted, thus I got to work.

## The solution

Since I was starting out, I had considered doing a dry and dirty "hack" of a solution where I would hijack the saving process and just proceed with my logic, but NO

JUST NO, I just HAD to understand all the code, run around learning how python works in relation to the cache, and the various quirks of the libraries the original author had used, and implement a solution that looked virtually "stock" to the application itself.

This took me about 5 hours mostly because I forgot to uninstall the panelcleaner module I had already installed, thus none of my code was actually getting run. But past this, I finally got to the step of implementing the rewrite of saving the image step.

## The futility

I took the code that chatGPT had given me earlier in the day, and pasted it in, making various changes where they made sense, and... nothing.

Well not nothing, it crashed lol.

Why? Why did it not work? Was it my implementation?

And finally, I went to the documentation.

Confusion runs across my face... why is there no example outlining how to create a PSD from scratch...

I go to chatGPT and ask it straight, "How do I create a PSD with PSD-Tools"

and it lays out that is not possible.

The ChatGPT from earlier in the day, it had "lied" to me, obviously the fault still lies on me, but still.

## Alternatives

To be frank, there are none, at least there are none if you want to continue to using photoshop.

Those alternatives being the image formats:
TIFF, and XCF

photoshop either refuses to work with them, or does "unintended" behaviour.

## Conclusion

1. Always look up the tools you're intending on using before wasting time
2. Don't trust chatGPT at step one, if you're not going to be using that logic till a later step
3. Always either familiarize yourself with libraries you intend on using, or at least make a dirty hack to see if something will work or not
---
title: "Planning and Development Versus Real World Scenerios"
date: 2024-05-30
---

## Preface
In development, sometimes it really helps to really put to test a solution to find out what the best solutions are. For example, I followed a poster on VK(russian facebook), they posted Linux ISO frequently, and I'd come on by occasionally and download interesting new ones. Everytime I'd come back to the page they'd have new Linux ISOs for me to consider downloading. The page itself has a lot of fluff that I don't need, all I needed was The Linux ISOs name, its proported features, and the picture used for the ISO.

## Goals

1. Get rid off all the fluff from the page that don't contribute to my task of figuring out which ISOs to download
2. Create a list of download links that I can feed into a download manager
3. Create a list of ISOs I've already downloaded, this is neccessary because I don't want to download an ISO again if I've already downloaded it once

To solve this I could write a web scrapper in node.js but that seems pretty excessive for a task I'm only doing maybe twice a month. Alternatively, websites are starting to REALLY crack down on bots and I don't want to have to deal with their anti-bot measures for such a simple task.

So to make this as simple as possible, a tampermonkey script would be the easiest.

## The first implementation

To start out with, I moved to solve the basic issues first.

The first implementation, worked as such

1. The user would scroll the page a certain amount (The page itself was infinite scroll, so I need to load as much data in as neccessary)
2. The user would initiate the scrapper, this was implement as hovering button in the lower right of the page
3. The script then pulls all data from every post into a simple UI which was basically just a list
4. The user is able click on these newly formed posts
5. Once the user is satisfied with the amount of posts they've marked, they can press a new button I made, called "copy download urls" and it will push the list of download urls to the users clipboard for a download manager
6. The script takes note of the post name, and saves it to a local DB so that the next time this script runs, it marks posts as "downloaded" so the user knows not to redownload those.

The script as is, works fine. Implementing the UX rebuilder was easy and neccessary.
Saving the post titles is contenious but its useful, but somewhat complicated.

## Complaints

As outlined in step 1 of the first implementation, the user has to scroll to a certain amount themselves, the user themselves does not know what was the last post that was downloaded, so the basic user flow was scrolling way too much and assuming it'd catch everything the user has not checked out yet.

Obviously this is not optimal.

Lazy Solution: 

- Posts are marked with a date
- The User is most likely going to explore all posts that are between "last date accessed" and "current date"
- Thus if I remind the user of the last time they executed a download url command they'd know how far to scroll down before stopping

## Implementation 2

I literally just logged the date they last executed the command, saved that to the local DB and added lazily added the last extract date to the "Extract Data(DATE ##)" button

## Insights

This cutdown on the amount of scrolling the user had to do substantially, but since script has access to the last date the user executed the script, and the dates on the posts themselves why not just automate the scrolling itself?

## Implementation 3

In a loop, initiate scroll to bottom in js till the posts are "<date last accessed"

## Insights

Okay now the user can press the Extract data button and do anything else until it finishes scrolling to the date last accessed.

Hmm... The user is ONLY interested in new ISO's and cares nothing about ISOs from before the last access...

Wait... Then the system in which ISO's are marked and saved in the database extremely unneccessary since:

- It marks already downloaded files
- Already downloaded files would only exist in list that would be "<date last accessed"


## Final thoughts

Actually using an appication yourself can really reveal things about the applications being created, and sometimes a simpler solution is really all thats needed. I started out with an idea, and never strayed from it thus creating extra work for no reason

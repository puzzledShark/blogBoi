---
title: "Job: Airline Caterer Data Entry Automater"
date: 2023-03-20
---

## The Job

A year before covid took over the world I got a job at an Airliner Caterer while I dealt with a few issues in life. The job basically comprised of coming into work, doing various menial tasks, but the main one was to double check the meal orders for flights heading out that day. It was pretty basic stuff.

## Meal Order Checker

Now as I outlined, my job was to get information about meal orders from our main client(the airliner) and cross reference it with our systems to make sure they were the same.

For example, flight XX123 has 3 GFMLs and 10 VGMLs in the data sent from the client, is that correctly outlined in our systems? If not rectify it. The system itself did load the data from the client at timed intervals but sometimes things would be missed.

As I was being taught the role I outlined many huge inefficencies in the processes.

The biggest one for me was the amount of extra steps that had to be taken to get a count of meals on flights.

The general workflow for getting meal order counts on the system worked as such:

1. Input flight search field on the flight search page

2. Find flight

3. Click into flight to make sure its a valid flight

4. Go to meal order page to double check that its not null

5. Return to the flight search page

6. Next to the flight, click "request report"

7. Wait 50 seconds while the system generates a report

8. Open Report and confirm the meal totals

9. If totals are off go back into the flight and update totals

Within a day I would have been expected to go about this around 200-300 times. Now to be a little more specific, inside the flight, the meal order page would look something like this:

![Example meal order page](/blogBoi/docs/assets/images/MealChecker.png)

## Fast Tallies

This is a small snippet but effectively a flight could have upwards of hundreds of meals. You could technically count them manually but this introduces human error, and wastes alot of time. If we could make this step even a little faster then we'd be saving effectively 50s * 200 = 10,000s or nearly 3 hours in wait time at minimum.

To speed up this step I used some of my knowledge making chrome extensions I was able to make a simple extension that would detect that it was on the flight meal order page and simply tally the numbers, saving time and effort from asking the main server to generate reports.

![Example fast tallies](/blogBoi/docs/assets/images/FastTallies.png)

It looked rough but since this was my second day at the job I wanted it to work to save myself time. I was also able to share this with my peers within the office to help speed up their roles.

## Flight Meal Order Checker Automater Preface

After speeding up that use case, I wasn't really satisfied with merely manually checking flights. I had prior experience with making webscrappers from a previous pet project of mine which involved scrapping websites for images and hosting a website locally to display them in a specific fashion.

For this automater my goal was to automate the "checking" of flights, not neccessarily the full process of checking/updating. If I could automate the process of checking then the user could essentially act as a secondary checker to ensure everything was correct.

My previous experience was in Nodejs using a package called Nightmare.js, Nightmare.js effectively is just built on top of electron which in itself is just chromium. Thus to the intranet itself I was just another web browser user.

## Flight Meal Order Checker Automater V1

For version 1 I was mainly working on making sure it worked without running into any errors, but embrassing as it is to say, the implementation was very rudimentary. For the webscrapper to know what steps to take I had hardcoded it to do actions based to TIME not events, essentially it would type in to the search field, press enter, and then I hardcoded in a wait of X amount of seconds before it would move on. I made sure to leave in a very long delay to ensure it worked, and it did definitely work but obviously this wasn't a good solution.

## Flight Meal Order Checker Automater V2

At this point in the automater all the functionality that I wanted of it was done and created, so it was time to polish it up a bit.

Usability of the automater was abysmal, presently all input/output to the user was done through the command line, not really user friendly these days even if it was working. So for V2 I focused in on getting a usable GUI.

![Example of the GUI](/blogBoi/docs/assets/images/CXPAutomaterGUI.png)

Now, I won't fluff this up, I am NOT an front end programmer, making it pretty was 100% not my priority, and it shows. This is actually a picture of the final GUI, the inital one was literally just raw HTML with buttons and no CSS. But at the end of the day, the functionality worked.

## Flight Meal Order Checker Automater V3

With usablity improved I moved ontop improving its performance, at this point the web scrapper still worked via delays for EVERY single action. To fix this I sat down, and actually read the documentation for nightmare properly, and implemented .wait events based on whether elements on the page existed or not, or just telling the automater to wait for "page ready". With this the web scrapper finished all its work within 10 or so minutes. Doing all this manually would have taken upwards of 2 hours previously.

[![Youtube video of the automater in action](https://img.youtube.com/vi/JwE5bMYTb-w/0.jpg)](https://youtu.be/JwE5bMYTb-w)

Above is a video of the webscrapper/automater in action.

## Incidents

There was one incident that happened while I was on the job, just to refresh, my job title was essentially just "Data Entry" so I wasn't really expected to make all these programs to get my job done, but I had the go ahead by my 3 supervisors so I was allowed to do whatever as long as the work got done.

My job was to essentially double check all orders for the day. One of those days though, the client had sent the last minute order changes 1 hours late, with the way our system is setup, outdated data was already seeded into the system by the time the last minute order changes actually came in. Thus if this was not retified in system. With a 1 hour lead time to solve the issue for possibly 300 flights it was thrust upon me to "DO SOMETHING" and essentially I did just that, as a mere "Data Entry" drone I wasn't really allowed to run any commands directly on the system itself. Luckily enough I was already familiar with the format the data the client sent us daily, so with a few quick changes to the my automaters codebase I was able to set it up to scan all 300 flights urgently within 15 minutes, and fix the issue in time.

## Other automaters

Now on the job I did make other automaters too, either for functions I myself needed, or what my peers desired.

## Closing Thoughts

This job is the reason why I got interested in automaters, the joy of setting up something intricate and just seeing it orchestrate everything is a great feeling. Just seeing everything fall into place.

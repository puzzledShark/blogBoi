---
title: "Indeed Tampermonkey extension"
date: 2023-04-03
---

## What is the purpose for this extension

So I'm presently on the job hunt unforunately, so I apply for lots of jobs. For this I like collecting information about the job if I need to follow up on it.

For this I presently collect all the information of the job on a google sheet, but copy pasting all that information is a huge waste of time, I considered using google sheets built in =importxml but that function fails when the website has javascript.... which is basically all websites nowadays.

![Indeed information](/blogBoi/docs/assets/images/Indeed1.png)

The things I want from the indeed listings are:

- Job Title
- Company Name
- Location
- job url
- the current date(implying that I applied to that job that day)

## The Solution

I'm pretty used to injecting javascript code into websites, from my previous airliner job, and from my small annoyances with some websites. Thus the solution I came up with was to simply create a tampermonkey script, inject a button onto the page and tell it to extract information from the page, then simply send it to my clipboard.

All this is a very simple process for a script, the manipulation of the clipboard alone is a built in function of tampermonkey.

    var copyFunction = document.createElement ('div');
    copyFunction.innerHTML = '<button id="myCopyButton" type="button">'
    + 'Click Here to Copy Page Information'
    ;

    copyFunction.setAttribute ('id', 'myContainer');
    document.querySelector('#jobsearch-ViewJobButtons-container').appendChild(copyFunction);

    document.getElementById ("myCopyButton").addEventListener (
        "click", ButtonClickAction, false
        );

    function ButtonClickAction (event) {
        var title = document.querySelector(".icl-u-xs-mb--xs > span:nth-child(1)").innerText;
        var company = document.querySelector(".css-1h46us2 > div:nth-child(2) > div:nth-child(1) > a:nth-child(1)").innerText;
        var location = document.querySelector("div.css-6z8o9s:nth-child(2) > div:nth-child(1)").innerText;
        var url = window.location;
        var paste = url + "\t" + title + "\t" + company + "\t" + location + "\t=TODAY()";
        GM.setClipboard(paste);
    }

I fairly simply created a button, appended it to the page like this:

![Indeed information](/blogBoi/docs/assets/images/Indeed3.png)

Added a click action event, extracted all the information, then sent it to the clipboard:

(THIS WOULD BE THE URL)	Software Developer Internship	Intelliware Development Inc.	Toronto, ON	=TODAY()

Pasting this into google sheets gives us:

![Indeed information](/blogBoi/docs/assets/images/Indeed2.png)

## Closing notes

I could obviously make it look nicer, but it serves my purposes and thats all that matters. Since I made this extension for my purposes in making a "data is beautiful" post I hope that my job search is short lol.

---
layout:     post
title:      Wrestling a University Schedule
date:       2014-01-10
summary:    Improving the schedule building experiance with AngularJS and Python
categories: 
---

Crafting the ideal class schedule is an aggravating task.  Ok, maybe it's less aggravating if you're impressively proactive and organized enough to embark on this task the day registration opens.  But the truth is, most people don't do this.  Most people, including myself, ponder which classes they should take right up until the last few weeks before classes start.

At the University of Alberta the online system for picking these courses is called *BearTracks*.  It's a good name for a website - *bears* are our mascot, and *tracks* fits the image of the University journey.  But most of our compliments to BearTracks end there.

It has a confusing side-navbar with all these tabs and buttons that sometimes direct to the expected page, but sometimes lead confusingly astray.  Even the most experianced BearTrackers get lost - it's kind of like [vertically centering a div](http://stackoverflow.com/questions/396145/how-to-vertically-center-a-div-for-all-browsers).  Beartracks is certainly a traumatizing experiance for many first years.

This summer I was watching a talk given by John Resig, the creator of jQuery.  He was talking about some side projects he did in his undergrad at the University of Rochester, and mentioned how he worked on an [improved schedule builder](http://schedule.csh.rit.edu/) for his school.  I was intrigued by the idea. 

So I talked it over with one of my friends, [Ross Anderson](https://github.com/rosshamish), and we decided to make a schedule builder for UAlberta.  Our focus is **speed, usability, and accuracy**.  I am focusing on the front-end, while Ross is building the back-end.  We chose the AngularJS framework for the front-end, and Python on the backend.  

It was my first time using [Angular](http://briantford.com/blog/huuuuuge-angular-apps) so the learning curve has been treacherous at times, but I'm getting there.  And as Ross researched scheduling algorithms, he quickly found that it's commonly used as an example of an [NP-complete problem](http://stackoverflow.com/questions/1857244/np-vs-np-complete-vs-np-hard-what-does-it-all-mean).  But these challenges are what has made it exciting to work on. During the fall months we found our groove, had some solid commit streaks, and even tagged a version 0.0.1.  

Fall registration opens up in the spring and we hope to have a version 1.0 ready for that time.  

If we can save one first year from crying after trying to wrangle a schedule together by hand or using BearTracks, we've done what we wanted to do.




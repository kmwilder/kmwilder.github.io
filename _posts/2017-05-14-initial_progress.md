---
layout: post
title: Initial Progress
date: 2017-05-14
tags: [PROJECT_1]
---

I'm happy to report some surprising levels of progress over the past month or
so full of weekends. I'm not sure where the credit lies: Sarah's multiple suggestions that
we work on it together, the dog being old enough to not need constant attention, work settling
down enough to leave some non-jellied brain for off-hours, or WoW being a bad, dead game.

Anyway, the point of this whole exercise is to record stuff I learn on the path to releasing 
(maybe production-worthy?) SW that's good enough to not be laughed at. We've basically gotten a
shallow prototype up-and-running, via some basic tutorials:

**[Java+Tomcat+Maven](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/basic_app_embedded_tomcat/basic_app-tomcat-embedded.html)**

The last time I touched any kind of web server, Java, JSP, HTML, CSS, or SQL was back in 2012,
when I took CS108 at Stanford. I vaguely recalled it involving Tomcat, and I sorta
recognized the word "Servlet", but no useful knowledge survived the passage of time. This
was a pretty good re-introduction.

**[Java interactions w/ MySQL](http://stackoverflow.com/questions/2839321/connect-java-to-a-mysql-database)**

For ASIC design problems, it usually feels like consulting Google for answers will do nothing but waste
your time and try your patience as you sift through misleading, poorly constructed, and probably erroneous
answers (that usually aren't for the question you asked anyway.) Even problems with industry standard tools
\**shakes fist at Synopsys*\* send me into a pit of despair after more than 10 minutes of debug.

For SW problems, I'm totally impressed with how much information is out there, and how easy it is to find it.
It really feels like all the gruntwork needing to be done is a search or two away from code that's pretty 
representative of the final result -- and pretty much works (or, at least, provides good insight into how 
it *should* work.)

I know it's a running gag about how Google -> StackOverflow is an essential part of the SW dev's
workflow, but damn, it's effective. Not that what I wrote is robust/scalable/good, but it got me from zero to
a working CRUD prototype in under 48 hours of work, so that's great.

**[HTML5 MediaRecorder](https://developers.google.com/web/updates/2016/01/mediarecorder)**

I suppose I should be grateful that this kind of stuff exists, natively, in browsers. I think I have
audio transmissions working properly and efficiently, all under 150 lines of JavaScript (150 lines too many, IMO)
and a few \<audio\> tags. Thanks, browsers.

Anyway, this is probably peak optimism for me. The problem space went from totally unknowable "web app magic",
to a mostly-complete tiny CRUD app. I still have to clean stuff up and add some features, no big deal,
but then I've gotta get it running:
* on a cloud
* securely 
* robustly

Shouldn't be too hard, right?
---
layout: post
title: "What project to choose?"
description: ""
category: 
tags: [fp, c#, f#]
---
{% include JB/setup %}
<p>I've decided to convert an existing, non-trivial C# project into F#. So now I have to choose one. What am I looking for? I need something not too difficult to understand, as I want to be focusing on the porting and refactoring process, not on understanding some super-clever project. Also it needs to be not too easy, as there wouldn't be enough of a challenge. So it needs to be somewhere in the Goldilocks zone of complexity.</p>
<p>It seems a good idea to be a real project that people are using for something, this adds a bit of interest to me as I am coding. I've never taken part in an open source project, and there is a bit of mystery to me about just how these projects take off. I should be able to learn a bit in this direction by getting to know the internals of a project.</p>
<p>It needs to be relatively well written, so I don' scratch my eyes out reading through code that is oddly formatted or badly expressed in some way.</p>
<p>I spent a good deal of time trawling through github "trending c# projects", the projects of busy c# developers. I was close to picking <a href="https://github.com/SirCmpwn/TrueCraft">TrueCraft</a> since I thought it might be nice to do something gamey, where the results are satisfyingly visual. Then I noticed that it uses Mono. I don't have anything against the Mono, but I don't think it'll play well with F#.</p>
<p>Eventually I settled on <a href="http://dev.origodb.com/">OrigoDB</a>. I won't go into too much detail about what this is, as you can find better explanations on their site. It's an in-memory database. At first my reaction was "What, like a list?", but no it's smarter than that. It's a journal based in memory database, which can be persisted in various ways but holds all the data in memory when it's running. Also it's does lots of performance yadda yadda yadda. Some of the claims on the website look a little dramatic :"the traditional RDMBS architecture is obsolete"? - I'm not sure I buy that one, but nevertheless this is a serious project. People use it for stuff, judging by some related projects in github.<p>
<p>I'm going to be able to learn a bit about this kind of DB while I am working on it. Also it should throw me a few non-trivial problems along the way.</p> 
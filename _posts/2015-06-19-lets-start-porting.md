---
layout: post
title: "Let's start porting!"
description: ""
category:
tags: [f#, c#, fp]
---
{% include JB/setup %}
So, I have my project to convert. Now what?

I will start by finding what looks like the easiest part of the project to convert. Without editing the existing c# code, I can create a 'shadow' F# project, and start implementing replacements, type by type, until I am ready to replace a whole project.

Looking at the OrigoDB project we've got:

* OrigoDB.Benchmark - that sounds a bit scary, I'll leave it
* OrigoDB.Core - looks like the important bit
* OrigoDB.Test.MSTest - a small number of tests, presumably the ones they couldn't get to work in NUnit
* OrigoDB.Test.NUnit - the bulk of the tests, with (to me) a slightly quirky organisation, lacking subfolders. I would normally arrange the folders in my test project to reflect the subfolder (and namespaces) of the project it's testing.

So there isn't a small project I can easily replace, so I will have to settle for replacing things one namespace at a time.

Without looking too deeply into the project, I've found a folder called 'Utilities'. That seems like it's probably going to contain a few classes that are pretty self contained and not too difficult to make a start on. Sidenote: I'm always very dubious when I see a module of code called "Utilities" or "Helpers". It's an example of what Bob Martin calls "Magnet Code". If you give something a name like that, the next coder after you, if she has to choose where to put her class and it isn't obvious, may end up putting it in your Utilities area. Over time it grows into a dump of unrelated code.

I've made a new F sharp 'library' project, which sounds like it's the equivalent of a class library. I don't know what this _Script.fsx_ is there for, I won't let it it worry me.

![project hierarchy]({{site.baseurl}}/assets/images/project-setup.png)

So what's the easiest thing I can port? How about this little beauty?

{% highlight c# %}
namespace OrigoDB.Core.Utilities
{
    public enum CompressionAlgorithm
    {
        Gzip,
        Deflate,
        Custom
    }
}
{% endhighlight %}
That's pretty easy to convert to F#. In fact it looks a little more elegant already!
{% highlight fsharp %}
namespace OrigoDB.CoreFSharp.Utilities

type CompressionAlogrithm = Gzip | Deflate | Custom
{% endhighlight %}

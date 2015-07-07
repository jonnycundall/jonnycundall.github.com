---
layout: post
title: "I thought this would be easier"
description: ""
category:
tags: []
---
{% include JB/setup %}
Ok, next tiny bit of code! It'll be just as easy as the last bit, won't it?

{% highlight c# %}
namespace OrigoDB.Core.Utilities
{
    public static class ByteArrayExtensions
	{

	    public static ICompressor CompressionAlgorithm = new DeflateStreamCompressor();

		public static bool EqualsEx(this byte[] a1, byte[] a2)
		{
			return a1.Length == a2.Length
                && Enumerable.Range(0, a1.Length).AsParallel().All(i => a1[i] == a2[i]);
		}


        public static byte[] Compress(this byte[] data)
        {
            return CompressionAlgorithm.Compress(data);
        }

        public static byte[] Decompress(this byte[] data)
        {
            return CompressionAlgorithm.Decompress(data);
        }
	}
}
{% endhighlight %}
So this is a class created to give a few helpful extension methods to byte[]. I did wonder whether F# would actually have extension methods, since they are a bit of syntactical sugar, but they do. I think in general they have put any feature that c# developers are used to into f#, to keep us happy, even if it doesn't make that much sense to have them in a functional language. Not that I'm saying they don't make sense in a functional language. I don't even know that much yet.

So I tried. I tried and failed. Not only do extension methods exist in f#, you can add them to generic arrays, see this answer on [stack overflow]{http://stackoverflow.com/a/11849361}. To do that you have do this crazy syntax:
{% highlight f# %}
type 'a ``[]`` with
  member x.GetOrDefault(n) =
    if x.Length > n then x.[n]
    else Unchecked.defaultof<'a>
{% endhighlight %}
So I was trying something like this:
{% highlight f# %}
type 'byte``[]`` with
    member this.Compress =
        let comp = new DeflateStreamCompressor()
        comp.Compress(this)
{% endhighlight %}
Unfortunately this gives me the error "this type parameter has been used in a way that constrains it to always be byte". And further investigation tells me that you can't extend a typed array in f#. So they don't give us all the sugar we were expecting!

So I'll settle for now with just some static helper methods, I'll work out what to do with these later:
{% highlight f# %}
module Extensions

open OrigoDB.Core.Compression
open System.Linq

type ByteArrayExtensions =
    static member Compress(a :byte[]) =
        let comp = new DeflateStreamCompressor()
        comp.Compress(a)
    static member EqualsEx(a1 : byte[], a2 : byte[]) =
        a1.Length = a2.Length && ParallelEnumerable.Range(0, a1.Length).All(fun i -> a1.[i] = a2.[i])

{% endhighlight %}

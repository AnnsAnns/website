+++
author = "tomGER"
title = "Go Adventures #1: Coming from Python to Go"
date = "2020-06-15"
description = "Why would you want to learn Go, what are the differences coming from Python and more."
tags = [
    "go",
    "python"
]
+++

{{< figure src="https://i.imgur.com/5NDraTA.jpg" height="80%" width="80%" class="text-center">}}

In this little mini-series of blog posts I'm going to showcase the problems I faced learning Go and the cool tricks and tips I accumulated while trying to solve them. In this first blog post, I'm going to give a small introduction into the world of Go from a Python developers perspective, which means that some general knowledge about Python programming is required here.  
The next blog posts are going to be purely focused on problems inside of Go and are thus for people that are already familiar with Go.

Python is by far my favourite language. You can achieve so much with extremely simple code and because of the widespread usage nearly everything is possible, however, the high-level bytecode-compiled nature of Python can also be a downside in certain cases.

And here is where Go comes into play. Go is extremely fast with speeds close to pure C code, while being one of the most modern programming languages I have ever seen.  

If we look at some speed comparisons between Go and Python we see increases in execution speeds of up to 4200% while having a considerably lower memory usage. (For more details, read through the [amazing comparisons](https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/go-python3.html) done by the benchmarksgame team)

And thus I decided that I'd play around with Go in the later half of May, which was a surprisingly easy journey. To my surprise Go has an extremely interactive tutorial called "The Tour to Go", which you can easily go through within one or two hours: https://tour.Go.org/welcome/1.  

The first thing major difference is that everything is a package. You don't execute single files or have one main file. The entire design of Go is extremely modular, even the print() command is in it's own module, however one thing that you never worry about in Python, is at it's strongest in Go, and that is:

## **Types and Type Safety**

{{< figure src="https://i.imgur.com/IKMdow1.png" height="40%" width="40%" class="text-center" caption="*Javascript, the most infamous example of type safety*">}}

Python is such a blessing when it comes to easy variable declarations, as a programmer you normally only have 2 different types, either your variable is a string or an integer and you can easily convert between them through the str() or int() functions.   
C/C++ on the other hand has a lot of different type, which allows you to constrain the memory footprint of your program while also causing major type-safety. Well, now think of the type-safety of C/C++ and double it.  
Go is extremely type-safe by design, as even the type-safety of C/C++ wasn't enough for some certain use-cases. Thus every addition, subtraction, multiplication or division between two variables needs to be tightly controlled by you.  
Coming from Python this was quite confusing at first, not only did I need to worry about declaring my variables but every interaction between variables had to be written in a way that would cause no issues between the different types, which was esp. annoying when I tried to create my own CHIP8 emulator, though I must admit that this extreme type-safety is a good thing in the long run. If you ever manage to send some conversion bug onto your production server, I'll be extremely surprised.  
There are also some types that Python doesn't support by default, such as complex numbers, however, I'm not qualified to talk about them, so I'll just mention it as a little side-note for people that have any use for them.

## **OnlyFors.com and Switch Cases**

Since Go has a similar approach to Python's "complexity through simplicity", Go doesn't have any while-loops, instead it uses for-loops for everything, which I honestly found good, the way the implement for-loops, there is nearly no reason to add while-loops. I only wanted to talk about it so I could make the joke in the headline.  

Something that I was missing for a very long time in Python was switch cases, seeing all my C/C++ friends with their amazing switch cases, it was really annoying to not have something similar to it.  
Later on I started using dictionaries as my Python-ish replacement for switch cases but simple switch cases can make your life so much easier. From what I've heard, Go even has better switch cases than C/C++, which is nice to hear.

## **Go doesn't like Json**

Python has amazing Json support, it's like Json was made for Python's dictionaries. It's so easy to interact with Json that it has become my standard way to save and serve anything I do with Python.  
However, as I learned when I tried to port my discord bot that interacts with a Nintendo Switch error code API that I heavily based on Python's dictionary format, Go freaking sucks when it comes to Json.  

I'll likely make a JSON tutorial for Go in the future but the TL;DR of it is that the design of recursive json datasets based on Python dictionaries with a lot of sub-dictionaries doesn't play well with Go. A simple five line code would have turned into a huge function inside of Go just to parse anything from that API.  
Luckily I'm not the only person that realized how annoying Json parsing is in Go and after some digging and testing, I found [GJson](https://github.com/tidwall/gjson), which makes *reading* Json so much easier. Modifying Json is still another topic but I tried to ignore that for now.

## **Python's infamous Global Interpreter Lock and Discord**

{{< figure src="https://i.imgur.com/QElXAXw.jpg" height="40%" width="40%" class="text-center">}}

Something that some people might find controversial is that I find discord.py extremely annoying to work with. This might come from the fact that I just dislike how async or threaded Python works but it might also be that I just don't like the way it was built. Either way, even though I have created or taken part in the creation of a lot of bots, including errBot, Robocop, Komet and a lot more and even use discord.py on some subreddits to provide moderators easy access to data, I never became friends with discord.py.

Go has quite the different handling of threads, it's "Goroutines" are extremely easy to use and are natively built into the core of Go, compared to Python which has the so called **GIL**, which is extremely problematic for threading. The GIL is the *Global Interpreter Lock* and causes every single thread to fight for control over the Python interpreter. This is the biggest bottleneck for every threaded Python program and makes Python extremely hard to scale. At the time Python was written the concept of threads was far from reality so this isn't some malicious or bad decision by the Python team, it's just a relict of it's time.  
Go is extremely new, Go doesn't have to deal with this design problem because it is newer than threads, which also makes it a thousand times more scaleable than Python.

## Conclusion

At the start of this journey I thought that I'd only want to learn the basic Go features but the more I got into Go, the more I appreciated the design of it. It somehow caused me to get extremely interested in something that isn't Python, which is extremely surprising. There is still a lot of stuff that I want to try out before I feel like my Go knowledge is on-par with Python but I see a lot of potential in this language.  

There is still a lot more stuff that I want to talk about in much greater detail but there is a reason companies such as Netflix, Twitch, Twitter and PayPal decided to switch a lot of their infrastructure to Go.
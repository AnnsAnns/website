+++
author = "tomGER"
title = "How to cross-compile Rust from WSL Linux to Windows"
date = "2021-02-25"
description = "A small blog post showcasing easy ways to cross-compile Rust from WSL Linux (Arch) to Windows"
tags = [
    "rust",
    "short"
]
images = ["logo.png"]
+++

{{< figure src="logo.png" alt="🦀🦀🦀" height="50%" width="50%" class="text-center">}}

Okay, look, I have fallen down the rabbit hole when it comes to Rust. At first I didn't expect to use the language to a great extend but the more I use it, the more I like it. Besides the great compiler and all the other benefits Rust comes with, the tooling is also amazing. There are so many useful community and first-party tools for many boilerplate problems that keep you from working efficiently, from easy wasm support to embedded software.

In this (hopefully) short blogpost in the "Heck, I wish I knew this earlier" series, I want to showcase some really easy ways to cross-compile Rust projects to different architectures.

### WSL

WSL is extremely useful and Microsoft is doing one great job when it comes to their ["Embrace, extend, and extinguish"](https://en.wikipedia.org/wiki/Embrace,_extend,_and_extinguish) tactic. I love the fact that I can do all my work on the far greater platform for developers (Linux) while still running the buggy mess that is Windows 10 for all the software that doesn't really work well on Linux.

{{< figure src="neofetch.png" alt="Neofetch showing that I run Arch" height="70%" width="70%" class="text-center">}}

And as some readers might already know, "btw I use Arch". Which means that even my WSL distribution is Arch, thanks to [the awesome community of Arch](https://github.com/yuk7/ArchWSL).

While WSL 1 was quite mediocre, WSL 2 offers the full Linux experience, allowing me to do everything from desktop environments through server hosting. Sadly, WSL2 still only support software rendering, which is a major bottleneck for all applications that do more than a simple GUI, and even then, some GUIs don't even support software rendering.

Microsoft is even working on a solution to this, but it honestly looks quite questionable and is still not live so we couldn't even use it if we wanted to. There is a solution to this however, just cross-compile whatever you need to Windows and run it on Windows and there is a myriad of ways to do that. In this blog post I'll just quickly talk about 3 solutions that I went through with the most important one being ["Cross"](https://github.com/rust-embedded/cross) for rust.

### Lvl. 5, Crook: Just compile *on Windows*

I also like to call this the *"You want to suffer"* method. Even though this method has the most documentation, it kinda defeats the point. Why would you need a WSL instance when using the inferior Windows toolchain.

Anyways, the setup is basically just three *"simple"* steps.

1. Install half a terrabyte of Microsoft toolchains + Microsoft Visual Studio from here: https://visualstudio.microsoft.com/visual-cpp-build-tools/
    - To be more exact, you only need the "Visual Studio C++ Build tools" but naturally, you can't simply type "pacman -S" like on Arch.
2. Install [Rustup](https://www.rust-lang.org/tools/install)
    - As to be expected, Rust makes everything really really easy for you :)
3. Regret your life choices because you decided to use Windows as your programming environment

### Lvl. 50, Boss: Use Mingw64 to compile from Linux to Windows

Honestly, people have made way better tutorials for Mingw64 Linux and I don't feel like investing the time into explaining something I don't even recommend.

If you actually want to use Mingw64 instead of using Cross, follow the Arch Wiki: https://wiki.archlinux.org/index.php/Rust#Windows

### Lvl. 100, Hackerman: Use [Cross](https://github.com/rust-embedded/cross)

My god, I wish I knew this existed earlier. [Cross](https://github.com/rust-embedded/cross) is a project by the [Rust Embedded Tooling Team](https://github.com/rust-embedded/wg#the-tools-team) which makes cross-compiling of Rust absolutely painless. I have never had an easier time cross-compiling anything, it's literally a single line of work and absolutely astonishing work by the Rust Embedded Tooling Team.

##### Setup on Linux:

1. Have a working version of Rustup
    - ```pacman -S rustup```
2. Install either Docker or Podman
    - ```pacman -S podman```
3. Lastly, install cross
    - ```cargo install cross```

##### Setup on WSL:

1. Have a working version of Rustup
    - ```pacman -S rustup```
2. Ensure that you installed [Docker **on Windows**](https://www.docker.com/get-started)
    - Docker on Windows utilizes WSL2 and hijacks all docker calls, so you can't simple install Docker from within Arch afaik
3. Ensure that Docker for Windows lists your WSL2 instance in Settings>Resources>WSL Integration
4. Lastly, install cross
    - ```cargo install cross```

After this, you can simple use Cross to compile to your specified target. In our case we want to compile to x86_64 Windows, which means simple typing ```cross build --target x86_64-pc-windows-gnu```. After that, you should have ```<project_name>.exe``` in ```target\x86_64-pc-windows-gnu\debug```.

WSL even allows you to simple call the exe from your Subsystem's shell, in which case it will execute it natively from Windows. Success, you just cross-compiled to Windows from a Linux WSL instance in a single command.

### Conclusion

Rust is awesome, praise Rust.

In all seriousness though, such excellent tooling is beyond expectable for a language that is still so young and new. I hope I managed to keep this blog post relatively short and thank you for taking the time out of your day just to read it.

If you have any questions (or want to follow me on social media), feel free to visit my [Twitter](https://www.twitter.com/_tomGER).

I also made some major changes to my blog, majorly increasing speed, SEO, accessibility and more. If you noticed anything breaking, I'd be happy to fix it.
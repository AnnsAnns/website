+++
author = "tomGER"
title = "Rust, Risc-V and embedded systems"
date = "2021-02-11"
description = "First Steps: The Sipeed Longan Nano Risc-V microcontroller and Rust"
tags = [
    "rust",
    "embedded-systems"
]
+++

Guess what, I still exist. In the typical developer fashion I wrote a single blog post and then abandoned the whole site for nearly a year. In that time I *mostly* mastered Golang and did a lot of other things that I really want to talk about sooner or later. For now I'm going to try to write about my journey with microcontrollers in smaller more common blog posts instead.

Anyways, recently I bought a Risc-V development board, the Sipeed Longan Nano to be exact. Risc-V has always been something I just wanted to work on sooner or later, it's one of the few CPU architectures that fascinate me and I strongly believe that sooner or later it'll run most of our devices. The open source and modular nature of it makes it a wonderful contender for IoT and anything that needs to be fast, cheap and small.

{{< figure src="https://cdn.discordapp.com/attachments/677603781554470912/809436168528855100/IMG_20210211_154847930.jpg" alt="*The Longan Nano, Raspberry Pi Pico and a pen for scale.*" height="50%" width="50%" class="text-center" caption="*The Longan Nano, Raspberry Pi Pico and a pen for scale.*">}}

The Longan Nano in itself is actually quite amazing for the price. It offers 128 KB of Flash, 32 KB of SRAM and a lot of different peripherals while running at a *blazing fast* 32.768KHz [Low Spec Mode] and 8MHz at it's highest speed ;) Yes, those specs aren't that impressive compared to the Pico given that both share the same pricetag but the Longan Nano also comes with a MicroSD reader, USB-C and a 160x80 IPS RGB LCD which I'd call quite the package for it's price of only 5€.

Now, naturally one would assume that you'd have to use good old C/C++ with it and you'd probably be right in 9 out of 10 cases but I thought that was boring and really wanted to use the most hyped language of them all, Rust. I mostly blame [Shadow](https://github.com/shadowninja108) for his work on skyline, [Elise](https://github.com/EliseZeroTwo) for her WARS-8 project and [Jam1garner](https://github.com/jam1garner) for his really amazing and detailed blog posts that strongly inspired me (If you're reading this, thank you for inspiring me even though you probably never talked to me before). 
Sooner or later I really want to write a blogpost about Rust itself but I feel like I'm not too comfortable with the language yet to share my knowledge with random internet strangers.

Anyways, 1 + 1 = 2 and so I decided to try to use Rust for the microcontroller which at first seemed surprisingly easy but as everything in the low-level development world, it ofc had thousands of small problems that lurked behind the corner to destroy you once you tried it. Given that I want people to not fall into the same pitfalls, this simple and short blog post should hopefully solve most common problems when trying this (and might arouse interest for some, idk).

### My Setup

Before writing about many of the problems, I gotta admit something. My setup is really really cursed when it comes to such stuff.
I'm currently running Windows 10 Pro on my main machine with 99.9% of all development related stuff running inside a WSL2 Arch instance. For those that are familiar with the Windows Subsystem for Linux stuff, Arch actually isn't one of the officially supported systems for it. My Arch WSL only exists and works because of the amazing work and dedication by Arch fans. If you also dedicate your existence to sharing the word of our lord and saviour Arch, I'd recommend this: https://github.com/yuk7/ArchWSL

{{< figure src="https://external-preview.redd.it/N4eyMIDOoK93PZthrhaSTO8dSawi3nZTypJD73pYa10.png?auto=webp&s=db3215d5c1a58ffdacbd67a0a5f71bb3025f638d" height="50%" width="50%" class="text-center" alt="*btw I use Arch*" caption="*btw I use Arch*">}}

It honestly works really well and after having Arch as my main OS for quite some time, I really can't live without the AUR and rolling releases. So far I haven't experienced any major issues (With some exceptions for WSL scripts that were meant for debian based systems).

### Broken drivers

For some unknown reason my Longan Nano shipped with really broken drivers and Windows 10 had extreme issues installing any drivers for it. Normally it should just easily go into the flashing mode through a button combination and then appear in Zadig to simply install the WinUSB (or similar) driver. 
In my case Zadig broke completely and I had to do it manually. At first this annoyed and confused me but thanks to the [Microsoft WinUSB installation guide](https://docs.microsoft.com/en-us/windows-hardware/drivers/usbcon/winusb-installation) and [another developer](https://ribesjordi.wordpress.com/2020/04/10/setting-up-the-pio-ide-for-sipeed-longan-nano-in-windows-10/) that had the same issue, I was able to fix it quite painlessly. 

### The Longan Nano Rust Crate

Luckily, there is a well done and ready to use rust crate for my device already, you can find it here: https://github.com/riscv-rust/longan-nano

The Getting Started part wasn't actually that hard aside from the fact that you had to basically install forks of every single thing because Risc-V related stuff isn't streamlined in most projects yet. 
Once again, I gotta thank the AUR for saving my from a lot of hassle by simply providing easily installable packages of most of these forks. Sadly the openocd package appeared to be broken for now because of some dependency issue but luckily there are three different ways to flash and use the rust crate so I could just switch to dfu-util.

### WSL and microcontrollers don't pair well

WSL is awesome but it sucks when it comes to physical devices. Given the nature of a subsystem, I sadly couldn't flash the microcontroller from my Arch instance and had to install dfu-util on my Windows machine to flash the device. Luckily the filesystem integration in WSL2 is so well done that I could simple open a powershell inside my WSL2 files and use my Windows tools on them. Glory to the monopoly of Microsoft I guess. All in all this was more of a minor hindrance that can easily be fixed with a custom buildscript.

### Building the examples

At first this seemed easy, there is one minor error in the documentation in which it tried to link to a wrong directory but that was quite easy to spot and fix. After a bit of tinkering I had a flashable file that I could just throw onto the Longan Nano and be happy with and that's what I did. The blinking example worked and so I moved on.

### The Present

As I said at the start of this blogpost, this blog post isn't as detailed as I originally expected my second blog post to be in order to be more consistent and actually have some form of content on my site. For now I'm still working on my own project with the library and have made some, even if little, progress with it over a few hours of testing. My aim is to get something more impressive to work for the next blogpost so I can explain most of peripherals the Longan Nano has.

The endgoal is to get Rust running on the Raspberry Pi Pico but for now I thank everyone that read this blogpost till this point and hope to see you in the next part of this series. ~~~Lets just hope that I'm motivated enough to write the next one~~~
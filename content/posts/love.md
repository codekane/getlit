---
title: "Love"
date: 2024-03-10T11:10:36+08:00
draft: false
language: en
featured_image: ../assets/images/lights/Lit.jpeg
summary: The Lights - Design Process for the Dual-Sided SK6812 RGBW lights that I designed, and had manufactured last year, and the incredible amount of work that goes into making something Good.
description: The Design Process is a Costly Endeavour. I had meant to talk about something new, but instead it reminded me of something old, from last year, and I felt like sharing.
author: Ryan Horricks
authorimage: ../assets/images/lights/IMG_0261.jpg
categories: Powerful
tags:
---

# Love: It's not always enough

I'm going to level with you, I didn't meant to be posting this today. What I'd sought to achieve was to design a 
case for the smaller battery, and to 3D print it, and incorporate it into a new hat close to half the weight, so that 
I could put it on comfortably for a night out, and get people interested.  

That sounds easy, when it's strung together in a sentence, however the fact is that the work that goes into every 
detail is profound. I started today with the expectation that it would take me 2 hours. 2 hours later, I had the 
beginnings, and a feeling for the process. 4 hours later I'd remembered how to use [Rhino](https://www.rhino3d.com/) 
and hit my original estimate. Now, it's 8 hours later, and while I'm mostly done, the design file has suffered harm 
from what became an experimental process, and will need to be cleaned up before being suitable for manufacture.

I've wisely decided to set it aside, relax, and get ready for my trip to Seattle. Sure, I won't have my kit, but 
at the same time, my value and worth as a human being is not defined by the things that I make, but rather something 
deeper, and more intrinsic. It's something that we are all born with, but for those of us who have suffered unduly 
in this world, we have been known to forget what we're worth. It's not healthy, and it's not happy, and it's a big part 
of why I've not made as much progress with this project as I could've. I was working on it for the wrong reasons. 
As the end, instead of a means to some greater good.

Meditation helps, and in the spirit of enlightment, I will now share with you the story of the last time I bit off 
something new, intimidating, time-consuming, and perhaps even beautiful.

## The Lights (and how to choose)

I'll start out by telling you what I went with. That would be the SK6812 RGBW.  
- White channel provides a greater depth of colour, and the light itself is much more usable than a comparable RGB LED, if you're actually wanting to see.  
- Relative insensitivity to voltage changes -- there is very little difference in the light produced when powered at 5V, 4.2V, or 3.3V. By the time the voltage drops enough to matter, the microcontroller has bigger problems.  

Now, I went with the 5050 option for this writeup, however they are also available in 3535, 4020, 2020, and 1515.
- These numbers are LxW in mm. So, 5050 is 5x5mm, 3535 is 3.5x3.5mm, 4020 is 4x2mm, and 2020 is 2x2mm, and 1515 is 1.5x1.5mm
- RGBW LED's are much harder to find in the smaller sizes, and given my premise is useful light, the smallest size I've found is the 3535.

This being said, there are downsides to my choice, as well as upsides to others. Here's a synopsis:

WS2811:
- This is a WS2812, but without the LED. It's a big chip, and was used in the original addressable LED's. It needs to be connected to a discrete LED to be useful.

WS2812:
- The original addressable LED, with an IC built into the chip to enable a string to be driven with a single wire for data
- Suffers from colour shifts when operated under 5V
- Uses a similar communication protocal to the SK6812, however at a somewhat lower frequency (effectively means that for a given length of LED's, the maximum frame rate will be somewhat lower.  

APA102:
- Uses a 2-wire Serial communication protocal, requiring a more complex setup, but enabling much longer chains of LED's without adversely affecting framerate
- Very High Refresh Rate... This is useful for Persistence of Vision applications, enabling it to crate the appearance of static images when moved quickly.
    - This is not possible using an SK6812
- No RGBW. Also, the speed isn't quite as fast as it used to be, on account of it no longer being manufactured by the original company.
- Pricy

SK9822:
- This is basically a knockoff of the APA102, using the same 2-wire communication protocal, and featuring a very similar refresh rate that is likewise suitable for Persistence of Vision (PoV)

APA108/APA109:
- Honestly, these look dope, and they sound dope, however I've yet to see them in-person, and a lot of the features I find important have been promised, but not delivered.

WS2815:
- These are the WS2812, but with an auxiliary data line. With the WS2812/SK6812/APA102, a single break in the chain will render all subsequent lights non-functional. Thiis means if one burns out, the entire devices goes bad.
    - This both is, and isn't an issue
    - This benefit comes with a cost: increased voltage drop, and subsequent colour degradation in long runs.


### The Moral?
- SK 6812 RGBW is great all-around, however isn't fast enough to serve effectively as a flow toy.
    - It's also the best option I'm aware of to run directly from a single Li-Ion/Li-Po battery without degrading itself.
- APA SK6822/APA102/APA108/APA109 are not availiable with a white channel, however are amazing for visual effects. Application-specific, but technically impressive.

## Strip Club

If you talk about LED's, you'll generally find them in strips. Actually, there are options.

> Through Hole
These are old-style LED's. If you had a computer in 1998, you would've had what I imagine to be a green LED to show that the power was on. It was capable of pulling ~20mA, much like most LED's you'll find today.  
- Modern LED's produce significantly more light for that 20mA
- Most LED's produce substantial quantities of photons when being given less than that. The higher the power, the less you notice the difference.
- Through-Hole LED's can be had with Red, Green, Blue, Violet (UV), Amber, White (actually Blue/Violet with a phosphor), and RGB (separate  red, green, and blue channels, with 4 leads).

> LED Strip
These can be had with virtually every variety of light, and in a variety of densities, voltages, and power requirements.  
- Common densities are 30, 60, 144, and sometimes even 240.
    - Which size of LED has a lot to do with what you can do with density, however even 5050 LED's can be laid very densely.  
- These are available in Analog, and various types of Addressable LED's.
    - What I mean by analog is that there are not IC's for each light, making the entire strip have the same colour when used.  
    - This is done most often with a common cathode (+), and a separate ground connection for R, G, B, and sometimes even more.
        - There are LED's out there with RGBW, others with two separate white channels, and in fact a CCT option that gives you Warm, Neutral, and Cool white.
        - Addressable IC's that easily support more than 4 channels (RGBW) aren't readily available, making use of strips with 5 or 6 channels much trickier to accomplish.  
- Power Requirements can be significant. At maximum draw, a WS2812B can pull 20mA x3, for each LED in the strip. That means full-brightness white for a 1m RGB strip with a length of 1m, and 30 LED's per meter requires 1.8A at 5V... Your phone charger might do 3A, if it's USB-C, and 2.1A tops otherwise.  
    - Some LED's make use of 12V instead of 5. The amperage is less severe, in this case (unless you are using a boost converter to get that 12V from 5V, in which case you're going to be losing rather than gaining.
    - Voltage ranges up to 24V in some cases.
        - Strips using these high voltages exhibit much less voltage drop over long-distance, which matters in some use cases.
        - Strips using 24V often have a series of 6 LED's for each IC, meaning that for each 6 in the strip, they will have the same colour, however the strip as a whole can be addressed, and changed with more nuance than analog LED's provide.  
- Weatherproofing is available. Look for IP67 or IP68 strips if you're looking to do an installation outdoors.
    - IP67 is rated for 30minutes at 3feet depth (do not submerge in water and expect it to work long-term)
    - IP68 is rated for permanent submersion down to a depth of 13 feet.
    - Insulation must be stripped off in order to solder to the ends of these, unlike unprotected strips.
- COB LED's
    - These strips are super-dense, with the LED mounted directly to a substrate (literally sapphire, FYI) to enable extremely high densities. Individual LED's are not perceptible.
    - I've found limitations in what these can do compared to other options, namely being addressable, however they fulfill a useful niche.

> LED String
These are varied. You'll find some of these at the dollar store, being a string of through-hole LED's encased in epoxy (and thus waterproof/diffused). This also includes fairy lights, which used SMD LED's, as opposed to the through-hole ones.  
- Addressable versions exist, however with limitations on form factor, and available options.
    - Some of these lights use the original addressable IC (WS2811).
    - Others are IP68 rated, making them useful for outdoor use.
    - Expect a lot of bulk. Weight of the wiring can be significant in certain applications, which is my major complaint (and reason for the developments to follow).

> PCB's
Examples include the Adafruit Mini Button PCB, which is roughly 9x9mm... That's probably one of your best options.  
- Labour is SIGNIFICANT. These have pads on the back, and need to be individually soldered.
    - When done correctly, they can be used much like an addressable LED Strip or String. It takes a lot of extra work, and some skill to use effectively.  

> High Power LED's
Up until now, we're wearing kid gloves. The SK6812 in our example is 56mA @5V with RGBW channels at maximum
- 20mA white, 12 mA R/G/B
- W = V * A, so 0.28A each (which is why we can use so many)
    - Heat is an issue here, however it's relatively minor.

High Power LED's are in the range of 1-5W, at perhaps 6V
- A = W / V, so you can expect a 3W LED to pull 0.5A, each, at maximum throttle.
    - These use the same package size as the smaller LED, making heat a much bigger issue. Most often these will need to be used with an aluminum PCB/heatsink, and even then, brightness should be throttled for longevity.  
- These can be had in an addressable form.
    - If you've ever felt the urge to cut open one of your "Smart Light Bulbs", you'll find a set of LED's with moderately high power, with an ESP8266 likely integrated to connect to wifi.  


## The Problem
I initially started off using Analog RGB strips. I controlled them with an Arduino, and 3 N-Channel Mosfets. It worked, and it was cool. That was 7 years ago.  

My most recent foray into the light started with the use of RGBW SK6812 IP68 LED Strips. The lights themselves were good, however there were problems:
- Heavy. For a string of 50 lights, we're talking 1lb.
    - How many pounds can you carry on your head?
- Much more wiring than was necessary for my use case
- While they were IP68 rated, that came with a lot of extra size, to account for the case, and weight, accounting for the epoxy used to seal out moisture.  

I also found a desire for something more, in this foray. I had 40 holes in the hat to populate, and 50 lights per string. I used the first 40 to point down, and then wrapped the last 10 around hte top, pointing upwards. I found the effect compelling, and it left me curious about the merit of "toplighting".

Alas, that did not exist. With proper diffusion, and even lenses you can deflect the light, however under no circumstances is it produiced in a 360 degree pattern. Most often, LED's are best at 60 degrees, useful up to 120 degrees, and due to the SMD form factor, at best capable of 180 degrees of illumination.  

Given my problem, and my use case, I set out to try to find a way to experiment. I wanted a bare PCB (I drastically underestimated the labour involved, although in theory that can be outsourced to third-worlders... Though I question the ultimate merit of passing the buck on the buck of carpal tunnel).  

That can be had. There are 9x9mm mini button RGBW SK6812 LED PCB's available, in packs of 10 for a decent cost. These are the same boards used in the light strings I initially purchased, and they work fine. Except, they don't go both ways. I wanted to try something dual-sided, and it turns out this doesn't exist... At least, not within my size constraints (some of the strings are 12mm diameter, others go up to 20mm, and none as small as I wanted).

So, in a dramatic twist of naievety, and in an absolute act of sabotage towards actually taking my initial product to launch, I set forth to develop a whole new product. One that was able to be connected at 45 degrees angles (to minimize wiring), illuminate both down and up, and do so in the smallest form factor possible.  

The funny thing is, I actually succeeded.

## The Process, The Product, The Pain
I present to you the finished product. 

I had ~480 of them manufactured, which is actually 960 LED's. This was my first foray into actually having a PCB manufactured, and I found it quite intimidating. The knowledge that any single mistake I made would be replicated 480 times, and potentailly leave me out a substantial sum of money bothered me. Truth is, I had also been working on designs for the mainboard PCB, and that scared me more. Looking back on those designs, I made mistakes that would have prevented things from working properly, so in that sense it's probably best that I opted for something simpler.  

### Define Simple
By simple, I mean my BoM (Bill of Materials) consisted of only 2 parts. SK6812-RGBNW (Natural White is ~4000k, whereas wharm white is ~2300k, and cool white is closer to 6500k). The other part was a decoupling capacitor, unnecessary with some LED's (WS2812C, I'm looking at you), however with the SK6812 it's reported as necessary, and serves to prevent the voltage from experiencing severe drops when demand increases.  

The hard part was the constraint, which was to keep it as small as possible. I went larger than the 9mm diameter of the mini-buttons, however through a series of iterations and experiments, I ultimately settled on another shape... You might find it familiar.  

It's cute, right? It's also tiny, and designed so as to be able to handle 1A of current through its traces, even when potted in epoxy (which resists weather, but hinders cooling).  

Rather than the solder pads on the back of the button, I opted for a mix of pads and through-holes. The theory was that soldering to pads is hard, and through holes would be easy. This was fallacy. It's true, when using solid core wire, however in my application I opted for stranded, because it's more flexible, and my product is intended to be worn. Problem with stranded wire is that it has a hard time going through a small hole without small strands splaying out into a neighbouring connection, causing a short, and making the process of using this option incredibly painful to implement.  
- Pads are a pain, however I'd likely opt to 3D print a jig, and get cables made professionally, so that the process could be completed with a minimum of effort.

As to the shape, it's geometric. I didn't intend, going into this, to make almost 500 tiny little hearts, however I have a love of design, and a sense that every detail should be shown love, if it's to be shown to the world. I iterated many times, taking inspiration from literally every other LED PCB I could find... Literally, I looked at all of them, imported them into the project, compared mine to theirs, and worked to create something with all that and more.  

### Good Artists Copy, Great Artist's Steal, and if you're Clever, you don't have to
Neat trick here is that for anything being sold on Adafruit, Sparkfun, and many smaller firms, you're likely to be able to find their schematics and layouts on github. Open-Source is a real thing with hardware, and you can learn a great deal from seeing other people's work. If you want to steal, you can have those products manufactured yourself. If you want to copy, there's a lot to be inspired by. And if you're great, then you'll be able to do better.  

### The Pain
I used to be able to sell myself on how easy this stuff is. Ignorance is bliss, unless it isn't, and when you're seeking perfection, you'll find that it takes a lot of tries to come up with something Great.  

I sold myself on this path by virtue of it opening another front. My theory was that the end-consumer for any given finished product is a wide swath, however it's limiting. I thought, if I'm going to make a product, then why not also make product's out of the pieces of it? Then I can expand my market to include the people smart/skilled/niche enough to actually do the thing's I describe, instead of settling for being the wizard who magically makes it happen.  
That might not be a bad path, however I don't know. I've failed to validate that assumption, and in fact built the product before I found out if anybody else wanted it. Worse, serving as the sole hand behind all of this, and trying to hold down a job while I did it, I paid a terrible price for the progress I made. Four hours of sleep, and 16 hours of work a day week-after-week left me with difficulty rememebering the names of people I met, and was, simply, not healthy.  

Even worse than that, was that due to how much of myself I poured into the product, I had nothing left to handle the business, the marketing, the socialization and validation and business that comes with actually turning these efforts into money. On a two-man team one guy can float the boat, but when it's all me, and I'm already struggling with life/money/mental health, the hit was significant.  

Now, a reasonable man would simply live a better life. To value his health. To protect his energies, and ensure they are spent in a manner that affords him the best of possible lifes.  

Alas. I Ihave not always been a reasonable man.

## The Point
I'll admit to having spent 8 hours today trying to push through the impossible, and I'll point out that it isn't plainly impossible. It's largely a matter of skill, and I learn as I go. I don't do the tutorials. I imagine what I want to create, and I build it, and invariably my vision is vastly greater than my first attempt. I continue, I persist, and I have learned to apprecaite the journey over the destination. To expect greatness is to feel you somehow need to, and that signifies a lack of self worth. In fact, this is the first time I've picked this project up seriously since December. I did a demo at DemoCamp, a year after my first time attending (and deciding I wanted to do it). Everyone loved it. People reacted in a manner that was overwhelmingly positive. I shone, and in fact what I had was sheer magnifence in comparsion to what everyone else presented (not to knock, but there were no one-man army's with a vision and product and passion and heart).  

So why haven't I worked on it? It's not what I was doing, but why. These aren't my first products. This isn't the first timie I've ideated, iterated, and ultimately produced something very nice. My motives for needing to do something so grand were a symptom, and presenting on-stage highlighted it. People reacted glowingly, and my world views were so dark, I couldn't even take it as it was. I saw everythiing wrong with the world, and with myself, and in fact fell into a deep depression. When I had motive to act, it was in ways counter to my own interests, and in familiar ways that I'd yet to understand.  

What the Hell? That's why I work with Light.  

The point, at the end, is that I don't know any of this was worth it. I don't regret my choices, because they brought me to where I am, however the place I am in is a far cry from where I sought to be seven years ago, when I started on my journey. The patterns persist until the lesson is learned, and the moral of the story is that the light of consciousness is all that we can hope to bring with us to battle with out demons. By shining a light on the darkness I was able to learn the truth, the real reasons why I am who I am, and what I can do about it. The answer is to Trust, and that's something I now learn. I think the reason I work this alone is because of my nature, the distrustful ways that I've seen the world, and the ways I've kept others from being close enough to make a difference to the outcome.  

That's another topic, mind. This is last year's post.

This year is different. I leave for a week in Seattle tomorrow, and I can honestly say that I'm happy that I can go as I am, as a wonderful man with no plan, barely enough money, and a path to enlightenment.  

I'm also happy that I picked this up. The times are changing, and the insanity is over. This time around, we all have a choice. I wonder what I choose?

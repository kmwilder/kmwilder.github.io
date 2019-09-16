---
layout: post
title: Wedding Clock
date: 2019-08-15
tags: Clock
---

## Constructing a Ceremony

As of a few days ago, I'm a married man. With the help of our [talented officiant, Marguerite](http://www.meaningfulmarguerite.com/), Sarah and I were able to make a customized ceremony: shedding the 'traditional' aspects we didn't particularly care for, adding personalized jokes and flair to replace it.

One part we decided to swap (before we fully knew how much work the replacement, or the wedding overall would be) was the unity candle. We saw the value in displaying some symbol of unity, but the candle as a symbol here feels kinda... odd?

We take our individual flames, lit pre-ceremony (or during?), to light the central flame. If we're precise, we'll smoosh our candles together to create a single flame, before hitting the wick of the shared candle so that we can both claim we contributed to the lit candle. Though under the pressure of the moment, it's easy for one of our flames to miss, meaning only one of us lit the candle, rendering the remainder of our marriage fraudulent. Then, we have the option to blow out our individual candles (as we're now one, spiritually and for tax purposes), or leave them lit to signify that we've not lost our individuality. Neither of us are going to give up our individuality, but what are we going to do with our three flames, then? We'll just blow them out as soon as the ceremony's over. The whole thing seems like a temporary diversion.

So, we gave it some thought, and came up with this touch-triggered clock as a replacement. It consists of an Arduino, two servos, three power sources, a tiny speaker, a relay, a pushbutton, and a pull-up resistor that we ground with our own bodies. We each grab a wire, and when we touch, we bring an Arduino input down from 5V to about 2.5V. The Arduino constantly polls this input, sees the transition, then fires off the servos, toggles the relay, and then plays a little tune.

I forget which of these we thought of before settling on the clock, or which we thought of afterwards to do some post-hoc justification of why it works, so I'm just going to list everything:
* By completing a circuit with our own bodies, we're equally and unmistakably contributing to the triggering of the mechanism. Minor differences in body resistances can't even symbolically matter, since we're sampling the result as a discrete 1 or 0.
* The moment marks the beginning of the rest of our lives together: the clock starts, and it keeps going as long as we're still breathing. To maintain the conceit, maybe we'll hold our breaths whenever a battery swap's needed.
* Sarah's a SW engineer, working at a startup that makes the law easier to search through. The code we wrote for this made the moment we were legally wed quite visible.
* I'm a HW engineer, focusing on voltage-aware clock generation logic. Kinda obvious connections to draw here.

## Constructing the Clock

Initially, we wanted to simply have the clock start by turning on its power, which was quite simple:
![Initial touch bridge](/assets/touch_bridge.png)

We'd touch, providing power to an SCR, which would trigger a relay, which would provide power (via a dummy battery, or simple spliced wires) to any clock we can find.

We got this working pretty quickly, but after a bit of clock shopping, realized we needed a bit more. By simply turning on a simple clock face, it'd move once per minute: not too flashy. Many came with pendulums, but these end up moving whether the timekeeping device is on or not. They also need an initial push to get going.

<img src="/assets/wall_clock.jpg" alt="Bulova Cranbrook pendulum wall clock" width="200" style="float:right"/>

We settled on this wall clock, which uses 2 C batteries to keep the pendulum going, and 1 AA battery to power the clock face & timekeeping devices. The AA would be powered by our "dummy" battery, for the symbolic start-the-clock reaction to our touch, and the C batteries could just remain in there without alteration. We'd need a servo, though, to hold the pendulum in an inactive state to the side until we triggered it.

Since we needed to trigger a servo, we figured the Arduino was needed. Since we were involving the Arduino, we let additional features creep in:
* Because we already had servos figured out for the pendulum, it was quick and easy to add a second servo to raise a flag that said "Married!" at the same time. 
* I had messed with audio on a different Arduino project, so getting it to play a small tune involved only some copy-pasting from the old one. We probably spent more time on deciding what to play: we tried a few different wedding-appropriate tunes, and a MIDI version of "Such Great Heights", but in the end decided we wanted something super short. So, "da da da DAA".

We were also able to make things a little more resilient via the Arduino, since analog circuit design isn't really in our comfort zones, but code definitely is.

For starters, we deglitched our touch inputs by polling for the same value over 10 milliseconds before allowing a toggle. We noticed that sometimes, static electricity would cause a trigger as soon as we first touched the wires.

We added a third state to the whole device, rather than the simple on/off:
* RESET: The power on state, the whole device is idle/unresponsive until the pushbutton is pressed.
* PRIMED: The servos are moved to their untriggered position, and the touch inputs are polled.
* ON: When transitioning to the ON state, the servos are fired, power to the clock is connected via the relay, and a sound is played. Clock power is maintained in this state.

This way, we could power the thing on, do some quick testing during rehearsal, then put it in the RESET state. There'd be no risk of firing it off, even as we're handed the wires. As our officiant explained the device, our best man hit the PRIME button, and when instructed to kiss, we'd do so, moving it to ON.

![Wedding Clock Fritzing diagram](/assets/wedding_clock.png)

The final Arduino code, and Fritzing diagram, have been checked into [this GitHub repo](https://github.com/kmwilder/wedding_clock).

<img src="/assets/clock-breadboard.jpg" alt="Breadboard prototype" width="1000"/>

## Demo Day

To prevent wires coming loose from a breadboard, I soldered most of it down onto a protoboard. It's... not my finest work. We tossed it into a box for transportation. Because I'm paranoid, I included a second copy of the circuit on a breadboard, so we could either scavenge it for parts or swap to it completely.

<div style="text-align:center">
<a href="/assets/clock-protoboard.jpg"><img src="/assets/clock-protoboard.jpg" alt="Soldered protoboard." width="500" align="middle" style="display:inline-block"></a>
<a href="/assets/clock-casing.jpg"><img src="/assets/clock-casing.jpg" alt="Wooden casing." width="500" align="middle" style="display:inline-block"></a>
</div>

We shipped it to Chicago a few weeks in advance. On arriving (three days before the wedding), testing showed that one of the servos did not survive the journey. Based on how hot the servo wires were getting, something was shorted. Luckily, Sarah's father had a large bin full of spares, which we were able to tape into place without much hassle (but leaving me paranoid about shorts for the rest of the week.) We also realized, we didn't quite have a solution for making our wall clock stand unaided on the "unity candle" table. For a while we were going with some wire and a bag of sand, but my dad was able to cut some spare 2x4s based on some photos I sent him, and we had a solid base for presentation.

The day of the wedding, it sat in the trunk of our car until we got to the venue. I set it up in-between pre-ceremony family photos, tested it it very quickly, hit reset, and ran off for more photos. At this point, it had been working pretty dependably all weekend, and all the batteries were fresh, so I was resolved to stop worrying about it.

When our ceremony started, I can thankfully report that it was out of my mind completely, so I was able to focus 100% on the whole "getting married" thing going on... until we got to the end:

![Clock, triggered](/assets/clock-triggered.jpg)

TODO: Vid of it working?

All in all, it went really well, and I'm glad we did it. The marriage, of course, but the clock too.

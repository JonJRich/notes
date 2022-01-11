#BalenaLabsResidency 
LAST UPDATE - 11 Jan 2020

*Notes from Jon*

*IMAGES - to be updated/refined - especially the wiring diagram, I used this as a personal reference when I was putting it together but know it needs work - is there a stylesheet we follow for this kind of thing*

*SOFTWARE - Instructions, feel a little basic/obvious so we may need to cut it down, I also couldn't find how to download direct from balenahub (only fork the fleet?) - but this could well be me not understanding the process fully...*

---

# Sunlamp - Blog - Draft 1

## The problem

The sun is a magical thing, not only does it give us light and warmth but through it's regular rising and setting it drives our circadian rhythm - the natural process that regulates our sleep–wake cycle.

But sometimes that connection with the natural rhythm of the sun breaks. If you're in the northern hemisphere in the depths of winter the idea of waking up at 8am and going to bed at 4pm with the sun might sound ideal, but isn't exactly feasible. Equally sometimes you might need to be up late, or very early, sometimes by choice, and sometimes not.

Light up alarm clocks already exist to help us with this dilemma, most built around a light that gradually brightens up to your desired wake up time. Unfortunately in my experience I found them very basic, and on top of this they missed one important factor, that not all sunlight is the same.

If you think back to seeing the sunrise (or set if you're a night owl) the light is warmer/more orange early in the morning and late at night, and brighter/more blue during the day. Yet my wake up alarm clock only had the option of one colour. Not ideal.

## My solution

With these issues at the forefront of my mind I created the "sunlamp".

![image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/sunlamp_video_01_cover.png)

[Watch the video](https://raw.githubusercontent.com/JonJRich/notes/main/assets/sunlamp_fullsequence_720_low.mp4)

An ambient lamp that can be programmed to mimic the natural light cycle of the sun, giving you a subtle reminder of the suns natural transitions through out the day. Gradually illuminating with a soft warm light, before rising to a bright light and repeating the cycle in reverse at the end of the day.

Powered by a Raspberry Pi running on BalenaOS the lamp times and fade duration can be set remotely from anywhere in the world. The lights in the lamp are LED strips containing both Warm White and Bright Light LEDs, meaning that a wider spectrum of white light can be achieved and at the right times.

My final device houses the LEDs, Raspberry Pi and all necessary electronics into a single container creating an effective, and I think pretty good looking, 'lamp'. This however isn't essential, or even especially necessary as you could simply use the LEDs as ambient strips behind you monitor, TV, or a even just large piece of furniture like the headboard of a bed.

## Difficulties I faced

When I initially approached this project I hoped that I would be able to use some of the great LEDs drivers available like the Adafruit Fadecandy used on the balena [Christmas Tree.](https://www.balena.io/blog/control-your-christmas-tree-a-raspberry-pi-powered-rgb-led-matrix-v2/) This however, was not going to be the case, as the Fadecandy only supports WS2811 or WS2812 LEDs, which use individually addressable RGB LEDS, unfortunately these do not depict white light as accurately as true white LEDS so I continued my quest.

Not a problem I thought, I'll just go out and find an LED strip that has Warm White and Bright White LEDs, and eventually I did find them but there's a very limited amount of options out there. [These](https://www.amazon.co.uk/dp/B08D6S2H45) are the ones that I went with in the end, with both types of LEDs contained on a single strip. As fas as I could see if you want just the strip with out the power supply and remote you'd have to get the two strips separately through Aliexpress.

## Want to try it your self?

   ### List of parts

   - Raspberry Pi
   - SD Card
   - LED light strip
   - 12v Power Supply ( I used the one that came with the LEDs but if buying strips on their own this will be needed)
   - 2.1mm DC barrel jack adapter
   - N-channel power MOSFET (30V / 60A) × 2
   - Perfboard
   - 12v to 5v power converter
   - Case*
   - Thin plywood*

*optional

### Choosing your casing

For my Sunlamp I had decided that even though I was using LED strips I wanted to create something that was closer to a traditional lamp, with a single unit housing the electronics and LEDs and the light being from single source. I knew that I could arrange the LEDs strips in parallel to create a light panel, so all I needed was to find a case. Essentially I needed a nice looking box with a transparent lid. And I found this...
![Image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/sunlamp_case.jpeg)
What is this I hear you ask, it's a fancy wine box of course ;)

Inside this I was able to get all the electronics as well as 8 lengths of 30cm LED strip, plenty to be bright enough for what I needed.

If you go down the route of housing everything inside a single case don't feel like you have to copy my design, in fact as I neared the end of the project I experienced a couple of problems...

The main issue I had was figuring out how to diffuse the LEDs so instead of each one being clearly visible behind the glass, it was a single pane of light. My first error was to mount the LEDs facing out of the box, apparently for ideal diffusion I should have mounted them around the internal edge of the box and bounced the light off of a white back board, but by the time I realised this it was too late for me to implement easily.

Instead I went for 3 layers of materials, that together provided an OK amount of diffusion. These were 5mm of white, semi-transparent foam, followed by the acrylic 'glass' that came with the lamp sanded on one side and a sheet of thin paper on the front (mainly to hide the sticky back plastic I stuck the foam on with...).

And to be completely honest the casing isn't an essential part of the project – it will work just as well if you mount the LEDs strip directly on or behind some furniture to create an ambient lighting effect, possibly even better.

### Setting up the hardware

The hardware consists of four main parts; the board with the electronics, the Raspberry Pi, the light panel and the power converter. I'll go through the set up for each in that order.

#### Setting up the hardware

In this lamp the Raspberry Pi is used to trigger the two sets of LEDs on/off but as the LED strips I'm using are 12v and the Raspberry Pi uses [CHECK!] logic I needed to have an N-channel power MOSFET for each of the rows of LEDs. These acted as a switch where the low voltage logic could turn the high voltage on and off. In additional to the two transistors I used soldiered a 2.1mmm barrel jack onto my board so that I could use the power supply that came with the LEDs, whilst still being able to unplug it.

For those following along at home here's a diagram of the wiring....

**DIAGRAM TO BE UPDATED**
![sunlamp_wiringdiagram_TOBEUPDATED.png](https://raw.githubusercontent.com/JonJRich/notes/main/assets/sunlamp_wiringdiagram_TOBEUPDATED.png "sunlamp_wiringdiagram_TOBEUPDATED.png")

And this is how mine looked...

![sunlamp_internals.jpg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/sunlamp_internals.jpg "sunlamp_internals.jpg")

#### The light panel

If you're going to be using the LEDs au natural as a strip then you can skip this next bit. Seriously nothing to see here!

If like me you're plan to house the LEDs inside a case you will need to make a light panel. For this I cut a piece of plywood to the internal dimensions of my box and drilled a 5mm hole into one corner to feed the wires back through. Then it's simply a case of sticking down as many strips of LEDs as you want/can fit on the board and soldiering them end to end - one thing to note is that LED strips are directional so the end of one needs to join up with the beginning of the next. The set I bought didn't come with a helpful arrow, oh no that would be too easy, but I followed them round one by and figured it pretty easily.

![sunlamp_lightpanel.jpg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/sunlamp_lightpanel.jpg "sunlamp_lightpanel.jpg")

#### The Raspberry Pi

This ones a pretty short step, attaching the following cables into the Raspberry Pi; Warm White Trigger ( I used PIN 17), Bright White Trigger (I used PIN 13) and Negative (PIN 06). At this point it's worth flashing the SD card you're going to be using and putting it in too (see software guide next).

#### 12v to 5v convertor

The final step, although not technically necessary is to wire the 12v to 5v connector to the perfboard and connect it to the Raspberry Pi for power. This means that both the LEDs and Raspberry Pi can be powered off of a single input. One thing to note is that the micro USB that comes with the converter protrudes quite far from the Raspberry Pi, I got round this by mounting mine at a jaunty angle but a neater solution would be to use a right angled adapter.

*Note: Once I had everything powered up I was getting undervolted warnings for the Raspberry Pi, as far as I have tested everything seems to be working ok but to be doubly sure a more powerful power supply is possibly a good idea. *

And there you have it, system's go!

### Software installation

**Steps...**

So, first things first, login to your balena dashboard account, or if you don't have one create one.

Once in, click on the 'Create fleet' button in the top left to create the fleet your lamp will be part of.

![Image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/01_sunlamp_install.png)

After creating your fleet, chose to 'Add device' from the middle box. Here you can set the device type and version, I would also recommend setting the edition to 'Production' and including your wifi details. Once that's done download the image to your machine.

![Image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/05_sunlamp_install.png)

The next step is to flash the image to the devices SD card, ideally using balena Etcher. From there it's a case of plugging in and powering on lamp, and after a minute or so you should at this point you should see the lamp as part of your fleet.

![Image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/08_sunlamp_install.png)

At this stage the device still doesn't have the lamp code on it, just the balenaOS, this needs to be upload to the device separately. To do this download sunlamp code from [here](https://github.com/JonJRich/sunlamp/archive/refs/heads/main.zip), and push to the device using balenaCLI.

![Image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/11_sunlamp_install.png)

At this point, after rebooting itself, the lamp should be working, but if you want to set the on/off and bright/warm times as well as the fade duration you will need to add them as variables to your fleet.

*note: the variables only contain the 'start' time for each phase as the 'end' time is automatically taken from the start of the next one. For instance LAMP_BRIGHT_OFF = LAMP_WARM_START and so on.*

![Image.jpeg](https://raw.githubusercontent.com/JonJRich/notes/main/assets/15_sunlamp_install.png)

Sit back and enjoy the ambiance

....

### Final thoughts

So if you've made it this far first up congratulations, hopefully you also by this point have some nicely glowing LEDs beside you too.

As part of balena residency, and my first foray into software and hardware hacking, I've learned an awful lot and not simply that I am truly terrible soldiering. Cliched as it sounds this feels like just the beginning, whilst the lamp is functionally sound there are still a lot of features I would love to add, here's just a few:

- Physical on and off switch
- Ability to control the brightness of the LEDs
- Web based input for scheduling
- Auto adjustment to the actual rhythm of the sun

On top of that there's so much I'd love to do with the physical design of the lamp, somewhat naively I'd assumed that diffusing the LEDs would simply be a case of frosting the glass in the case a little, but turns out it's a little more complicated than that. For future designs I'd like to experiment with mount the LEDs around the internal edges of them to bounce them off an internal back paint, taking advantage of...

^ *Read up on this and expand upon*

---

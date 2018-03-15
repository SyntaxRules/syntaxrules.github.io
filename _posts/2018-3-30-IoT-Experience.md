---
layout: post
title:  "Creating IoT Devices"
tags: IoT getting-started software
---

Some years ago I was tasked to create a number of IoT devices from scratch. The goal of this was to create low-cost sensors for factory automation. When I started my knowledge of circuit design, pcb design and the manufacturing process was non-existant. My background is in software, I was use to blaming hardware engineers- not creating hardware.

This article explains what I did by teaching you (the reader) about IoT today. I'll cover:

  1. The bussiness of IoT (Market, Players, Technologies)
  2. The technologies of IoT (Hardware, Tranportation, Analysis)
  3. Buy or build?
    * Cost Analysis
  4. Building
    * Selecting the Chips
    * Prototypes
    * Manufacture
    * Case
  5. Lessons to Learn
  
## The Bussiness Of IoT

Internet of Things, or IoT, is the buzzword for the concept of connecting things via a network for the purpose of exchanging data. These "things" can be fridges, actuators, cars, pisons in a car, fire alarms, water detection systems... and so on. Connecting these devices allows users to be gather information for alerts, analysis and monitoring of variaous devices. IoT is a huge market, esitmated at $7.1 trillion by 2020 (this number depends greatly on your defintion of the market). Popular applications in this market are:

  * Home automation (lights, tempurature)
  * Security (checking doors, windows, monitoring sounds...)
  * Energy Management (home or industrical scale)
  * Industrial automation (when condition X is sensed, do Y)

The biggest of these applications (or "market segements") is probably Industrial monitoring and automation. Companies want to  know if something starts to show signs of concern. Its is expensive to have an individual go around and check every sensor manually, so generall connected sensors (IoT devices), can report back the current state. 

> A quick example: If it costs a company $500,000 a year to audit its fleet of cars via 3 employees. They probably can save money by attaching an GPS IoT device to each car to read out its location and status. 

## IoT Technologies

The technology for IoT started taking shape around 1999; by ~2015 there were several solutions for an IoT ecosystem. [1](https://en.wikipedia.org/wiki/Internet_of_things) Generally an IoT installment needs three parts:

  1. Sensors (a.k.a. Devices, hardware)
  2. An aggregator (Recieve or Fetch the sensor data)
  3. An alerting/analysis framework (Software)
  
IoT is still very fragmentted- which makes adopting a IoT based solution difficult. Here are a few different IoT solutions you may be familiar with:
  1. [Phidgets](https://www.phidgets.com/) - Modualr devices for sensing over USB
  2. [Z-Wave](http://www.z-wave.com/)/[ZigBee]() - A wireless protocol targeted at the home automation. Solutions like SmartThings, Wink, ADT, and OpenHAB use this.
  3. [Lutron Caseta]() - Lighting controls- their own proprietary connectivity solution.
  4.  SimplySafe - Home monitoring and security, uses its own proprietary solution for communicating between devices.
  5. WEMO - Wifi based IoT plugs
  6. NEST - Wifi based thermostat.
  
Why the fragmentation? There are a number of standards that have attempted to fix this, but they all end up in line with [this xkcd comic](https://xkcd.com/927/). 

## My Experience

As I mentioned before, I spent about 6 months working on a few IoT devices for Intel. Intel was having a problem with there chemical cabinets that fed checmicals to the factory. These ecabinets routinely needed to be refilled. If a checmical ran out the fab would have to shut down while it was refilled. Non of these cabinet had the ability to report how much chemical was left, so it required a person to check these cabinets. This is expensive and maybe the worst job ever (Imagine walking to hundreds of cabients a day just to record readings off them).

Enter IoT devices.

We could replace this mundane job with an automated one be reporting back the amount of chemical left in a cabinet.

## Creating an IoT Edge Device

### Porotyping and Desiging the Schematic

#### Selecting the right chips

For IoT devices you want to select a chip that fullfill your requirements and has low power consumption. For this one I needed 3 things:
  1. USB connectivity
  2. Sensor Connectivity (I decided on using I2C to talk to the sensor)
  3. Power below 100ma (max spike)

#### Getting software

For my time, I used Diptrace. Diptrace is a combination of a schematic editor and PCB editor. I highly recommend a tool that does both. A newer, free, tool is KiCad which has similar functionality. The important thing for selecting your editing software is that it can check connectivity from your schematic to your PCB.

#### Start testing

Once you have a general idea of the chips you think you need, get a few and test them out. Breakout boards and sample code are especially helpful. You can find implementation suggestions in the datasheet for most chips. Companies like [Adafruit](https://www.adafruit.com/) provide a good deal of help in this phase of this project.

You can also get sample chips from some companies, this helps keep the price low. I got sample boards and development tools for Atmel and Microchip (they recently merged).

You can test individual chips with an Arduino board, a Raspberry Pi board, or via  breadboard. For my application a Raspberry Pi board was to large, Arduino was good for testing individual sensors and a breakout board worked perfectly for integrating sensors with my microcontroller.

> Suprisingly Intel is not in the space of creating chips below 32 bits and has a hard time competing with the low power consumption of the 8 bit chips I was using.

You'll need a handfull of resistors and capacitors, multimeter, some soldering equiptment... check out a video on [about setting up a workspace at the EEVBlog.](https://youtu.be/HicV3Z6XLFA) *You probably don't need a ocilliscope to start, contrary to what the video recommends.*

### Designing the PCB

I learned a lot about how to design a PCB from a youtube chanel called the EEVBlog. There is an insanley informative video on there about [designing your PCB for manufacture](https://youtu.be/VXE_dh38HjU).

One thing I did to double check my work was to print out my PCB and place all the components on the printout. This helped me check for clearances. This practice worked well for my small boards, and saved me a messed up production run more than once.

Again datasheets have requirements for PCB placement, be sure to follow these recommendations!

### Prototype runs

You can see a video on how PCB are made (in the factory) [on the EEVBlog on youtube](https://youtu.be/rEB0pl8a5C0).

To make a small production board you will need a PCB, components that go on it, a stencil, solder paste, and a hotplate or oven of some type.

Here is how Sparkfun uses the [hotplate to create devices](https://www.sparkfun.com/tutorials/59).

### Production Runs

## Results of my experience

We did some back of the envelope calculations for my use case, at $10 a sensor, with full deployment across 

power consumption: ~33ma when active

Anaylsis engine >> Gateway >Usb/Wifi> Sensor



One major problem of IoT solutions is power. IoT devices take power, and adding power homes or factories where it was not orgionally intended is hard. Batteries are not much better, current Wifi devices only last a matter of months before requiring the battery to be changed. More conservitive frameworks, like Z-Wave can last up to two years. 
 
 

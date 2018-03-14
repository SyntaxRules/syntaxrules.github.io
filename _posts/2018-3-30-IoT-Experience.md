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

One major problem of IoT solutions is power. IoT devices take power, and adding power homes or factories where it was not orgionally intended is hard. Batteries are not much better, current Wifi devices only last a matter of months before requiring the battery to be changed. More conservitive frameworks, like Z-Wave can last up to two years. 
 
 

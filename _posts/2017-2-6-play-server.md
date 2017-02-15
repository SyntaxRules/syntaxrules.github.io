---
layout: post
title:  "Buying a Cheap Play-Around server"
tags: hpc servers ipmi
---

In my quest to learn more about HPC systems, I quickly realized I need a server that is ipmi compatible. Why? A large majority of handling HPC systems is their administration. I don't have any large simulations, or research to run, so the requirements of my server is kind of unique.

For my purposes, here's what I need:

- IPMI, for remote access, power managements and some out of band sensors
- Minimal CPU power, as running heavly jobs isn't really the purpose of this machine
- 8Gb RAM for Pxe booting
- No Hard drives required, although I might want them later
- Cheap, it can be old, it can be used, it just has to work

## Finding a server

So where do you start? How to find that perfect, cheap, server? I started my search on google, and quickly found [Server Monkey](http://www.servermonkey.com/), a seller of refurbished servers. This is a great way to get a cheap, garenteed to work server. You can get a pretty decient setup there for about $100.

However, you can go even cheaper. Look through Server Monkey, find what they sell for cheap, then head over to [Ebay](http://www.ebay.com). You'll often find various configurations of these servers on e-bay for (sometimes) a fraction of the cost.

## What I got, what I paid

After looking around [Server Monkey](http://www.servermonkey.com/) I found that the Dell PowerEdge 2950 was cheap and IPMI compliant. With a little E-bay searching I found a seller willing to sell me one for $40+$21.99 shipping. The shipping prices are steep for these servers. Because the seller was local, I was able to get them to drop the shipping charges and allow me to pick it up locally. Here's the specs:

- Dell PowerEdge 2950
- Dual Xeon 5160 3.0Ghz
- 16GB Ram
- 6x 3.5" 300GB SAS (at 15k)
- PERC5i Raid controller
- 1 PSU (The box has room for two)

The [Dell PowerEdge 2950](http://www.dell.com/us/dfb/p/poweredge-2950/pd) is old, its not a powerhouse either, but it checks all the boxes for requirements I need.
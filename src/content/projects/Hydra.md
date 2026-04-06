---
title: "Hydra"
description: "Custom 5 head toolchanger 3D-Printer - Fully custom tool changing mechanism integrated with COTS printer parts"
image: "/images/projects/Hydra/20250807_222804.jpg"
startDate: "2025-05-01"
endDate: "2025-09-30"
skills: ["CAD (Onshape)", "Mechanical Design + Integration", "Electronics + Software Integration", "Klipper", "3D-Printing", "Manual Machining"]
sourceLink: "https://github.com/AGB556/Hydra"
---

## Project Overview

Hydra is a fully custom designed 5 toolhead CoreXY gantry 3D printer. It contains a large 310 mm x 310 mm x 240 mm build volume, automatic toolhead changes, auto z leveling, and a custom slicer profile. Designed fully in Onshape in my last year of high school over 100 hours of in CAD development, this printer was the first custom printer that made it out of the CAD stage. I've always wanted to design a toolchanger 3D printer, so with some free time before college, I took the leap. 

## Design Overview

Multi color and multi material printing has long been a passion of mine. This printer takes the best of both worlds, allowing for up to five different colors and/or materials to be used in one print. I made it my goal to fully design this printer in Onshape, allowing me to properly budget space and ensure that everything gets assembled smoothly. 

![Hydra design overview](/images/projects/Hydra/Hydra(3).png)



### Frame and Electronics

The frame of Hydra uses 2020 extrusion combined with 3D printed L brackets and CNC aluminum gussets to create a strong robust frame. It was designed to accomodate the COTS build plate and electronics box in the back while also being optomized to neat measurements to make manufacturing easier. 

I used 2020 extrusion for a few reasons: 
 - interfaces well with the MGN9 rails I wanted to use
 - easy to work with and build a platform off of        
 - extrusion is easier to machine over sheet metal or round tube

<div style="text-align:center;">
  <img src="/images/projects/Hydra/hydraframe.png" alt="hydraframe" style="width:500px;max-width:100%;height:auto;display:inline-block;" />
</div>

The frame ended up being just under 20" x 24", being just big enough to fit the entire 310 mm x 310mm build plate space while still being able to fit through a door easily. 

I went with electronics on the back of the printer for:
 - ease of access
 - more workable space
 - I already had to extend the printer out that way for the toolhead docks 

 I am using the Big Tree Tech (BTT) Octopus Pro v1.1 for my mainboard, a Meanwell LRS-350-24 Power Supply, and a Raspberry Pi 5 for my coprocessor. Note that while the CAD contains a Pi 0 2W, I upgraded to a Pi 5 to install a touchscreen interface, shown below. I am also using the BTT U2C Can converter to communicate with my 5 toolheads over CAN protocol. These were all mounted on a piece of lasercut acrylic that also isolated the build chamber from the electronics to prevent overheating. 

<div style="display:flex;gap:16px;justify-content:center;align-items:center;flex-wrap:wrap;">
  <img src="/images/projects/Hydra/electronics.png" alt="electronics CAD" style="width:48%;max-width:500px;height:auto;" />
  <img src="/images/projects/Hydra/1000017318.jpg" alt="electronics build" style="width:48%;max-width:500px;height:auto;" />
</div>

### Toolhead + Toolchanger Design
The toolhead and toolchanger design was custom designed by me in order to create a simple, reliable mechanism without needing a flying gantry (toolhead on a z axis). 

Looking at the mechanism, it utilizes a sprung servo system that uses a servo to open the latch and a spring to close it and keep the toolhead on the gantry. It also uses a pair of magnets and COTS nozzles to align the toolhead to the holder and keep it aligned. 
<div style="text-align:center;">
  <img src="/images/projects/Hydra/toolheadsection.png" alt="toolheadsection" style="width:500px;max-width:100%;height:auto;display:inline-block;" />
</div>
The toolchanger also holds the part cooling system, which contains a 5015 blower fan and custom ducts to direct the airflow at the optimal angle at the nozzle. The mounts were split up into multiple parts for printability and ease of assembly. 

The toolhead itself was designed around a few core concepts:
 - cost
 - ease of assembly
 - performance
 - horizontal footprint
 - futureproofing
With these constraints, I used the ProtoXtruder 2.0 combined with the Bambu Labs hotend and the BTT EBB 36 toolhead board, which allowed me to create a mostly printed, modular toolhead that had a horizontal footprint of 2.1 inches. This allowed me to fit all 5 toolheads into my limited space on the printer. 
<div style="text-align:center;">
  <img src="/images/projects/Hydra/toolhead.png" alt="toolhead" style="width:500px;max-width:100%;height:auto;display:inline-block;" />
</div>
To simplify my design further, I decided to mount the Z leveling probe to its own modified toolhead, freeing up much needed space on the toolchanger. Additionally, mounts to hold the toolheads when they were not in use that utilized magnets and a steel rod to align and hold the toolhead on were created, mounting above the electronics bay in the back.

<div style="text-align:center;">
  <img src="/images/projects/Hydra/toolheadhome.png" alt="toolheadmount" style="width:500px;max-width:100%;height:auto;display:inline-block;" />
</div>

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:12px;">
  <iframe
    src="https://www.youtube-nocookie.com/embed/rZie5YIdD2w"
    title="Hydra Toolhead Swap"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    referrerpolicy="strict-origin-when-cross-origin"
    allowfullscreen
    style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;"
  ></iframe>
</div>

### Motion System - X, Y, and Z

I utilized a belt driven CoreXY motion system for my gantry, driven by two Nema 17 stepper motors and GT2 Belts on MGN9 linear rails 
### Firmware

The firmware used on Hydra was a fork of Klipper called Kalico, formerly known as Danger Klipper. I made a custom profile and built out individual macros for each individual tool change and homing sequence, optomizing them to be as quick as possible while still having a perfect tool swap rate. 
## Final Results

After assembling the entire printer, wiring it up, and troubleshooting many various problems with the wiring and firmware, Hydra was running smoothly. With my custom Orcaslicer profile, I could run some test multicolor prints, some of which are shown below. 

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:12px;">
  <iframe
    src="https://www.youtube-nocookie.com/embed/r3AWCBeJ4Wg"
    title="Hydra Multicolor Print"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    referrerpolicy="strict-origin-when-cross-origin"
    allowfullscreen
    style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;"
  ></iframe>
</div>


After some tuning, I got a 2 color benchy!

<div style="text-align:center;">
  <img src="/images/projects/Hydra/1000017086.jpg" alt="2colorbenchy" style="width:500px;max-width:100%;height:auto;display:inline-block;" />
</div>

I am currently working on adding and tuning in the other 3 toolheads along with fully enclosing the printer to print more exotic materials. 
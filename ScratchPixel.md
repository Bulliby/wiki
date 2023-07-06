---
title: ScratchPixel
description: 
published: true
date: 2023-07-06T19:38:02.691Z
tags: 
editor: markdown
dateCreated: 2023-06-20T17:07:36.437Z
---

# ScratchPixel

> https://www.scratchapixel.com/

## Right-Handed cordinate system

If we take the bottom left corner of our screen as our origin coordinate system XY (0,0) we can choose to create a Z axis perpendiculare to XY plane in both direction forward or backward the screen plan.

The **Left-Handed** and **Right-Handed** it's just here to remberer in which convention we place our object.

*X,Y,Z* are respectively *thumb,index and middle finger*, the **thumb** must always point to **right**. In this configuration we can see that our **left hand** have a middle finger which points **forward** and with the **right hand** **backward**.

![geo-lefthand-vs-righthand.png](/geo-lefthand-vs-righthand.png)

## Row Major vs Column Major Vector

With **scratchpixel** we use row major vector and matrix.

## Transformation matrix

> **Transformation matrix** are a mean to change of coordinate system.

The camera is an abritrary point who is the center of an other coordiate system.
We can obtain this point with multiplication of the world coordiante with a transformation Matrix.
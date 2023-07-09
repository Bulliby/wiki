---
title: ScratchPixel
description: 
published: true
date: 2023-07-09T14:07:32.953Z
tags: 
editor: markdown
dateCreated: 2023-06-20T17:07:36.437Z
---

# Scratchpixel

> https://www.scratchapixel.com/

## Right-Handed coordinate system

If we take the bottom left corner of our screen as our origin coordinate system XY (0,0) we can choose to create a Z axis perpendiculare to XY plane in both direction forward or backward the screen plan.

The **Left-Handed** and **Right-Handed** it's just here to remberer in which convention we place our object.

*X,Y,Z* are respectively *thumb,index and middle finger*, the **thumb** must always point to **right**. In this configuration we can see that our **left hand** have a middle finger which points **forward** and with the **right hand** **backward**.

![geo-lefthand-vs-righthand.png](/geo-lefthand-vs-righthand.png)

## Row Major vs Column Major Vector

With **Scratchpixel** we use row major vector and matrix.

## Transformation matrix

> **Transformation matrix** are a mean to change of coordinate system.

A matrix is a coordinate system transformation "tool" with the 3 axis of the new coordinate system who represent it's orientation and a translation vector who represent the movement to move the center of one coordinate system to the other.

> **Transformation matrix** can be combined, but in a certain order

We need to apply them in the reverse order who want it to achieve a valid result.
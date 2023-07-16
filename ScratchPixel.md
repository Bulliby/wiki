---
title: ScratchPixel
description: 
published: true
date: 2023-07-16T12:17:00.675Z
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

## Matrix

### Matrix multplication

Matrix multplication need compatible size. In a **row major** matrix. The row size of one matrix must be equal to the column size of the other.

### Row Major vs Column Major Matrix

With **Scratchpixel** we use row major vector and matrix.


### Transformation matrix

> **Transformation matrix** are a mean to change of coordinate system.

A matrix is a coordinate system transformation "tool" with the 3 axis of the new coordinate system who represent it's orientation and a translation vector who represent the movement to move the center of one coordinate system to the other.

$$
\begin{bmatrix}
\color{red}{c_{00}}& \color{red}{c_{01}}&\color{red}{c_{02}}&\color{black}{c_{03}}\\
\color{green}{c_{10}}& \color{green}{c_{11}}&\color{green}{c_{12}}&\color{black}{c_{13}}\\
\color{blue}{c_{20}}& \color{blue}{c_{21}}&\color{blue}{c_{22}}&\color{black}{c_{23}}\\
\color{purple}{c_{30}}& \color{purple}{c_{31}}&\color{purple}{c_{32}}&\color{black}{c_{33}}\\
\end{bmatrix}
\begin{array}{l}
\rightarrow \quad \color{red} {x-axis}\\
\rightarrow \quad \color{green} {y-axis}\\
\rightarrow \quad \color{blue} {z-axis}\\
\rightarrow \quad \color{purple} {translation}\\
\end{array}
$$


> **Transformation matrix** can be combined, but in a certain order

We need to apply them in the reverse order who want it to achieve a valid result.
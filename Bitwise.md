---
title: Bitwise
description: Operations on Bit
published: true
date: 2020-03-28T15:00:53.952Z
tags: lowlevel, binary, bit
---

# Bitwise for CONST

You can use Bitwise operation for handling Flag to use with constant. A good article can be found for **JS** here : [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Flags_and_bitmasks).

I will try to resume and adapt on my need.

```js
const STATUS = {
	ERROR: 1,
  SUCCESS: 1 << 1,
  RUNING: 1 << 2,
  PAUSED: 1 << 3,
  STOPPED: 1 << 4
}
```

We can use this const with **flags** to define what we need in a **single** variable (That's less memory consuming). For example if we want to handle an action on ERROR and STOPPED status
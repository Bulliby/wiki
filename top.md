---
title: Top
description: Configuring and use Linux's top
published: true
date: 2020-04-06T18:31:58.288Z
tags: 
---

# Top

## Controls

- `t` Change rendering of summary area with CPU stats.
- `1` Print CPUS details.
- `c` Show/Hide print the command line who intiate the processus.
- `V` Tree mode
-  `W` Save the current configuration
-  `i` Print only active process.
-  `f` Select fields
-  `x` Highligth the current column
-  `>` or `<` Column change

## Load average

`top - 19:57:23 up 22 min,  1 user,  load average: 0,42, 0,51, 0,50`

* Load average first minute : `0,42`
> It means the CPU for a quad core was 358% idle on average

* Load average 5'st minute: `0.51`
> It means the CPU for a single core was 49% idle on average

* The last measure is for the last 15 minutes : `0.50`

> ref : [techmint](https://www.tecmint.com/understand-linux-load-averages-and-monitor-performance/)
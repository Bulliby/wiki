---
title: Systemd
description: 
published: true
date: 2021-07-07T21:42:19.530Z
tags: sysv, init, systemd, unit, journalctl, systemctl
editor: markdown
dateCreated: 2021-07-07T21:42:19.530Z
---

# Systemd

## Reference

* [units file](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files)

## Introduction

All unit are launch **asynchronously** at time defined in unit file.
* We can add our own unit file in `/etc/systemd/system`
* We can override existing one with a `.conf` file in a folder `toto.service.d` for the toto unit. We can override the file line by line.

## Sections

> They are case sensitive

### [Install]

* `WantedBy=` Permit to start a unit at **boot** in combination with `systemctl enable`.

### [Unit]

* `Description=` Can be seen in `journalctl` or `systemctl status`.
* `After=,Before=` space separated list of units who define before/after which unit this one must start.

### [Service]

`ExecStart`, `ExecStop` are respectively call at start and stop of the Unit.
`RemainAfterExit` permit to consider the unit still active. It's useful for non daemon script or unit without line `ExecStart` present. Like this we are sure that the `ExecStop` can be executed. 

## At stop

If we want unit call something at shutdown of the **unit** we must ensure that the service is active and that the `ExecStop` is furnish. All must be think in reverse order. `After=` became `Before` (vise-versa).
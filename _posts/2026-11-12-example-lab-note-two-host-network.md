---
layout: post
title: "Example lab note: a two-host practice network"
date: 2026-11-12
categories: [labs]
tags: [example, homelab, networking]
description: "Sample lab note for a homelab or tool notebook. The addresses and the command output are illustrative."
---

Sample lab note for a homelab or tool notebook. The addresses and the command output are illustrative.

<blockquote class="example">
  <p><strong>Example.</strong> This is sample content so the layout is easy to copy. Delete this post when you publish a real note.</p>
</blockquote>

## Layout

| Host | Role | Address |
| --- | --- | --- |
| kali | daily driver | 10.10.10.20 |
| placeholder | practice target | 10.10.10.10 |

Both addresses are examples on a private range. Replace them with the hosts you actually run.

```yaml
hosts:
  - name: kali
    address: 10.10.10.20
  - name: placeholder
    address: 10.10.10.10
```

## Checks after boot

Confirm the interface and the route into the lab segment before anything else.

```bash
ip -br addr show dev eth0
ip route
```

```text
eth0             UP             10.10.10.20/24
default via 10.10.10.1 dev eth0
10.10.10.0/24 dev eth0 proto kernel scope link src 10.10.10.20
```

## What belongs here

Lab notes are for setup and tools you want to repeat: a network layout, a package you installed on Kali, a sensor config, a list of which VM is which. A walkthrough of a single target belongs in `writeups`.

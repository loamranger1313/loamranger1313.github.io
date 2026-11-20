---
layout: post
title: "Example writeup: the Placeholder box"
date: 2026-11-18
categories: [writeups]
tags: [example, linux, enumeration]
description: "Sample writeup that shows the front matter, section order, and code-block style. The host and the findings are fake."
---

Sample writeup that shows the front matter, section order, and code-block style. The host and the findings are fake.

<blockquote class="example">
  <p><strong>Example.</strong> This is sample content so the layout is easy to copy. Delete this post when you publish a real note.</p>
</blockquote>

## Scope

- Lab: a personal practice network
- Target: `placeholder.lab` (`10.10.10.10`), a fictional Linux host
- Goal: leave a note the next session can follow

Keep published notes inside work you are allowed to test. Redact passwords, keys, and session tokens before you commit.

## Recon

Put the command in a `bash` fence and the part of the output worth keeping in a `text` fence. Lowercase the language name. Leave line numbers off so a command is easy to copy.

```bash
# Scope is the lab host only.
nmap -sV -p 22,80 --open "10.10.10.10"
```

```text
Starting Nmap 7.94 ( https://nmap.org )
Nmap scan report for placeholder.lab (10.10.10.10)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1
80/tcp open  http    Apache httpd 2.4.58
```

## What turned up

Write the finding in one sentence, then the evidence under it.

- The site on port 80 was a static placeholder page.
- `robots.txt` named a directory, `/notes/`, that was not linked from the homepage.
- A file in that directory contained the string `EXAMPLE-CREDENTIAL-REPLACE-ME`.

## Lesson

- Save the exact command and a trimmed copy of the output.
- End with what you would try first on a similar box.
- Move anything you would not say out loud into a private note, and keep the public writeup redacted.

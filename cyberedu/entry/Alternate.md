**Platform:**  CyberEDU
**Category:**  Forensics
**Difficulty:**  Entry Level
**Date:** 2026-08-12  
**Tags:** forensics, defcamp2024quals

---

## Overview
We are given a .rar archive and the description says that there is a file hidden in it. We are also told that windows is our best friend :)

## Reconnaissance
First we run `strings` command on the archive to see what we get and the following pop up:

![[alternate1.png]]

Taking into consideration that we were told that windows is our friend, we will check the bytes using `xxd` 

![[alternate2.png]]

Here we can see that is  RAR! archive at 0x00, 0x2c reveals the file which we get if we extract the archive, 0x5c shows a service header of type stream, which will help us get to the real flag and 0x62 shows the name of the hidden stream with `:` as NTFS separator

Running `7z x Flag.rar` will extract the whole archive with full paths and we get the hidden stream: 

![[alternate3.png]]
## Flag
`ctf{7ce5567830a2f9f8ce8a7e39856adfe5208242f6bce01ca9af1a230637d65a2d}` 
# unsupported - forensics


## Description

Straight forward challenge, the flag is written on running notepad process. Flag is direct without BHFlagY{} tag.

## Quick overview

The goal of this challenge is to find what is written in **Notepad** from the given **memory dump** using volatility.

## Solution

First thing we need to do is to list the running processes 

!["pslist"](pslist.png)

We can see **Notepad.exe** with **pid=6028**, this information is useful to dump this process memory and then search for any interesting strings, use `python3 /opt/volatility/vol.py -f memdump.mem windows.memmap --dump --pid 6028`

!["bad_strings"](bad_strings.png)

After doing some searches, it seems that the content of **Notepad** is 16-bit little-endian encoded in the **memory map**, that's why we need to use this command `strings -e l pid.6028.dmp | grep "BHflagY"`, where the option `-e l` is used for this purpose, we can see more interesting things here

!["success_strings"](success_strings.png)

remove **BHFlagY{}** and spaces from the data found then submit the correct flag :))




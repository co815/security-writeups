**Platform:**  HackTheBox Academy
**Category:**  Footprinting
**Difficulty:**  Hard
**Date:** 2026-11-06  
**Tags:** footprinting, htb academy, hard

---

## Reconnaissance

1. Enumerate the server carefully and find the username "HTB" and its password. Then, submit HTB's password as the answer.

Again, we will start with an `nmap` scan

![](assets/lab1.png)

Not very useful, lets run a udp scan too

![](assets/lab2.png)

The `snmp` port is of interest for us, first lets find the community string for accesing it

![](assets/lab3.png)

We've found the community string for the snmp agent that runs on some machine/device in that network, lets enumerate it and see what it contains

![](assets/lab4.png)

After running `snmpwalk`, we can see a user and a password in plaintext, we will use these on the other services that are already running on the network to see if this password is somehow reused, first lets ssh 

![](assets/lab5.png)

Ok we need a key, lets login into the mailboxes see if there are anything useful there

![](assets/lab6.png)

Indeed, there was the key in the mailbox, copy it, place it in a file and give permissions to it then ssh using the key

![](assets/lab7.png)

After ssh-ing into the machine, we see something interesting, the mysql history for commands, meaning that there is a database on this machine that can be accessed, lets do that with the credentials for tom

![](assets/lab8.png)

There is a database for users, lets see if there is any user named `HTB` 

![](assets/lab9.png)

## Flag / Root

1. `cr3n4o7rzse7rzhnckhssncif7ds` 
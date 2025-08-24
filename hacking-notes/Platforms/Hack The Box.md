---
aliases:
  - HTB
tags:
  - Platform
  - MOC
web: https://hackthebox.com
banner: "![[htb-banner3.jpeg]]"
---
> [!INFO] Hack The Box
> Hack The Box (HTB) is a cybersecurity platform that provides vulnerable machines and practical challenges to learn and train ethical hacking skills in a safe environment.
^description

> [!FLAG] Machines
> 
> ```dataview
> TABLE WITHOUT ID
>     file.link AS Note,
>     difficulty AS Difficulty,
>     dateformat(date(file.cday), "ccc dd, LLL. yyyy") AS Beginning
> FROM
> 	[[#]] AND
> 	!"Resources"
> WHERE
> 	platform = [[Hack The Box]]
> SORT
> 	file.name ASC
> ```
^machines

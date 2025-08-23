---
aliases:
  - HTB
tags:
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
>     file.link AS Nota,
>     dificultad AS Dificultad,
>     dateformat(date(file.cday), "ccc dd, LLL. yyyy") AS Inicio
> FROM
> 	[[#]] AND
> 	!"00 - Recursos"
> WHERE
> 	plataforma = [[Hack The Box]]
> SORT
> 	file.name ASC
> ```
^machines

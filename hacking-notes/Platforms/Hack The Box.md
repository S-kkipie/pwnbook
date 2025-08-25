---
aliases:
  - HTB
tags:
  - Platform
  - MOC
web: https://hackthebox.com
banner: "![[htb-banner7.jpg]]"
---
> [!INFO] Hack The Box
> Hack The Box (HTB) is a cybersecurity platform that provides vulnerable machines and practical challenges to learn and train ethical hacking skills in a safe environment.
^description

> [!INFO] Hack the box provides different platforms to practice:

## HTB LABS
It's a platform to practice your hacking skills on real-world applications.
Each lab contains different running services, some of which are vulnerable to certain [[Exploit]]

## HTB ACADEMY
Provides some [[HTB Module|Modules]] and [[HTB Path|Paths]] for learning and certifying your skills, they are very very useful for your career.

## HTB CTF
It's a platform where you can practice and improve your [[CTF|CTFs]] knowledge and showcase your skills.


> [!FLAG] Machines
> 
> ```dataview
> TABLE WITHOUT ID
>     file.link AS Note,
>     difficulty AS Difficulty,
>     status As Status,
>     dateformat(date(file.cday), "ccc dd, LLL. yyyy") AS Beginning
> 	
> 	    
> FROM
> 	[[#]] AND
> 	!"Resources"
> WHERE
> 	platform = [[Hack The Box]]
> SORT
> 	file.name ASC
> ```
^machines

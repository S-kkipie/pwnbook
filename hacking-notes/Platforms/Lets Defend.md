---
tags:
  - "#Platform"
  - "#MOC"
web: https://letsdefend.io/
banner: "![[letsdefend-social-banner.png]]"
---
> [!INFO] LetsDefend  
> **LetsDefend** is a blue-team focused cybersecurity platform that offers realistic Security Operations Center (SOC) environments to learn, practice, and improve defensive skills in a safe, hands-on way.  

> [!INFO] LetsDefend provides different platforms to practice:
>
> ## LetsDefend SOC  
> A live Security Operations Center simulation where you can investigate real-world style incidents, analyze alerts, and respond to threats as if you were on a professional SOC team.  
>
> ## LetsDefend Academy  
> Offers structured **Modules** and **Learning Paths** that teach incident response, threat hunting, and digital forensics, helping you build and certify practical defensive skills for your cybersecurity career.  
>
> ## LetsDefend Challenges  
> A set of hands-on defensive security challenges and mini-labs to sharpen your skills in areas such as malware analysis, log analysis, and threat detection.


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
> 	platform = [[Lets Defend]]
> SORT
> 	file.name ASC
> ```
^machines

# CTFs Activity
## Last Machines

```dataview
TABLE WITHOUT ID
	file.link AS Machine,
	plataforma AS Platform,
	dateformat(date(file.mtime), "ccc dd, LLLL") AS Beginning
FROM
	"Machines"
LIMIT
	5
SORT
	file.cday DESC
```

## Pending Machines

```dataview
TABLE WITHOUT ID
    platform AS Platform,
	rows.file.link AS Machine
FROM
    "Machines" AND
	!#Completed
LIMIT
	5
GROUP BY
    platform
SORT
	file.ctime
```

# Notes Use

## Incoming notes
```dataview
TABLE WITHOUT ID
    file.link AS Nota,
    length(file.inlinks) AS Conexiones
FROM
    !"00 - Recursos" AND
    !#MOC
LIMIT
	10
SORT
    length(file.inlinks) DESC,
    file.link ASC
```

## Outgoing notes
```dataview
TABLE WITHOUT ID
    file.link AS Note,
    length(file.outlinks) AS Connections,
    file.outlinks AS Outgoing
FROM
    !"00 - Recursos"
LIMIT
	10
SORT
    length(file.outlinks) DESC,
    file.link ASC
```

## MOCs
The Most Used [[MOC|MOCs]].
```dataview
TABLE WITHOUT ID
    file.link AS MOC,
    length(file.inlinks) AS Incoming
FROM
    #MOC 
LIMIT
	10
SORT
    length(file.inlinks) DESC,
    file.link ASC
```


# Registry

## Notes created today
```dataview
TABLE WITHOUT ID
    file.link AS "Note",
    dateformat(date(file.ctime), "HH:mm") AS Time
WHERE
    date(today) = date(file.cday) AND
	!containsword(file.name, ".excalidraw")
LIMIT
	20
SORT
	file.ctime DESC
```


## Last modifications

```dataview
TABLE WITHOUT ID
    file.link AS "Note",
    dateformat(date(file.mtime), "ccc dd, LLL (HH:mm)") AS Date
LIMIT
	20
WHERE
	!containsword(file.name, ".excalidraw")
SORT
	file.mtime DESC
```

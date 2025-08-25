# TO-DO
```dataview
TABLE WITHOUT ID
    file.link As Name,
    tags[0] AS Type
FROM 
	!"Resources"
WHERE
	contains(file.tags, "#TO-DO") or
	status = "Incomplete"
LIMIT
	10

```

# Machines Activity
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

# Journal Resume
```dataview
TABLE WITHOUT ID
	file.link AS Note,
    file.aliases[2] AS Date,
    description AS Description
FROM
    "Journal"
LIMIT
	10
SORT
    length(file.inlinks) DESC,
    file.link ASC
```

# Notes Use

## Incoming notes
```dataview
TABLE WITHOUT ID
    file.link AS Nota,
    length(file.inlinks) AS Conexiones
FROM
    !"Resources" AND
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
    length(file.outlinks) AS Connections

FROM
    !"Resources"
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
    #MOC and
    !"Resources"
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

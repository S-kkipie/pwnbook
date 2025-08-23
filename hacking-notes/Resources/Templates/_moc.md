---
aliases: 
tags:
  - "#MOC"
---
> [!INFO] <% tp.file.title %>
> Description of the  [[MOC]].
^description

```dataview
TABLE WITHOUT ID
    file.link AS Note,
    tags AS Tags
FROM
    [[#]] AND
    !"00 - Recursos"
SORT
    length(file.inlinks) DESC,
    file.name ASC
```
^conections

# References
- 
- 

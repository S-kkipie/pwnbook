---
aliases:
  - <% tp.date.now("DD/MM/YYYY", 0, tp.file.title, "YYYY-MM-DD") %>
  - <% tp.date.now("DD-MM-YYYY", 0, tp.file.title, "YYYY-MM-DD") %>
  - <% tp.date.now("dddd DD, MMMM YYYY", 0, tp.file.title, "YYYY-MM-DD") %>
banner: "![[anything_banner2.jpg]]"
---
> #tutorial : Some text for today 

# Registry

> [!SUCCESS] Notes created at *<% tp.date.now("dddd DD, MMMM YYYY", 0, tp.file.title, "YYYY-MM-DD") %>*
> ```dataview
> TABLE WITHOUT ID
>     file.link AS "Note",
>     dateformat(date(file.ctime), "HH:mm") AS Time
> WHERE
>     date(this.file.name) = date(file.cday) AND
>     this.file.name != file.name
> SORT file.cday DESC
> ```
^registry

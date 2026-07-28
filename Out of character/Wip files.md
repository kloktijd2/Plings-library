

dataview

```dataview
TABLE
	file.link AS "Note",
	length(file.inlinks) AS "Incoming links"

FROM #wip

SORT length(file.inlinks) DESC

```



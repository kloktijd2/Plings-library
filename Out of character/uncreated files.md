dataview

```dataview
TABLE
	length(rows) AS "Notes",
	rows.file.link AS "Referenced in"

FLATTEN unique(file.outlinks) AS o
WHERE !contains(meta(o).path, ".")

GROUP BY o AS "Uncreated file"

SORT length(rows) DESC
LIMIT 200
```



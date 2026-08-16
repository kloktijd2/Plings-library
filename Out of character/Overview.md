```dataviewjs
// Count all notes
const allNotes = [...dv.pages()];
const totalNotes = allNotes.length;

// Count notes tagged #wip
const wipNotes = allNotes.filter(p => p.file.etags.includes("#wip")).length;

// Notes excluding #wip
const nonWipNotes = totalNotes - wipNotes;

// Collect unique unresolved links
const orphanedLinks = new Set();

for (const page of allNotes) {
    const links = page.file.outlinks ?? [];

    for (const link of links) {
        const exists = app.metadataCache.getFirstLinkpathDest(
            link.path,
            page.file.path
        );

        if (!exists) {
            orphanedLinks.add(link.path);
        }
    }
}

// Display results
dv.table(
    ["Metric", "Count"],
    [
        ["Notes", totalNotes],
        ["#wip Notes", wipNotes],
        ["Notes (excluding #wip)", nonWipNotes],
        ["Unique Orphaned Links", orphanedLinks.size],
        ["Notes + Unique Orphaned Links", totalNotes + orphanedLinks.size]
    ]
);
```

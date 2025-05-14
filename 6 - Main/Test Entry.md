--- 
tags:
- "#glossar"
related: [[Test Entry]]
topic: German 
---


# Definition
This is the definition content of the note.

```dataview
const tagName = "#glossar"; // The tag to group notes by
const mySectionName = "Definition"; // The section to extract

/**
 * Extracts the content of a given Markdown section from a string.
 * @param {string} markDownString - The Markdown content.
 * @param {string} sectionName - The section name to search for.
 * @returns {string} - The content of the section, or "<span>-</span>" if not found.
 */
const getSectionContent = (markDownString, sectionName) => {
    const sectionPattern = new RegExp("#{1,5}\\s*" + sectionName);
    const nextSectionPattern = new RegExp("#{1,5}");
    let sectionHeaderLength;
    if (sectionPattern.test(markDownString)) {
        sectionHeaderLength = markDownString.match(sectionPattern)[0].length;
    } else {
        return "<span>-</span>";
    }
    const startingIndex = markDownString.search(sectionPattern);
    const endingIndex = markDownString.substring(startingIndex + sectionHeaderLength)
        .search(nextSectionPattern);
    if (endingIndex == -1) {
        return markDownString.substring(startingIndex + sectionHeaderLength).trim();
    } else {
        return markDownString.substring(
            startingIndex + sectionHeaderLength,
            startingIndex + sectionHeaderLength + endingIndex
        ).trim();
    }
};

// Group notes by the first character of the note's name
const groupedTableEntries = dv.pages(tagName).groupBy(note => note.file.name.charAt(0).toUpperCase());

for (let group of groupedTableEntries) {
    const tableEntries = await Promise.all(
        group.rows.map(async (note) => {
            const content = await dv.io.load(note.file.path); // Load the note content
            return {
                name: note.file.name,
                link: note.file.link,
                definition: getSectionContent(content, mySectionName),
                topic: note.topic,
                related: note.related
            };
        })
    );

    // Render the table
    dv.header(3, group.key); // Group Header (First Character of Note Name)
    dv.table(
        ["Begriff", "Definition", "Thema", "Verwandt"], // Column Headers
        tableEntries
        .sort((entryA, entryB) => entryA.name.localeCompare(entryB.name)) // Sort alphabetically
        .map(entry => [entry.link, entry.definition, entry.topic, entry.related]) // Table Data
    );
}

```

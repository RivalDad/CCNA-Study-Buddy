---
tags: [ccna, readme]
type: readme
---
# How to Use This CCNA Vault

[[00 - CCNA Home|← CCNA Home]]

## Purpose

This vault is designed as a **shareable technical reference** for the Jeremy's IT Lab CCNA 200-301 lessons covered so far (Days 1-17), while keeping the physical notebook intentionally short.

The division of labor is:

```text
Obsidian vault → complete organized reference
Paper notebook → high-value facts, formulas, commands, memory anchors
Packet Tracer  → applied practice and troubleshooting evidence
```

## Folder Layout

```text
01 - Lessons     One detailed note per lecture video
02 - Labs        One page per Packet Tracer/lab video
03 - MOCs        Topic maps that group related lessons
04 - Reference   Commands, subnetting, packet walks, glossary, troubleshooting
05 - Templates   Reusable lesson/lab templates
06 - Study       Review material and notebook roll-ups
99 - Optional    Optional Dataview/CSS enhancements
```

## Obsidian Features Used

### Wikilinks

Concepts link to related lessons/reference pages using `[[wikilinks]]`. This makes backlinks and Graph View useful rather than decorative.

### MOCs — Maps of Content

MOCs group **like data together** even when the course introduces it on different days. For example, ARP, switching, interfaces, and VLANs all appear together in the Ethernet MOC.

### Callouts

The notes preserve the color logic used in the paper notebook:

- 🔵 `info` = facts/numbers
- 🟢 `success` = core concepts
- 🟠 `warning` = behavior/rules
- 🟣 `example` = commands/examples
- 🔴 `danger` = traps/must remember

### Embedded Highlights

Every lesson has a `## Notebook Highlights` section. [[06 - Study/CCNA Notebook Highlights]] embeds those sections directly, so there is one auto-updating review page without copying data.

### Mermaid

Protocol flows and packet walks use Mermaid diagrams that render natively in Obsidian.

### YAML Properties

Each page has frontmatter for day, topic group, type, status, mastery, and source. This is readable without plugins and can also be queried by Dataview.

### Canvas

[[CCNA Course Map.canvas]] provides a graphical course map.

## Optional Enhancements

Nothing in the main vault requires a community plugin.

If you use **Dataview**, open [[99 - Optional/Dataview Dashboard]] for an automatically generated lesson table.

An optional CSS snippet is included at:

```text
99 - Optional/Obsidian CSS/ccna-notes.css
```

Copy it into your vault's `.obsidian/snippets/` folder and enable it in **Settings → Appearance → CSS snippets** if you want the callout palette tuned to the notebook colors.

## Sharing These Notes

The lesson notes are **original summaries**, not copied transcripts. Each lecture page links to the corresponding Jeremy's IT Lab video and a synchronized transcript/chapter index so a reader can verify context or watch the source.

When sharing, keep [[Source Attribution]] with the notes.

## Recommended Study Loop

```text
1. Watch lesson
2. Read/annotate detailed Obsidian page
3. Write only Notebook Highlights by hand
4. Complete lab without copying commands first
5. Verify with show commands
6. Explain one packet walk aloud
7. Use Active Recall section later without looking at answers
```

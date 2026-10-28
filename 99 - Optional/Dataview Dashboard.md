---
tags: [ccna, optional, dataview]
type: optional
---
# Optional Dataview Dashboard

[[00 - CCNA Home|← Home]]

This page requires the community **Dataview** plugin. The rest of the vault does not.

## Lessons

```dataview
TABLE WITHOUT ID
  link(file.link, "Day " + string(day) + " — " + file.name) AS Lesson,
  topic_group AS Topic,
  status AS Status,
  mastery AS Mastery
FROM "01 - Lessons"
WHERE type = "lecture"
SORT order ASC
```

## Labs

```dataview
TABLE WITHOUT ID
  file.link AS Lab,
  parent_lesson AS "Parent Lesson",
  status AS Status
FROM "02 - Labs"
WHERE type = "lab"
SORT order ASC
```

## Notes Needing Review

```dataview
LIST
FROM "01 - Lessons"
WHERE mastery = "weak" OR mastery = "shaky" OR status != "studied"
SORT order ASC
```


## Core Verbs

### Create New Columns

To make create columns starting with constant values those need to be expanded to static columns using with `const`
```
df.createColumn("user_id") { const("id") + nrow }

```


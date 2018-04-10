
## Core Verbs

### Create New Columns

To make create columns starting with constant values those need to be expanded to static columns using with `const`
```
df.createColumn("user_id") { const("id") + nrow }

```






{% hint style="info" %}
 `sleepData.sortedBy{ "order" }`
{% endhint %}




## Examples

1. Add a suffix to some column names
```kotlin
// first select column names to be altered
irisData.names.filter { it.startsWith("Sepal") }.map {
    // second, apply renaming
    oldName -> irisData.rename(oldName to ("My" + oldName)) 
}
```

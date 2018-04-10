{% hint style="info" %}
For a primer on tidy data read http://garrettgman.github.io/tidying/
{% endhint %}


# Example: Data Reshaping with `krangl`

```kotlin
val climate = dataFrameOf(
        "city", "coast_distance", "1995", "2000", "2005")(
        "Dresden", 400, 343, 252, 423,
        "Frankfurt", 534, 534, 435, 913)
```

```
     city   coast_distance   1995   2000   2005
  Dresden              400    343    252    423
Frankfurt              534    534    435    913
```

```kotlin
climate. gather("year", "rainfall", columns = { matches("[0-9]*")} )
```

```
     city   coast_distance   year   rainfall
  Dresden              400   1995        343
Frankfurt              534   1995        534
  Dresden              400   2000        252
Frankfurt              534   2000        435
  Dresden              400   2005        423
Frankfurt              534   2005        913
```

???

`colummns` use function literals again, with column names type as receiver

---
# Example: Data Ingestion with `krangl`

```kotlin
dataFrameOf("user")("brandl,holger,37")
        .apply { print() }
        .separate("user", listOf("last_name", "first_name","age"), convert = true)
        .apply { print() }
        .apply { glimpse() }
```

```
            user
brandl,holger,37
```
-----
```
last_name   first_name   age
   brandl       holger    37
```
-----
```
DataFrame with 1 observations
last_name  : [Str]	, [brandl]
first_name : [Str]	, [holger]
age        : [Int]	, [37]
```


This is the [manual](https://krangl.gitbook.io/docs/) for [krangl](https://github.com/holgerbrandl/krangl).

`krangl` is a {K}otlin library for data w{rangl}ing. By implementing a grammar of data manipulation using a modern functional-style API, it allows to filter, transform, aggregate and reshape tabular data.

`krangl` tries to become what pandas is for `python`, and `readr`+`tidyr`+`dplyr` are for R.

`krangl` is open-source and [developed](https://github.com/holgerbrandl/krangl) on github.


Features
--------

* Filter, transform, aggregate and reshape tabular data
* Modern, user-friendly and easy-to-learn data-science API
* Reads from plain and compressed tsv, csv, json, or any delimited format with or without header from local or remote
* Supports grouped operations
* Ships with JDBC support
* Tables can contain atomic columns (int, double, boolean) as well as object columns
* Reshape tables from wide to long and back
* Table joins (left, right, semi, inner, outer)
* Cross tabulation
* Descriptive statistics (mean, min, max, median, ...)
* Functional API inspired by [dplyr](http://dplyr.tidyverse.org/), [pandas](http://pandas.pydata.org/), and Kotlin [stdlib](https://kotlinlang.org/api/latest/jvm/stdlib/index.html)



Further more it provides methods to go back and forth between untyped and typed data.

# Example

```kotlin
flights
    .groupBy("year", "month", "day")
    .select({ range("year", "day") }, { listOf("arr_delay", "dep_delay") })
    .summarize(
            "mean_arr_delay" to { it["arr_delay"].mean(removeNA = true) },
            "mean_dep_delay" to { it["dep_delay"].mean(removeNA = true) }
    )
    .filter { (it["mean_arr_delay"] gt  30)  OR  (it["mean_dep_delay"] gt  30) }
```

And the same snippet written in `dplyr`:

```r
flights %>%
    group_by(year, month, day) %>%
    select(year:day, arr_delay, dep_delay) %>%
    summarise(
        mean_arr_delay = mean(arr_delay, na.rm = TRUE),
        mean_dep_delay = mean(dep_delay, na.rm = TRUE)
    ) %>%
    filter(mean_arr_delay > 30 | mean_dep_delay > 30)
```

The biggest different are the comparison operators, which Kotlin does not allow to [be overridden](https://kotlinlang.org/docs/reference/operator-overloading.html) in a vectorized way.



And the same in `pandas`. **{PR needed here}**


# krangl-gitbook

The [manual](https://krangl.gitbook.io/docs/) for krangl.

`krangl` is open-source and [developed](https://github.com/holgerbrandl/krangl) on github.



## Introduction


`krangl` is inspired by the excellent R-package [`dplyr`](http://dplyr.tidyverse.org/). Here's an example using airline on-time data for all [flights departing NYC in 2013](https://cran.r-project.org/web/packages/nycflights13/index.html).

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


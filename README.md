This is the [manual](https://krangl.gitbook.io/docs/) for krangl.

`krangl` is a {K}otlin library for data w{rangl}ing. By implementing a grammar of data manipulation using a modern functional-style API, it allows to filter, transform, aggregate and reshape tabular data.

`krangl` tries to become what pandas is for `python`, and `readr`+`tidyr`+`dplyr` are for R.

`krangl` is open-source and [developed](https://github.com/holgerbrandl/krangl) on github.



## Introduction

## Can we build data science workflows with Kotlin?

First, should we? Yes, because

* R & Python fail to be scalable & robust solutions for data science
* Java is known for great dependency tooling & scalability
* Java as a language is less well suited for data-science (cluttered, legacy bits)


In Febuary 2018 Kotlin v1.0 was released. Designed with DSLs in mind it comes alongs With great features language such Type Inference, Extension Functions, Data Classes, or Default Parameters, making it a perfect choice to do *data science on the JVM*.

`krangl` is inspired by the excellent R-package [`dplyr`](http://dplyr.tidyverse.org/). Here's an example using airline on-time data for all [flights departing NYC in 2013](https://cran.r-project.org/web/packages/nycflights13/index.html).

## To type or not to type?

* _Static types_ are cool, but most data has no type
* It's more robust/fun to use types and they allow for better design
* Many data attributes are very fluent

```kotlin
data class Employee(val id:Int, val name:String) 
val staffStats = listOf(Employee(1, "John"), Employee(2, "Anna"))  
    .predictNumSickDays()     // new type!
    .addPerformanceMetrics()  // new type!
    .addSalaries()            // new type!
    .correlationAnalysis()    // odd generic signature :-|
```
* R/python lack static typing, which make such workflows more fluent/fun to write

```r
staff %>% 
    mutate(sick_days=predictSickDays(name)) %>%   # table with another column
    left_join(userPerf) %>%                       # and some more columns
    left_join(salaries) %>%                       # and even more columns
    select_if(is.numeric) %>%                     
    correlate(type="spearman")                    # correlate numeric attributes
```


Defining types is a tedious process.

`krangl` allows to mix typed and untyped data in a tablular data structure:

`val dataFrame : DataFrame =`

| `employee:Employee` | `sales:List<Sale>` | `age:Int` | `address:String` | `salary:Double`   |
|:-----|:-------------|:----|:-----|:--|
| `Employee(23, "Max")` |    `listOf(Sale(...), Sale())` |   23  | "Frankfurt"     |  50.3E3 |
| ... |  ...    | ...    |  ...    | ...  |


It implements a  `pandas`/`tidyverse` like API to create, manipulate, reshape, combine and summarize  data frames

```kotlin
// aggregations like
dataFrame.groupBy("age").count()
dataFrame.summarize("mean_salary"){ mean(it["salaray"])}

// integration like
val df: DataFrame = dataFrame.leftJoin(otherDF)

// transformations like
dataFrame.addColumn("intial"){ it["employee"].map<Employee>{ it.name.first() }}
```


Further more it provides methods to go back and forth between untyped and typed data.


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


## Why doesn't krangl provide vectorized comparison operators?

Some (`+`, `-`, `*`, `!`) can be overridden for collections, but others cannot (e.g. all arithmetic and boolean comparison ops)

No vectorization for `>`,  `&&` `==`, etc. in table forumlas → Use function calls or not so pretty `gt`, `AND`, `eq`, etc.


## Can we build data science workflows with Kotlin?

First, should we? Yes, because

* R & Python fail to be scalable & robust solutions for data science
* Java is known for great dependency tooling & scalability
* Java as a language is less well suited for data-science (cluttered, legacy bits)


In Febuary 2018 Kotlin v1.0 was released. Designed with DSLs in mind it comes alongs With great features language such Type Inference, Extension Functions, Data Classes, or Default Parameters, making it a perfect choice to do *data science on the JVM*.


## Further Reading?

[`krangl` presentation at Kotlin-Night in Frankfurt (March 2018)](https://holgerbrandl.github.io/kotlin4ds_kotlin_night_frankfurt//emerging_kotlin_ds_ecosystem.html)


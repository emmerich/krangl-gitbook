# `kravis` - https://github.com/holgerbrandl/kravis

Early pre-alpha!! :-)

`kravis` implements a grammar to create a wide range of plots using a standardized set of verbs.

`kravis` builds on top of `krangl

It implements a Kotlin DSL wrapper around [vega-lite](https://vega.github.io/vega-lite/):


.left-column60[

```kotlin
import krangl.*
import kravis.*

val movies = DataFrame.fromJson("movies.json")

plotOf(movies) {  mark = Mark(circle)
 
 encoding(x,"IMDB_Rating",binParams=BinParams(10))
 encoding(y, "Rotten_Tomatoes_Rating", bin = true)
 encoding(size, aggregate = Aggregate.count)
}
```

![](.data_vis_images/kravis_plot.png)


### Plot Immutablity.

Plots are -- similar to krangl data-frames -- immutable.

```

```

# Other options

There are great other libaries available, which typically don't work with `krangl` yet, but provide awesome ways to visualize data.

* [Vegas](https://github.com/vegas-viz/Vegas) Vega-lite wrapper, aims to be the missing MatPlotLib for Scala + Spark
* [data2viz](https://github.com/data2viz/data2viz) is a multi platform data visualization library with comprehensive DSL
* [XChart](https://github.com/timmolter/XChart) is a light-weight Java library for plotting data
* [Kubed](https://github.com/hudsonb/kubed/) is a Kotlin library for manipulating the JavaFX scenegraph based on data.
* [TornadoFX](https://github.com/edvin/tornadofx/wiki/Charts) provides some Kotlin wrappers around JavaFX
* [Jzy3d](http://www.jzy3d.org/) is an open source java library that allows to easily draw 3d #surfaces, scatter plots, bar charts
* [plotly-scala](https://github.com/alexarchambault/plotly-scala) which provides scala bindings for plotly.js and works within jupyter
* [grafana](https://grafana.com/) is an open platform for beautiful analytics and monitoring

However, none of the options above provides coherent `ggplot2` like framework with grammar for graphics, to build plots with

> `layers` + `aesthetics` + `coordinates system` + `transformations` + ` facets`

Which reads as `one or more layers` + `map variables from data space to visual space` + `coordinates system` + `statistical transformations` + `optional facets`. That's the way.



Also, JVM graphics device project that works from Kotlin REPL, in Intellij, and in jupyter notebooks



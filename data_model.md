# Data model of `krangl`


What is a DataFrame?

> A "tabular" data structure representing cases/records (rows), each of which consists of a number of observations or measurements (columns) [reference](https://github.com/mobileink/data.frame/wiki/What-is-a-Data-Frame%3F)

And by mapping this defintion to Kotlin code, we obtain the core abstraction of `krangl`:
```kotlin
interface DataFrame {
    val cols: List<DataCol>
}

abstract class DataCol(val name: String) {
    abstract fun values(): Array<*>
}
```
* Implemented as column model to allow for vectorization where possible
* Column implementations using nullable types `String?`, `Int?`, `Double?`, `Boolean?` and `Any?`
* Internal length and type consistency checks (e.g. prevent duplicated column names)


# Get your data into krangl


It allows to read from tsv, csv, json, jdbc, e.g.

```kotlin
val users = dataFrameOf(
    "firstName", "lastName", "age", "hasSudo")(
    "max", "smith" , 53, false,
    "eva", "miller", 23, true,
    null , "meyer" , 23, null)
 
val tornados = DataFrame.readCSV(pathAsStringFileOrUrl)
tornados.writeCSV(File("tornados.txt.gz"))
```

* Guess column types & default parameters
* Built-in missing value support

Convert any iterable into a data-frame via extension function + reflection

```kotlin
data class Person(val name:String, val address:String)
val persons : List<Person> = ...

val personsDF: DataFrame = persons.asDataFrame() 
```

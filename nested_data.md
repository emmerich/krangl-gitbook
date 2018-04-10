# Digest objects into attribute columns

Cherry-pick properties with `Iterable<T>.deparseRecords`
```kotlin
val deparsedDF = records.deparseRecords { mapOf(
    "age" to it.age, 
    "weight" to it.mean_weight
) }

```

Be lazy and use reflection
```kotlin
data class Person(val name:String, val age:Int)
val persons :List<Person> = listOf(Person("Max", 23), Person("Anna", 43))

val personsDF: DataFrame = persons.asDataFrame() 
personsDF
```

```
age   name
 23   Max
 43   Anna
```

# List/object columns

`krangl` supports arbitrary types per column

```kotlin
val persons: DataFrame = dataFrameOf("person")(persons) 
persons
```

```
                      person
   Person(name=Max, age=23)
   Person(name=Anna, age=43)
```

```kotlin
personsDF2.glimpse()
```

```
DataFrame with 2 observations
person	: [Any]	, [Person(name=Max, age=23), Person(name=Anna, age=43)]
```



# Unfold objects into columns

* similar to `separate()` but for object columns


```kotlin
data class Person(val name:String, val age:Int)
val persons :Iterable<Person> = listOf(Person("Max", 22), Person("Anna", 23))

val df : DataFrame = dataFrameOf("person")(persons)

df.names
```
```
["person"]
```
--

Expand properties of `person` into columns via reflection

```kotlin
var personsDF = df.
    unfold<Person>("person", keep=true) 
    // unfold<Person>("person", select=listOf("age"))
    
personsDF.names   
```

```
["person", "name", "age"]
```


# Let krangl define the schema


Infer a schema with

```kotlin
irisData.printDataClassSchema("Iris")
```
which makes krangl to __print__ the Kotlin data class schema for data frame:

```kotlin
data class Iris(val sepalLength: Double, val sepalWidth: Double, val petalLength: Double, 
                val petalWidth: Double, val species: String)
                
val records: Iterable<Iris> = irisData.rowsAs<Iris>()
```

Paste it back into workflow code and continue with typed objects!

```kotlin
records.take(1)
```

```
[ Iris(sepalLength=5.1, sepalWidth=3.5, petalLength=1.4, petalWidth=0.2, species=setosa) ]
```

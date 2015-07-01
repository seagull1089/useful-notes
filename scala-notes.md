Notes from the NoMonads presentation
====
https://www.parleys.com/tutorial/unsung-heroes-less-fashionable-patterns-scala
* type early type often
* case objects -- enum replacements?
* Loan pattern 
```scala
def withIterator[A](filename:String)(fn:Iterator[String] => A): A = { 
  val source = Source.fromFile(filename)
  try{ 
    val iter = source.getLines()
    fn(iter)
  }finally source.close()
}
// usage: 
withIterator("hello.txt"){ 
  iter => iter.map(_.toUpperCase).toList
} 
```

https://www.parleys.com/tutorial/scala-tricks
* http://www.agiledeveloper.com
* open a file
```scala
import scala.io._ 
println(Source.fromFile("sample.scala").mkString)

// sample code.
class Car(val year:Int, var miles:Int)
var car = new Car(2013,0)

// sample scoped
def createPerson() = { 
  new {
    var first = "James" 
    var last = "Bond"
  }
}

var doubleOSeven = createPerson()
println(doubleOSeven.first, doubleOSeven.last)
```

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

// anonymous objects
def createPerson() = { 
  new {
    var first = "James" 
    var last = "Bond"
  }
}

var doubleOSeven = createPerson()
println(doubleOSeven.first, doubleOSeven.last)
```
* Implicit methods to create smaller code. 
```scala
println(2.days.ago)
class IntUtil(val number:Int){ 
  def days = this
  
  def ago = { 
    var today = Calendar.getInstance
    today.add(Calendar.DAY_OF_MONTH, -number)
    today.getTime()
  }
}

implicit def someDummyFunction(num:Int)  = new IntUtil(num)
```
* SICP -- proceduce vs process
```scala
@scala.annotation.tailrec
def factorial(fact: BigInt, n: BigInt) :BigInt = if (n == BigInt(1)) fact else factorial(fact*n, n-1)
factorial(1,5000)
```
* Traits
```scala
trait Friend{ 
  val name:String
  def listern = println("I'm" + name + "listening")
} 
class Human(val name: String) extends Friend
class Animal(val name:String)
class Dog(override val name:String) extends Animal(name) with Friend
class Cat(oveeride val name:String) extends Animal(name)

// The cat doesn't extend Friend here. 
val clinton = new Cat("Clinton")
clinton.listen // Error

// You can extend Friend here. 
val clinton = new Cat("Clinton") with Friend
clinton.listen // success

```
* Decorator Pattern
```scala 
abstract class Writer { 
  def write(msg:String)
}

class StringWriter extends Writer { 
  val target = new StringBuilder()
  override def write(msg:String) = { 
    target.append(msg)
  }
  override def toString = target.toString
}

trait UppercaseFilter extends Writer { 
  abstract override def write(msg:String) = { 
    super.write(msg.toUpperCase())
  }
}

trait ProfanityFilter extends Writer {
  abstract override def write(msg:String) = {
    super.write(msg.replace("stupid", "s*****"))
  }
}

writeStuff(new StringWriter) // this is stupid
writeStuff(new StringWriter with UpperCaseFilter) // THIS IS STUPID
writeStuff(new StringWriter with ProfanityFilter) // this is s****
writeStuff(new StringWriter with UpperCaseFilter with ProfanityFilter) // "THIS IS S****" 

```
* Lens in scala - http://koff.io/posts/292173-lens-in-scala - is an abstraction to deal with updating of complex immutable nested objects.




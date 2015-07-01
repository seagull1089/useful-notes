Scala Macros
=============
* https://www.parleys.com/tutorial/scala-macros-what-are-they-how-do-they-work-who-uses-them
* Example: convert `debug(x*amount)` to ` println("x*amount = " + (x*amount"))` so that it outputs `x*amount = 10.23` or something like that. 
* Scala macors should be part of a seperate project and should be compiled first before using them in your code. The macros project should be a dependency for your actual project. 
* Macros have access to the compile time code. A macro is simply Scala code that is executed at compile time and that manipulates the AST of a program
* 
```scala

import language.experimental.macros
import reflect.macros.blackbox.Context

object step1{ 
  def hello(): Unit = macro hello_impl
  
  def hello_impl(c:Context)(): c.Expr[Unit] = { 
    import c.universe._
    reify { println("Hello World") } // reify is a macro to write macros. 
  }
}

object step2 { 
  def myPrintln(param: Any): Unit = macro myPrintln_impl
  def myPrintln_impl(c:Context)(param: c.Expr[Any]): c.Expr[Unit] = { 
    import c.universe._ 
    reify(println(param.splice))
  }
}

object step3{ 
 def debug(param: Any): Unit = macro debug_impl
 def debug_impl(c:Context)(param: c.Expr[Any]): c.Expr[Unit] = { 
    import c.universe._ 
    val paramRep = show(param.tree)
    val paramRepTree = Literal(Constant(paramRep))
    val paramRepExpr = c.Expr[String](paramRepTree)
    reify{ println(paramRepExpr.splice + "=" + param.splice) }
  }

}


```

## Chapter 3: Next steps in Scala

1. Parameterize arrays with types
  * When you instantiate an object in Scala, you can *parameterized* it with values and types, which means "configuring" an instance when you create it.
  * You parameterized an instance with values by passing objects to a constructor in parentheses.
  * You parameterized an instance with types by specifying one or more types in square brackets.
  * When you parameterized an instance with both values and types, types come first in square brackets, then followed by values in parentheses.
  * The type parameterization portion forms part of the type of the instance, when the value parameterization part does not.
  * If a methods take only one parameter, you can call it without dot or parentheses.
  * When you apply parentheses surrounding one or more values to a variable, Scala will transform the code into an invocation of a method named `apply` on that variable. So `array(i)` is transformed into `array.apply(i)`
  * When assignment is made to a variable to which parentheses and one or more variable have been applied, Scala will transform the code into an invocation of a method named `update` that takes the arguments in parentheses as well as the object to the right ot the equal sign. So `array(i) = 1` is transformed into `array.update(i, 1)`
  * A concise way to create a new array of length three, with "zero", "one" and "two" elements:

      ```scala
      val numNames = Array("zero", "one", "two")
      ```

    What this code is actually doing is calling a factory method, named `apply` and defined on the Array *companion object*, which creates and returns the new array.

      ```scala
      val numNames = Array.apply("zero", "one", "two")
      ```


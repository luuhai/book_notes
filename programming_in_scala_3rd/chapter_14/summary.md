## Chapter 14: Assertions and Tests

1. Assertions
  * Assertions in Scala is written as calls to predefined method `assert`.
  * There're 2 versions of `assert`
    + `assert(condition)` throws an `AssertionError` if condition does not hold.
    + `assert(condition, explanation)` tests condition and, if it does not hold, throws an AssertionError that contains the given explanation. The type of explanation is Any, so you can pass any object as the explanation. The assert method will calltoString on it to get a string explanation to place inside the AssertionError.
  * We can also use `ensuring` method to make assertions. The `ensuring` method can be used with any result type because of an implicit conversion. It takes an argument, a predicate function that takes a result type and return Boolean, and passes the result to the predicate. If the predicate returns true, `ensuring` will return the result; otherwise, `ensuring` will throw an `AssertionError`.

      ``` scala
      private def widen(w: Int): Element =
        if (w <= width)
          this
        else {
          val left = elem(' ', (w - width) / 2, height)
          var right = elem(' ', w - width - left.width, height)
          left beside this beside right
        } ensuring (w <= _.width)
      ```

  * Assertions can be enabled and disabled using the JVM's `-ea` and `-da` command-line flags. When enabled, each assertion serves as a little test that uses the actual data encountered as the software runs.

## Chapter 20: Abstract members

* Scala has 4 types of abstract members: `val`, `var`, `method`, `type`

    ```scala
    trait Abstract {
      type T                  // Abstract type
      def transform(x: T): T  // Abstract method
      val initial: T          // Abstract val
      var current: T          // Abstract var
    }
    ```

* `Abstract type` means a type declared (with `type` keyword) to be a member of a class or trait, without specifying a definition.
* `Abstract val` declaration has a form like

    ```scala
    val initial: String
    ```
* Client code both refer to both the val and method in the same way. But a val will yield the same value everytime it is referenced, while a method won't.
* An `abstract val` constrains its legal implementation: Any implementation must be a val definition; it may not be a var or a def. `Abstract method` declarations, on the other hand, may be implemented by both concrete method definitions and concrete val definitions.
* An `abstract var` is much like an `abstract val`, that is it declares just a name and a type without initial value. By declare an `abstract var`, you implicitly declare an `abstract getter method` and and `abstract setter method`.
* An instance of an `anonymous class` can be defined by a `new` keyword follow by a trait name and the body.

    ```scala
    trait RationalTrait {
      val numer: Int
      val denom: Int
    }

    // create an anonymous class' instance
    val rt = new RationalTrait {
      val numer = 1
      val denom = 2
    }

    rt.numer // => 1
    ```

 In this form, the `anonymous class` is initialized *after* the initialization of the trait, so the values of the expressions inside the body are not available during the initialization of the trait. An implementing val definition in a subclass if only evaluated after the superclass has been initialized. On the other hand, class parameters are evaluated before passing to the class constructor.
* `Pre-initialized field` is a method to initialize a field of subclass before the superclass is called. To do this, simply place the field definition in braces before the superclass constructor call.

    ```scala
    new {
      val numerArg = 1 * x
      val denomArg = 2 * x
    } with RationalTrait
    ```

    ```scala
    object twoThirds extends {
      val numerArg = 2
      val denomArg = 3
    } with RationalTrait
    ```

    ```scala
    class RationalClass(n: Int, d: Int) extends {
      val numerArg = n
      val denomArg = d
    } with RationalTrait {
      def + (that: RationalClass) = new RationalClass(
        numer * that.denom + that.numer * denom,
        denom * that.denom
      )
    }

    ```

 A `pre-initialized field`'s initializer can not refer to the object that's being constructed. If such an initializer refers to `this`, the reference goes to the object containing the object or class that's being constructed.

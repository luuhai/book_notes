### Cake pattern

1. Introducton

   The aim of the `Cake Pattern` is to provide a Scala programmatic approach to the classic `Dependency Injection` strategy used when connecting dependent objects with the types they depend on.

2. Pattern Classification

   Code Resuse Pattern

3. Intent

   To provide a strategy to be used when needing to inject objects into a dependent consumer.

4. Context

   Traditionally a given type knew all of it needed to know about the types that is was dependent upon and created instances of those types within its constructor of initialization functions as required. However these relationships are hard coded within the dependent object and become difficult to control, modify or update either dynamically at runtime or static at compile time. Scala provides its own frameworks that allow similar functionality as external DI frameworks.

5. Forces/Motivation

   The `Cake Pattern` can be used when
   * The decisions about the objects to provide to a dependent object can be generated at runtime but need to be type safe.
   * Compile time configuration is acceptable.

6. Constituent Parts

   * **A Configuration Trait** This is an abstraction that defines the objects that will be available for injection into dependent objects
   * **One or more Concrete Configuration Traits** These are the types that define how the objects to be made available will be created. For example, they could be loaded from a configuration file, from a database or maintained in memory.
   * **A Context Trait** This trait which identifies the appropriate concrete configuration to load.
   * **A Dependent Component** This is a component that depends on objects supplied by a Concrete Configuration.

   The configuration traits wrap around the dependent component providers layers that provide the data and behaviour on which the root component depends.

7. Implement Issues

   * How are the configuration objects configured?
   * How the appropriate `Concrete Configuration` is identified?

8. Example

  ```scala
  trait Context

  trait Config {
    load
    val text: String
    def load: Unit
  }

  case class InMemoryConfig extends Config {
    lazy val text = "hello"
    def load = println("Load: " + text)
  }

  trait MyContext extends Context {
    this: Config =>
    def welcome = this.text
  }

  object Env extends MyContext with InMemoryConfig

  object Test extends App {
    println(Env.text)
  }

  // => Load: hello
  // => hello
  ```

9. Pros and Cons

   * Advantages:
     + Provides type safe injections of objects via the `this` self-type reference.
     + Implementations can be changed at the point of use by altering which trais are mixed in.
   * Disadvantages:
     + It may not be obvious how the dependent object obtains the data or behaviour it depends upon.
     + Which traits will be mixed into the dependent object must be known at compile time, runtime systems may offer greater flexibility.

### Singleton

1. Introducton

   The `Singleton` pattern describes a type that can only have one object constructed for it.

2. Pattern Classification

   Creational Pattern

3. Intent

   To limit the number of instances of a given type to one within a specific context.

4. Context

   The motivation behind this pattern is that some classes, typically those classes that involve the central management of a resource, should have exactly one instance. For example a connection pool could be a singleton.

5. Forces/Motivation

   The `Singleton` pattern can be used where:
   * There must be exactly one instance of a type and it must be accessible to clients from a well-known access point.

   In some cases additional consideration need to be taken into account. For example:
   * Whether the sole instance should be extensible be sub-typing and clients should be able to use an extended instance without modifying their code.
   * When should the singleton be created?
   * Should the singleton ever be killed?
   * Does the singleton have a lifecycle which needs to be represented such as operations that are performed just after the singleton is created and/or just before the singleton is killed etc.
   * What if the singleton concept needs to be shared across virtual machines, for example within a server farm?

6. Constituent Parts

   The primary participant is the `Singleton` type itself. Its collaborators are the clients who access the singleton class.

7. Implement Issues

   * How do you implement/ensure a single instance of an object?
   * The lifecycle of a singleton, the ability to subclass a singleton and possibly the need for a slightly more flexible approach (such as the so called `duoton` which limits the number of instances to two etc.)

8. Example

   * Basic Scala Singleton Implementation

  ```scala
  object Session {
    val id = "session"
    override def toString = "session singleton"
  }

  object Test extends App {
    val id = Session.id
    println(id)
    println(Session)
  }
  ```

   * Extended Singleton Scenario

  ```scala
  trait Session {
    val id: String
  }

  private trait InternalSession extends Session {
    def postCreate: Unit
    def preDestroy: Unit
  }

  private class SessionImpl(val id: String) extends InternalSession {
    def postCreate = println("SessionImpl postCreate")
    def preDestroy = println("SessionImpl preDestroy")
    override def toString = "session" + id + " singleton"
  }

  object SessionManager {
    private[this] var _instance: Option[InternalSession] = None
    private[singleton] def instance: Session = {
      if (_instance.isEmpty) {
        _instance = Option(new SessionImpl("jeh"))
        _instance.get.postCreate
      }
      return _instance.get
    }
    def destroy = {
      if (_instance nonEmpty) {
        _instance.get.preDestroy
        _instance = None
      }
    }
    def session: Session = {
      return new SessionDelegate()
    }
  }

  private class SessionDelegate extends Session {
    override val id: String = {
      SessionManager.instance.id
    }
    override def toString = SessionManager.instance.toString
  }

  object Test extends App {
    val s1 = SessionManager.session
    println(s1)
    val s2 = SessionManager.session
    println(s2)
    SessionManager.destroy
    println(s2)
    val s3 = SessionManager.session
    println(s3)
  }

  // => SessionImpl postCreate
  // => session jeh singleton
  // => session jeh singleton
  // => SessionImpl preDestroy
  // => SessionImpl postCreate
  // => session jeh singleton
  ```

9. Pros and Cons

   * Basic Implementation Advantages:
     + Simple implementation approach within the Scala language.
     + Access to the sole instance based on visibility.
     + Reduced name space with little likely confusion between class, traits and the object instance.
   * Basic Implementation Disadvantages:
     + Little control over the lifecycle of the singleton including the behavior that should be invoked after construction or before the singleton is destroyed.
     + No ability to sub-type the singleton.
     + Little actual control on access to the singleton object and thus little ability to change the singleton transparent to the clients.
   * Extended Implementation Advantages:
     + More control over the lifecycle of the singleton and the behavior that is invoked as part of that lifecycle.
     + May allow the ability to sub-type the singleton and use that sub-type in place of the original type.
     + More control over access to the singleton object.
   * Extended Implementation Disadvantages:
     + Increased complexity, as the inherent facilities associated with the Scala object keyword are not directly being used.
     + Increased namespace pollution and potential lack of clarity of who to use the singleton types.
     + Greater confusion as the implementation does not align with developer's expectations.

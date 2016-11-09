## Chapter 19: Type parameterization

**1. Functional Queue**

The code below implement basic functional (immutable) Queue.

  ```scala
  class Queue[T](
    private val leading: List[T],
    private val trailing: List[T]
  ) {
    private def mirror =
      if (leading.isEmpty)
        new Queue(trailing.reverse, Nil)
      else this

    def head = mirror.leading.head

    def tail = {
      val q = mirror
      new Queue(q.leading.tail, q.trailing)
    }

    def enqueue(x: T) =
      new Queue(leading, x :: trailing)
  }
  ```

**2. Information Hiding**

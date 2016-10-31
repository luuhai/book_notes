## Chapter 21: Implicit conversions and parameters

#### 1. Rules for implicits
  * `Implicit definitions` are those that the compile is allowed to insert into a program in order to fix any of its type errors.
  * Implicit conversions are governed by the following general rules:
    **+ Only definitions marked implicit are available.**
    The `implicit` keyword is used to mark which declarations the compiler may use as implicits. You can use it to mark any variable, function, or object definition. This way, you avoid confusion that would result if the compiler picked random functions that happen to be in scope.

    **+ An inserted implicit conversion must be in scope as a single identifier, or be associated with the source or target type of the conversion.**
    The Scala compiler will only consider implicit converions that are in scope. Moreover, the implicit conversion must be in scope as a single identifier. If you want to make `someVar.conversion` as an implicit, you would need to import it. There's one exception to the "single identifier" rule: The compiler will also look for implicit definitions in the companion object of the source or expected target types of the conversion.

    **+ Only one implicit is inserted.**
    The compiler does not insert further implicit conversions when it is already in the middle of trying another implicit.

    **+ Whenever code type checks as it is written, no implicits are attempted.**
    The compiler will not change code that already works. That also means you can always replace implicit identifiers by explicit ones.

    **+ Implicit conversion can have arbitraty names.**
    Them name of an implicit conversion matters only in 2 situations: if you want to write it explicitly in a method application and for determining which implicit conversions are availablea at any place in the program.

    **+ There're 3 places implicits are used in the language: conversions to an expected type, converions of the receiver of a selection, and implicit parameters.**
    Implicit conversions to an expected type let you use one type in a context where a different type is expected. Conversions of the receiver let you adapt the receiver of a method call if the method is not applicable on the original type. Implicit parameters are usually used to provide more information to the called function about what the caller wants. It especially usefule with generic functions, where the called function might otherwise know nothing at all about the type of one or more arguments.

# Scala collections

These are all immutable covariant collections from the package `scala.collection.immutable`:

- ~~[Traversable](https://www.scala-lang.org/api/2.12.0/scala/collection/Traversable.html)~~ ([deprecated](https://docs.scala-lang.org/overviews/core/collections-migration-213.html))
- [Iterable](https://www.scala-lang.org/api/current/scala/collection/immutable/Iterable.html)
- Sets
  - [Set](https://www.scala-lang.org/api/current/scala/collection/immutable/Set.html), can be created with Set(1,3,3) which will create a default implementation (HashSet) with {1,3}
    - `+` incl
    - `++` concat
  - [HashSet](https://www.scala-lang.org/api/current/scala/collection/immutable/HashSet.html) (default Set)
  - etc
- Maps
  - [Map](https://www.scala-lang.org/api/current/scala/collection/immutable/Map.html)
    - `_1` key
    - `_2` value
  - [HashMap](https://www.scala-lang.org/api/current/scala/collection/immutable/HashMap.html) (default Map)
  - etc
- Sequences
  - [Seq](https://www.scala-lang.org/api/current/scala/collection/immutable/Seq.html): Sequences
      - `++` concat (Returns a new list containing the elements from the left hand operand followed by the elements from the right hand operand.)
      - `+:` prepend
      - `++:` prependAll
      - `:+` append
      - `:++` appendAll
      - `exists()`
      - [`groupBy()`](https://www.scala-lang.org/api/current/scala/collection/immutable/Seq.html#groupBy[K](f:A=%3EK):scala.collection.immutable.Map[K,C]) partitions this immutable sequence into a map of immutable sequences according to some discriminator function.
      - [`forall()`](https://www.scala-lang.org/api/current/scala/collection/immutable/Seq.html#forall(p:A=%3EBoolean):Boolean) tests whether a predicate holds for all elements 
      - [`zip()`](https://www.scala-lang.org/api/current/scala/collection/immutable/Seq.html#zip[B](that:scala.collection.IterableOnce[B]):CC[(A@scala.annotation.unchecked.uncheckedVariance,B)]) returns a sequence formed from this immutable sequence and another iterable collection by combining corresponding elements in pairs
      - `unzip()`
      - [`flatMap()`](https://www.scala-lang.org/api/current/scala/collection/immutable/Seq.html#flatMap[B](f:A=%3Escala.collection.IterableOnce[B]):CC[B]) applies to each element a function which returns a collection, then flattens (merges) all the obtained collections
      - `sum()`
      - `product()`
      - `max()` (elements must implement [Ordered](https://www.scala-lang.org/api/current/scala/math/Ordered.html))
      - `min()` (elements must implement [Ordered](https://www.scala-lang.org/api/current/scala/math/Ordered.html))
  - [IndexedSeq](https://www.scala-lang.org/api/current/scala/collection/immutable/IndexedSeq.html): Indexed sequences, can be accessed at a certain index
    - [Vector](https://www.scala-lang.org/api/current/scala/collection/immutable/Vector.html) (default IndexedSeq)
      - [`updated()`](https://www.scala-lang.org/api/current/scala/collection/immutable/Vector.html#updated[B%3E:A](index:Int,elem:B):scala.collection.immutable.Vector[B]) replaces the element in a certain position
    - [Range](https://www.scala-lang.org/api/current/scala/collection/immutable/Range.html)
      - `1 until 5` = 1,2,3,4
      - `1 to 10 by 3` = 1,4,7,10
      - `6 to 1 by -2` = 6,4,2
    - etc
  - [LinearSeq](https://www.scala-lang.org/api/current/scala/collection/immutable/LinearSeq.html): Linear sequences:, accessible only sequentially
    - [List](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html) (default LinearSeq)
      - Empty list: [Nil](https://www.scala-lang.org/api/current/scala/collection/immutable/Nil$.html)
      - `::` add the element to the beginning 
      - [`map()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#map[B](f:A=%3EB):List[B]) (es: `def scaleList(xs: List[Double], factor: Double) = xs map (_ * factor))` where `(_ * factor)`=`(x => x * factor)`
      - [`filter()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#filter(p:A=%3EBoolean):List[A])
      - [`filterNot()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#filterNot(p:A=%3EBoolean):List[A])
      - [`partition()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#partition(p:A=%3EBoolean):(List[A],List[A]))
      - [`takeWhile()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#takeWhile(p:A=%3EBoolean):List[A])
      - [`dropWhile()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#dropWhile(p:A=%3EBoolean):C)
      - [`span()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#span(p:A=%3EBoolean):(List[A],List[A]))
      - [`reduceLeft()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#reduceLeft[B%3E:A](op:(B,A)=%3EB):B) for left associative operations
        - es: `def sum(xs: List[Int]) = (0 :: xs) reduceLeft (_ + _)`) where `( _+_ )`=`((x, y) => x + y)`
      - [`foldLeft()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#foldLeft[B](z:B)(op:(B,A)=%3EB):B)
        - es: `def sum(xs: List[Int]) = (xs foldLeft 0) (_ + _)`
        - es: `def maxLength(strings: List[String]) = (strings foldLeft 0)((len:Int, str:String) => len.max(str.length))`
      - [`reduceRight()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#reduceRight[B%3E:A](op:(A,B)=%3EB):B) for right associative operations
      - [`foldRight()`](https://www.scala-lang.org/api/current/scala/collection/immutable/List.html#foldRight[B](z:B)(op:(A,B)=%3EB):B)
    - [Queue](https://www.scala-lang.org/api/current/scala/collection/immutable/Queue.html)

# Relevant classes

- [scala.Some](https://www.scala-lang.org/api/current/scala/Some.html)
- [scala.Option](https://www.scala-lang.org/api/current/scala/Option.html)
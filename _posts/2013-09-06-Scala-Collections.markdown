---     
  layout: post
  title: Scala-Collection
---
{{ page.title }}
===================
　
###    Scala Collections Tips

1 Type Hierarchy

    trait IterableLike[+A, +Repr] extends Any
                                    with Equals 
                                    with TraversableLike[A, Repr] 
                                    with GenIterableLike[A, Repr] 
    
    trait Iterable[+A] extends Traversable[A]
                                    with GenIterable[A]
                                    with GenericTraversableTemplate[A, Iterable]
                                    with IterableLike[A, Iterable[A]]

    trait TraversableLike[+A, +Repr] extends Any
                                    with HasNewBuilder[A, Repr]
                                    with FilterMonadic[A, Repr]
                                    with TraversableOnce[A]
                                    with GenTraversableLike[A, Repr]
                                    with Parallelizable[A, ParIterable[A]]

    




                                    
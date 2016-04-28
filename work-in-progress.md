# Work in Progress


# useful resources 

Clojure examples - https://jr0cket@github.com/jr0cket/ClojureProgramming.git


# Abstraction through syntax

Syntactical abstraction can vary between using functions to abstract away common operations and full fledged DSLs that allow us to express complex tasks with ease.

## Using threading macros

Classic lisp gives rise to syntax such as

```clojure
(:baz (:bar (:foo my-map)))
```

Using the thread first macro in Clojure you can make this much more readable

```clojure
(-> my-map
  (:foo)
  (:bar)
  (:baz))
```

Threading macro converts nested code into sequential code

## Minimise nested statements

In this example there are several nested if statements, making the code hard to read and slower to interpret.

```clojure
(if :pred-1
  :result-1
  (if :pred-2
    :result-2
    (if :pred-3
      :result-3
      :result-4)))
```

You can simplify this by using the `cond` function instead

```clojure 
(cond
  :pred-1 :result-1
  :pred-2 :result-2
  :pred-3 :result-3
  :else :result-4)
  ```

`cond` executes its predicates in turn (:pred-1, :pred-2 ...) until one evaluates to something truthy, then it executes the corresponding result and returns it. Again this is exactly what the `if` version does, cond is a macro that turns the latter into former.


## Repeated forms

Creating a local symbol with `let` and then using that symbol as an `if` predicate can be replaced by `if-let` macro:

(let [data :data]
  (if data
    :data-is-bound
    :no-data))

(if-let [data :data]
  :data-is-bound
  :no-data)

To streamline the code even further, we can often use destructuring

(let [list-items '(3 4)
      x (clojure.core/nth list-items 0 nil)
      y (clojure.core/nth ?list 1 nil)]
  (+ x y))

(let [[x y] (list 3 4)]
(+ x y))



### Edn
edn is an extensible data notation. A superset of edn is used by Clojure to represent programs, and it is used by Datomic and other applications as a data transfer format. This spec describes edn in isolation from those and other specific use cases, to help facilitate implementation of readers and writers in other languages, and for other uses.

[Clojure api 1.6 for edn](https://clojure.github.io/clojure/clojure.edn-api.html)

https://github.com/edn-format/edn

http://www.compoundtheory.com/clojure-edn-walkthrough/



http://www.clojuresphere.com/

http://blog.jenkster.com/2013/12/a-cider-excursion.html

clojure emacs metaprogramming trick https://www.youtube.com/watch?v=LXhWW1Yqpt0

http://eigenhombre.com/clojure/2014/07/05/emacs-customization-for-clojure/

http://martintrojer.github.io/clojure/2014/10/02/clojure-and-emacs-without-cider/

https://github.com/technomancy/mire

https://github.com/cemerick/drawbridge

https://github.com/technomancy?tab=repositories

https://github.com/jr0cket/kensa-create-clojure

http://christophermaier.name/blog/2011/07/07/writing-elegant-clojure-code-using-higher-order-functions

https://github.com/jamesmacaulay/zelkova

http://www.purelyfunctional.tv/core-async

http://blog.cognitect.com/blog/2014/10/24/analysis-of-the-state-of-clojure-and-clojurescript-survey-2014

clojure daily - http://paper.li/ajlopez/1291580164

https://github.com/r0man/sablono

https://github.com/swannodette/om/wiki
https://github.com/magomimmo/om-start-template

clojure at a bank http://www.pitheringabout.com/?p=693

clojurescript any better http://rrees.me/2014/01/16/clojurescript-is-it-any-better-yet/

https://medium.com/@hlship/clojure-owning-the-language-ec0196871c40

http://cognitect.com/









#### Charicteristics

* Dynamic 
- typed - like Python, Ruby or Groovy 
- because its a LISP - you can redefine running code
- REPL - a fast way to explore your problem domain with code

* Functional programming
- in contrast to imperative programing
- immutable data structures at its core, everything is immutable by default
- if any piece of data can be changed, that is mutable state
- in imperative programming, we change state where ever we like
- in functional programming we avoid changing state as much as possible 
- if a function does not change state it is referentially transparent, always returning the same result when given the same input (arguments) - often returned as a pure function 
- impure functions can affect other functions and therefore has to be very mindful of the changes it makes and when it makes them
- pure functions are truely modular as they do not affect any other part of the system
** Changing state
- rather than changing a data structure, fp instead creates a new data structure that contains the changes and copies of the existing data.
- to manage the potential overhead of copying data structures, Clojure uses Persistent collections (Lists, Vectors, Maps) which are immutable but provide an efficient way to mutate by sharing common elements (data) 
** Input & output with functional programming 
- other fp languages like haskel & Scala use monads to encapsulate data changes whilst appearing stateless to the rest of the program - monads allow us to sneak in impure code into the context of pure code.
- Clojure doesnt try and enforce functional purity, so any function can include impure code 
- most functoins should be pure though or you loose the benefits of functional programming
- Clojure encourages minimal state changes / mutable state - so its up to the developer to keep the ratio of mutalble data small
- Clojure uses reference types to manage threads and mutable state.  References provide syncronisation of threads without using locks (notoriusly cumbersome).  See STM 

* Hosted on the Java Virtual Machine 
- writen for the JVM & heavily integrated, giving beautiful integratoin 
- Clojure is compiled to Java byte code 
- many parts of the Clojure standard library, Clojure.core defer to the Java Standard library, for example for I/O (reading,writing files)
- Clojure makes invoking Java very convieninet and provides special primative constructs in the Clojure language to do so (new .javaMethodName javaClassName. etc)

* Supporting concurrency
- atoms etc 
- automatic management of state changes via Software transactional memory - like having an ACID database in memory, managing requests to change values over time.
- by having immutable data structures - if your values do not change then its trivial to have massive parallelism.

* A modern LISP 
- leaner syntax and not as many brackets as LISP
- clean data structure syntax at the core of the language
- LiSP was the first language to introduce first class functions, garbage collection and dynamic typing, which are common in languages used today

Macros 
- a function that takes in source code and returns source code, replacing the macro code  
- use macros to take out repetition / boilerplate code
- as LISP syntax is extremely simple it is much easier to write macros that work compared to non-LISP languages


> **fixme** assuming you need more, I'll add to this page, but Clojure is a very powerful language, incredibly flexible and tonnes of fun.  What more do you need ?


> **fixme** concepts to explore 

Clojure emphasizes safety in its type system and approach to parallelism, making it easier to write correct multithreaded programs. 

Clojure is very concise, requiring very little code to express complex operations.

Data centric design - a well constructed data structure helps define and clarify the purpose of the code

Modularity - Clojure and its community build things in modules / components that work together (in a similar design approach to the Unix file system, for example). 

It offers a REPL and dynamic type system: ideal for beginners to experiment with, and well-suited for manipulating complex data structures. 

A consistently designed standard library and full-featured set of core datatypes rounds out the Clojure toolbox.

Clojure is close to the speed of Java 

#### Constraints

Clojure relies on the JVM so there can be a longer boot time than a scripting language like Javascript.  However, as you can connect to the Clojure runtime (the REPL) of a live system and because Clojure is dynamic, you can make changes to that live system without any downtime.  

If you require more performance from Clojure, you can specify _ahead of time_ compilation.



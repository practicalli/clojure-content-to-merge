# Features of Clojure 

#### Dynamic Development

  Clojure has a REPL, its run-time environment.  You can define functions and data structures on th fly, change code and re-evaluate it whilst your application is still running.
  
  You could even connect to the REPL of a live system and change its behaviour without any down time (unless of course you write code that crashes).

#### Functional Programming

  Functions return a value (even if that value is nil) and you can therefore use a function as an agument to another function.  This is termed as _first order_ functions.

#### Lisp

  Everything is a list, yes everything, even those things that dont look like a list are a list underneath.  
  
  Lists are executable.  The open Parentesis `(` denote that the next thing is the name of a function to be called.  The behaviour of `(` can be over-ridden using `quote` or its short form `'` and the list is treated only as data.

#### Runtime Polymorphism

  See Clojure arity and multi-methods

#### Concurrent Programming

  Thread'ed code is much safe when you dont change state (eg. immutable state).  Clojure is stateless by default.
  
  Clojure helps you scale your applications by with a parrallel procssing approach, as you can run functions over immutable datastructures without conflict.

#### Hosted on the JVM

  Clojure has great Java Interoperability.  It can be nicer to work with Java libraries in Clojure that it can in Java (eg. Swing)


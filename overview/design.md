# Clojure Design 

  Clojure leads to a very component based approach to development.  There are no huge and bloated frameworks in Clojure.  The core is very small.  Hundreds of focused libraries to use in collaboration.

# Everything is a list

Clojure code is represented as a list, with the first element of that list evaluated as a function call.  This is a language design from LISP (List Processing) and gives Clojure much of its flexibility and concise nature.

The List is also a build in persistent data structure.  Persistent data structures are immutable (cannot change state once created), however the result of running a function over a list can return a list that contains only the changes between the original list and the result returned.  This is a highly efficient way to manage data changes in memory.

# Maps & Vectors

Maps and vectors are two more built-in persistent data structures that are more commonly used to represent data within a Clojure application.

Vectors are a catch all data structure that can hold any type of information, including other data structures and function calls.

Maps are a collection of key / value pairs that provide an easy way to reference data by keys.  Its common to use Clojure `keywords` as the keys as keywords are self-referential (they point to themselves).  Using keywords in a map means you can use a specific keyword as a function call on the map that returns its associated value.


# Extensibility via Macros 

  You can extend the language and define your own constructs using Macros. 
  
  The first example of this you see is from Leiningen.  The `defproject` function is a macro that helps you easily define the configuration of a Clojure project.
  
  An example of a macro that is part of the core Clojure language is `defn`.  When you define a function with `devfn` it is syntactic sugar for defining a thing that is a function.
  
  (defn my-function [parameter] (my-behaviour parameter) )
  
  (def my-function
    (fn )
    
**Special forms**

  The following are the building blocks of Clojure, everything else is either a macro or a function
  
  catch, def, do, dot ('.'), finally, fn, if, let, loop, monitor-enter, monitor-exit, new, quote, recur, set!, throw, try and var



#### Application design 

  Boiled down to the most simplest structure, Clojure applications you write typically look like this: 

```clojure 
;; define a namespace
(ns name-space.name)

;; define one or more immutable data structures - the fewer the better typically
(def my-data-struture [[{}{}]])

;; define behaviour that acts on data structures inside one or more functions
(defn my-function [paramter] 
  (my-behaviour parameter))

;; Call those functions to make your application do something  
(my-behaviour data)
```

>  param's can be functions too !!

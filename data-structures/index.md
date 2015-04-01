# Clojure data structures 

Clojure has 4 datastructures as part of the language that are used extensively, rather than defining your own types.  

* List
* Vector 
* Map
* Set 

Elements of these Clojure data structures can be of any type. as Clojure works out those types only when it needs to.

Clojure data structure share the following characteristics:
* Immutable - once a data structure is defined it cannot be changed.  Any changes you ask for are created in a new data structure which is linked back to the original data structure 

* Persistent 

* Sequences

* Shared 

* contains any value, including functions (as they evaluate to a value) 
* same conceptual functions 
* behaviour - you can ask your data structure for values it contains


In Clojure everything is a list, after all the language is a LISP (List Processing).

As Clojure is _Homoiconic_ then there is no real distinction between behaviour and data.  Clojure can be thought of as a data driven language (TODO or is this just my interpretation)


#### Everything is a List

Lists are the data structure for the whole language, so when you just have data in a list it need to be evaluated using the quote or ' syntax.



#### Vectors are fast with indexed access 


#### Maps to categorise the world in key value pairs 


#### Sets when you want more order in your data structure 


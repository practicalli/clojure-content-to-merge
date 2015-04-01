# Whats my environment 

Clojure has built in symbols, which start and end with `*`

Symbols can be evaluated outside of a list structure, functions (the behaviour of your application) and their arguments are contained within a list structure ()

The full clojure version can be used to check you are running a particular version, major or minor of Clojure core

```clojure
    *clojure-version*
```

The version info for Clojure core, as a map containing `:major`, `:minor`, `:incremental` and `:qualifier` keys. Feature releases may increment `:minor` and/or `:major`, bugfix releases will increment `:incremental`.
Possible values of `:qualifier` include _GA_, _SNAPSHOT_, _RC-x_ and _BETA-x_

The directory where the Clojure compiler will create the .class files for the current project
This directory must be in the classpath for 'compile' to work.

```clojure
*compile-path*
```

The path of the file being evaluated, as a String.  In the REPL the value is not defined.

```clojure
*file*
```

A clojure.lang.Namespace object representing the current namespace

```clojure
*ns*
```

most recent repl values

```clojure
    *1
    *2
    *3
```


## Reading Java Properties

`java.lang` is part of the Java runtime environment, so when ever you run a REPL you can call any methods without having to import them or include any dependencies

From `java.lang.System getProperty()` as documented at:

http://docs.oracle.com/javase/8/docs/api/java/lang/System.html

```clojure
    (System/getProperty "java.version")
    (System/getProperty "java.vm.name")
```

Java properties can be obtained by calling System.getProperty from `java.lang`.  As System.getProperty is called as a function in clojure it needs to be wrapped in a list structure.

  To make the returned value more informative we can use the Clojure `str` function to give the value of the Java property some context

```clojure
    (str "Current Java version: " (System/getProperty "java.version"))
```
  We can also get the version of the Clojure project

```clojure
    (System/getProperty "clojure-through-code.version")
```

  We can also read the Leiningen project file and pull out specific values (this is more advanced code)
  
```clojure
    (->
      "./project.clj"
      slurp
      read-string
      (nth 2))
``` 

  Or just read in the whole Clojure Project file
```clojure
    (->
      "./project.clj"
      slurp)  
 ```
 
  You may have guessed that the function `slurp` reads in the text from the `project.clj` file.  The `read-string` function reads the file pulled in by `slurp`.

```clojure
    (->
      "./project.clj"
      slurp
      read-string)
``` 

> **Hint** The syntax `->` is called the threading macro, esentially it passes the result of each expression as the first argument of the next expression.  So in the example above, the `project.clj` file is passed to `slurp` and the text of the `project.clj` file is passed to `read-string`.  The value of calling `read-string` is returned as the value of the function call.

> The threading macro will be covered later with more examples, so dont worry if you dont get it just yet.  

## Mapping the project data

  A common approach in Clojure its to put data into a map, so lets add all project information to a map

```clojure 
    (->> 
      "project.clj"
         slurp
         read-string
         (drop 2)
         (cons :version)
         (apply hash-map)
         (def project))
```

> **Hint** Data in Clojure is often held in maps or vectors, quite often a combination of the two.  We will come to this later when looking at the Persistent data structures that are built into Clojure.

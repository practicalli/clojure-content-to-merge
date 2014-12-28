# Clojure syntax

#### Brackets everywhere

  Clojure has an abundance of `()` which represent a list.  As Clojure is a LISP (List Processing) language then everything is a list.  This makes Clojure very powerful and easier to read.


> **Comment**  The seemingly abundance of `()` does put some people off until they realise there are fewer "special characters" in Clojure than in other curly bracket langauges (Java, C#, C, etc).  A good editor will also match brackets for you as you type, making it easy to write Clojure.


> **fixme** Comparison to Java (and similar languages)

In Clojure




In Java



> **Comment** Syntax differences are not a valuable reason to avoid Clojure.


#### Prefix notation 

  Instead of having a mix of notations like other languages, Clojure uses pre-fix notation entirely.

  In Clojure: 
```clojure  
    (+ 1 2 3 5 8 13 21 )
    (str "Clojure" " uses " "prefix notation")
```
  In Java 
```java 
    (1 + 2 + 3 + 5 + 8 + 13 + 21);
    StringBuffer mystring = new StringBuffer("Java" + " mixes " + "notation") ;
```

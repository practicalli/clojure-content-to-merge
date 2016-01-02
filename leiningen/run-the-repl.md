# Run the REPL



## Reload changes from file 

If you do not have your editor connected to the REPL you can still reload changes made to files by reloading the changed namespace in the REPL.

Enter the following into the REPL, specifying your namespace

```clojure
(use 'your.namespace :reload)
```

You can also use https://github.com/clojure/tools.namespace, however, as refresh throws away the current namespace you have to enter both lines of code each time

```clojure
(use '[clojure.tools.namespace.repl :only (refresh)])

(refresh)
```


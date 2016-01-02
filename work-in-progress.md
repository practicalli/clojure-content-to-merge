# Work in Progress



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


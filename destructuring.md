# Destructuring

What is destructuring?

    Clojure supports abstract structural binding, often called destructuring, in let binding lists, fn parameter lists, and any macro that expands into a let or fn. -- http://clojure.org/special_forms

The simplest example of destructuring is assigning the values of a vector.

user=> (def point [5 7])
#'user/point

user=> (let [[x y] point]
         (println "x:" x "y:" y))
x: 5 y: 7

note: I'm using let for my examples of destructuring; however, in practice I tend to use destructuring in function parameter lists at least as often, if not more often.

I'll admit that I can't remember ever using destructuring like the first example, but it's a good starting point. A more realistic example is splitting a vector into a head and a tail. When defining a function with an arglist** you use an ampersand. The same is true in destructuring.

user=> (def indexes [1 2 3])
#'user/indexes

user=> (let [[x & more] indexes]
         (println "x:" x "more:" more))
x: 1 more: (2 3)

It's also worth noting that you can bind the entire vector to a local using the :as directive.

user=> (def indexes [1 2 3])
#'user/indexes

user=> (let [[x & more :as full-list] indexes]
         (println "x:" x "more:" more "full list:" full-list))
x: 1 more: (2 3) full list: [1 2 3]

Vector examples are the easiest; however, in practice I find myself using destructuring with maps far more often.

Simple destructuring on a map is as easy as choosing a local name and providing the key.

user=> (def point {:x 5 :y 7})
#'user/point

user=> (let [{the-x :x the-y :y} point]
         (println "x:" the-x "y:" the-y))
x: 5 y: 7

As the example shows, the values of :x and :y are bound to locals with the names the-x and the-y. In practice we would never prepend "the-" to our local names; however, using different names provides a bit of clarity for our first example. In production code you would be much more likely to want locals with the same name as the key. This works perfectly well, as the next example shows.

user=> (def point {:x 5 :y 7})
#'user/point

user=> (let [{x :x y :y} point]
         (println "x:" x "y:" y))
x: 5 y: 7

While this works perfectly well, creating locals with the same name as the keys becomes tedious and annoying (especially when your keys are longer than one letter). Clojure anticipates this frustration and provides :keys directive that allows you to specify keys that you would like as locals with the same name.

user=> (def point {:x 5 :y 7})
#'user/point

user=> (let [{:keys [x y]} point]
         (println "x:" x "y:" y))
x: 5 y: 7

There are a few directives that work while destructuring maps. The above example shows the use of :keys. In practice I end up using :keys the most; however, I've also used the :as directive while working with maps.

The following example illustrates the use of an :as directive to bind a local with the entire map.

user=> (def point {:x 5 :y 7})
#'user/point

user=> (let [{:keys [x y] :as the-point} point]
         (println "x:" x "y:" y "point:" the-point))
x: 5 y: 7 point: {:x 5, :y 7}

We've now seen the :as directive used for both vectors and maps. In both cases the local is always assigned to the entire expression that is being destructured.

For completeness I'll document the :or directive; however, I must admit that I've never used it in practice. The :or directive is used to assign default values when the map being destructured doesn't contain a specified key.

user=> (def point {:y 7})
#'user/point
 
user=> (let [{:keys [x y] :or {x 0 y 0}} point]
         (println "x:" x "y:" y))
x: 0 y: 7

Lastly, it's also worth noting that you can destructure nested maps, vectors and a combination of both.

The following example destructures a nested map

user=> (def book {:name "SICP" :details {:pages 657 :isbn-10 "0262011530"}})
#'user/book

user=> (let [{name :name {pages :pages isbn-10 :isbn-10} :details} book]
         (println "name:" name "pages:" pages "isbn-10:" isbn-10))
name: SICP pages: 657 isbn-10: 0262011530

As you would expect, you can also use directives while destructuring nested maps.

user=> (def book {:name "SICP" :details {:pages 657 :isbn-10 "0262011530"}})
#'user/book
user=> 
user=> (let [{name :name {:keys [pages isbn-10]} :details} book]
         (println "name:" name "pages:" pages "isbn-10:" isbn-10))
name: SICP pages: 657 isbn-10: 0262011530

Destructuring nested vectors is also very straight-forward, as the following example illustrates

user=> (def numbers [[1 2][3 4]])
#'user/numbers

user=> (let [[[a b][c d]] numbers]
  (println "a:" a "b:" b "c:" c "d:" d))
a: 1 b: 2 c: 3 d: 4

    Since binding forms can be nested within one another arbitrarily, you can pull apart just about anything -- http://clojure.org/special_forms

The following example destructures a map and a vector at the same time.

user=> (def golfer {:name "Jim" :scores [3 5 4 5]})
#'user/golfer

user=> (let [{name :name [hole1 hole2] :scores} golfer] 
         (println "name:" name "hole1:" hole1 "hole2:" hole2))
name: Jim hole1: 3 hole2: 5

The same example can be rewritten using a function definition to show the simplicity of using destructuring in parameter lists.

user=> (defn print-status [{name :name [hole1 hole2] :scores}] 
  (println "name:" name "hole1:" hole1 "hole2:" hole2))
#'user/print-status

user=> (print-status {:name "Jim" :scores [3 5 4 5]})
name: Jim hole1: 3 hole2: 5

There are other (less used) directives and deeper explanations available on http://clojure.org/special_forms and in The Joy of Clojure. I recommend both.

**(defn do-something [x y & more] ... )
Posted by Jay Fields at 7:44 AM Email ThisBlogThis!Share to TwitterShare to FacebookShare to Pinterest
Labels: clojure, destructuring
10 comments:

    fogus8:26 AM

    Nice post. One other note that naturally follows from the end of your post is that destructuring forms the basis of Clojure's named arguments:

    (defn print-status [& {name :name [hole1 hole2] :scores}]
    (println "name:" name "hole1:" hole1 "hole2:" hole2))

    (print-status :name "Joey" :scores [42 18])


    You can also use pre-conditions to check if certain arguments are passed in:


    (defn print-status [& {name :name [hole1 hole2] :scores}]
    {:pre [name]}
    (println "name:" name "hole1:" hole1 "hole2:" hole2))

    (print-status :scores [42 18])
    ; java.lang.AssertionError: Assert failed: name

    (print-status :name "Joey" :scores [42 18])
    ; name: Joey hole1: 42 hole2: 18


    :f
    Reply
    Jay Fields9:08 AM

    Good stuff Fogus, thanks.

    Cheers, Jay
    Reply
    Matt Todd5:31 PM

    Can you combine :as and :or et al?
    Reply
    Anonymous7:29 PM

    Yes, all the directives can be used at the same time.

    Cheers, Jay
    Reply
    Laurent PETIT3:08 AM

    Hi, one note about using destructuring for function arguments : by doing so, you're quite explicitly establishing a more detailed contract with the consumer of the function. That is, you open the internals of the passed arguments.

    Depending on the fact that the user may or may not be aware of the internals of the arguments, it may or may not be a good idea.

    So I tend to think about the use of destructuring function arguments directly in the function signature, depending on whether the "layout" of the arguments of the function is part of the user API.
    Reply
    
    
    

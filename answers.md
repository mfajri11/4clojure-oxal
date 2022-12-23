# 4CLOJURE EXERCISES


[problem 1, nothing but the truth](https://4clojure.oxal.org/#/problem/1)
```clj
true
```
[problem 2, simple math](https://4clojure.oxal.org/#/problem/2)
```clj
4
```

[problem 3, String](https://4clojure.oxal.org/#/problem/3)
```clj
"HELLO WORLD"
```

[Problem 4, Lists](https://4clojure.oxal.org/#/problem/4)
```clj
:a :b :c
```
[Problem 5, conj on lists](https://4clojure.oxal.org/#/problem/5)
```clj
'(1 2 3 4)
```

[Problem 6, Vectors](https://4clojure.oxal.org/#/problem/6)
```clj
:a :b :c
```
[Problem 7, conj on vectors](https://4clojure.oxal.org/#/problem/7)
```clj
[1 2 3 4]
```

[Problem 8, Sets](https://4clojure.oxal.org/#/problem/8)
```clj
#{:a :b :c :d}
```

[Problem 9, conj on sets](https://4clojure.oxal.org/#/problem/9)
```clj
2
```

[Problem 10, Maps](https://4clojure.oxal.org/#/problem/10)
```clj
20
```
[Problem 11, conj on maps](https://4clojure.oxal.org/#/problem/11)
```clj
[:b 2]
```

[Problem 12, Sequences](https://4clojure.oxal.org/#/problem/12)
```clj
3
```

[Problem 13, rest](https://4clojure.oxal.org/#/problem/13)
```clj
[20 30 40]
```

[Problem 14, Functions](https://4clojure.oxal.org/#/problem/14)
```clj
8
```

[Problem 15, Double Down](https://4clojure.oxal.org/#/problem/15)
```clj
#(* % 2)
```

[Problem 16, Hello World](https://4clojure.oxal.org/#/problem/16)
```clj
#(str "Hello, " % "!")
```

[Problem 17, map](https://4clojure.oxal.org/#/problem/17)
```clj
'(6 7 8)
```
[Problem 18, filter](https://4clojure.oxal.org/#/problem/18)
```clj
'(6 7)
```
[Problem 19, Last Element](https://4clojure.oxal.org/#/problem/19)
```clj
(let [&init last] last)
(comp first reverse)
(fn [xs]
  (nth xs (- (count xs) 1)))
```

[Problem 20, Penultimate Element](https://4clojure.oxal.org/#/problem/20)
```clj
(defn second-las [coll]
  (second (reverse coll)))
;; using composition
(comp second reverse)
;; just for fun
(comp first rest reverse)
;; anohter way
(comp last drop-last)
;;
(fn [xs]
  (nth xs (- (count xs) 2)))
```

[Problem 21, Nth Element](https://4clojure.oxal.org/#/problem/21)
```clj
(fn [xs i]
  (last (take (inc i) xs)))
;; alternative
(fn [i coll]
  (first (drop coll i)))
```
[Problem 22, Count a Sequence](https://4clojure.oxal.org/#/problem/22)
```clj
;; 1
(fn [xs]
  (apply + (map #(identity 1) xs)))
;; 2
(fn [xs]
  (reduce + (map #(identity 1)  xs)))
;; 3
(fn f [xs]
  (if (empty? xs) 0
    (+ 1 (f (rest xs)))))
;; 4
(fn [xs]
  (reduce +
    (map #(identity %2) xs (repeat 1))))
```

[Problem 23, Reverse a Sequence](https://4clojure.oxal.org/#/problem/23)
```clj
(fn reverse_ [xs]
    (if (= 1 (count xs)) (seq xs)
        (cons (last xs) (reverse_ (drop-last xs)))))
```

[Problem 24, Sum It All Up](https://4clojure.oxal.org/#/problem/24)
```clj
;; 1
reduce +
;; 2
apply +
;; 3 tail recursion?
(fn sum_ [xs]
  (if (empty? xs) 0
    (+ (first xs) (sum_ (rest xs)))))
;; 4 using accumulator
(fn sum_ [xs]
    (let [h (fn f [acc xs]
              (if (empty? xs) acc
                (f (+ acc (first xs)) (rest xs))))]
      (h 0 xs)))
```

[Problem 25, Find the odd numbers](https://4clojure.oxal.org/#/problem/25)

```clj
;; 1
filter odd?
;; 2
(fn [xs]
  (for [x xs
        :when (odd? x)] x))
;; 3
(fn [xs]
  (remove nil?
    (map #(if (= 1 (mod % 2)) %) xs)))
;; 4
keep #(if (odd? %) %)

```
[Problem 26, Fibonacci Sequence](https://4clojure.oxal.org/#/problem/25)
```clj
(fn [x]
    (let [fib-range (fn fib
        ([] (fib 1 1))
        ([a b] (lazy-seq (cons a (fib b (+ a b))))))]
            (take x (fib-range))))
```
[Problem 27, Palindrome Detector](https://4clojure.oxal.org/#/problem/27)
```clj
;; 1
(fn [xs]
  (reduce #(and %1 %2)
    (map #(= %1 %2) xs (reverse xs))))
;; 2
(fn [xs]
  (every? true?
    (map #(= %1 %2) xs (reverse xs))))
;; 3
(fn f [xs]
  (cond
    (empty? xs) true
    (= (first xs) (last xs)) (f ((comp rest drop-last) xs))
    :else false
    ))
```

[Problem 28, Flatten a Sequence](https://4clojure.oxal.org/#/problem/28)
```clj
;; 1
(fn f [xs]
  (cond
    (empty? xs) nil
    (coll? (first xs)) (concat (f (first xs)) (f (rest xs)))
    :else (cons (first xs) (f (rest xs)))))
```
[Problem 29, Get the Caps](https://4clojure.oxal.org/#/problem/29)
```clj
;; 1
(fn [xs]
  (apply str (re-seq #"[A-Z]" xs)))
```
[Problem 30, Compress a Sequence](https://4clojure.oxal.org/#/problem/30)
```clj
(fn [s]
  (map first (partition-by identity s)))
```
[Problem 31, Pack a Sequence](https://4clojure.oxal.org/#/problem/31)
```clj
;; 1
#(partition-by identity %)
;; same with
(fn [xs] (partition-by identity xs))
```
[Problem 32, Duplicate a Sequence](https://4clojure.oxal.org/#/problem/32)
```clj
;; 1
#(interleave % %)
;; same with 
(fn [xs] (interleave xs xs))
;; 2
(fn [xs] (mapcat list xs xs))
```
[Problem 33, Replicate a Sequence](https://4clojure.oxal.org/#/problem/33)
```clj
;; 1
(fn [xs n]
  (apply interleave (repeat n xs)))
;; 2 (from internet)
(fn [xs n]
  (mapcat #(repeat n % ) xs))
```
[Problem 34, Implement range](https://4clojure.oxal.org/#/problem/34)
```clj
;; 1
(fn [s f]
  (take (- f s) (iterate inc s)))
```
[Problem 35, Local bindings](https://4clojure.oxal.org/#/problem/35)
```clj
7
```
[Problem 36, Let it Be](https://4clojure.oxal.org/#/problem/36)
```clj
[x 7 y 3 z 1]
```
[Problem 37, Regular Expressions](https://4clojure.oxal.org/#/problem/37)
```clj
"ABC"
```
[Problem 38, Maximum value](https://4clojure.oxal.org/#/problem/38)
```clj
;; 1
(fn f
  ([x] x)
  ([x y] (if (> x y) x y))
  ([x y & more] (apply f (f x y) more)))
;; 2
(fn f [& xs]
  (reduce (fn [x y] (if (> x y) x y)) xs))
;; 3
(fn [& xs]
  (loop [
    res (first xs)
    args (rest xs)]
    (if (empty? args) res
    (recur (if (> res (first args))res (first args)) (rest args)))))
;; 4 (from internet)
(fn [& args]
  (-> 
  args
  sort
  last))
```

[Problem 39, Interleave Two Seqs](https://4clojure.oxal.org/#/problem/39)
```clj
;; 1
(fn [xs ys]
  (mapcat list xs ys))
```

[Problem 40, Interpose a Seq](https://4clojure.oxal.org/#/problem/40)
```clj
;; 1
(fn [n xs]
  (drop-last (interleave xs (repeat n))))
```
[Problem 41, Drop Every Nth Item](https://4clojure.oxal.org/#/problem/41)
```clj
;; 1
(fn [xs n]
  (loop [
    i 1
    ans []
    coll xs]
      (if (empty? coll) ans
      (recur (inc i) (if-not (= 0 (mod i n)) (conj ans (first coll)) ans) (rest coll)))))
```
[Problem 42, Factorial Fun](https://4clojure.oxal.org/#/problem/42)
```clj
;; 1
#(reduce * 1 (range 1, (inc %)))
;; 2
(fn f [n]
  (if (zero? n) 1
  (* n (f (dec n)))))
;; 3
(fn [n]
  (loop [
    ans 1
    x n
  ]
  (if (zero? x) ans
    (recur (* ans x) (dec x)))))
```
[Problem 45, Intro to Iterate](https://4clojure.oxal.org/#/problem/45)
```clj
;; 1
'(1, 4, 7, 10, 13)
;; 2
(range 1, 14, 3)
```
[Problem 46, Flipping out](https://4clojure.oxal.org/#/problem/46)
```clj
;; 1
(fn [f]
  (fn [a b]
    (f b a)))
;; 2 using anonymous function to make ti short
(fn [f]
  #(f %1 %2))
;; 3 from internet
(fn [f]
  (fn [& args] (apply f (reverse args))))
;; 4 from internet
(fn [f]
  (fn [& args]
    (->> args
      (reverse)
      (apply f)))) 
```
[Problem 47, Contain Yourself](https://4clojure.oxal.org/#/problem/47)
```clj
;; 1
4
```
[Problem 48, Intro to some](https://4clojure.oxal.org/#/problem/48)
```clj
;; 1
6
```
[Problem 49, Split a sequence](https://4clojure.oxal.org/#/problem/49)
```clj
;; 1 i don't know why it's wrong
(fn [n xs]
  (juxt 
    (partial take n)
    (partial drop n)) xs)
;; 2 still wrong
(fn [n xs]
  (juxt 
    (comp vec (partial take n))
    (comp vec (partial drop n))) xs)
;; 2 the right one
(juxt take drop)
;; now i know the right one
  (juxt 
    (comp vec take)
    (comp vec drop))
```
(Problem 51, Advanced Destructuring)[https://4clojure.oxal.org/#/problem/51]
```clj
[1 2 3 4 5]
```
(Problem 52, Intro to Destructuring)[https://4clojure.oxal.org/#/problem/52]
```clj
[c e]
```
(Problem 56, Find Distinct Items)[https://4clojure.oxal.org/#/problem/56]
```clj
(fn [xs]
  (loop [
    y (first xs)
    ys [y]
    zs (rest xs)]
    (letfn [(in? [v coll] (some #(= v %) coll))]
      (if (empty? zs) (if (in? y ys) ys (conj ys y))
        (if-not (nil? (in? y ys))
        (recur (first zs) ys (rest zs))
        (recur (first zs) (conj ys y) (rest zs)))))))
;; 2

```

(Problem 57, Simple Recursion)[https://4clojure.oxal.org/#/problem/57]
```clj
[5 4 3 2 1]
```
(Problem 58, Function Composition)[https://4clojure.oxal.org/#/problem/58]
```clj
;; 1 still not passed all the test
(fn [& fs]
  (fn [& args]
    (reduce #(apply %2 %1) args (reverse fs))))

;; 2
(fn [& fs]
  (fn [& args]
    (let [
      val (apply (last fs) args)]
      (letfn [
        (f [acc fs] (if (empty? fs) acc (f ((last fs) acc) (drop-last fs))))] (f val (drop-last fs))))))
```

(Problem 60, Sequence Reductions)[https://4clojure.oxal.org/#/problem/60]
```clj
(fn [f xs]
  (let [v (f (first xs))]
    (letfn [
      (g [acc zs]
      (let [val (f acc (first zs))]
        (lazy-seq (cons acc (g val (rest zs))))))]
        (g v (rest xs)))))

```

(Problem 61, Map Construction
)[https://4clojure.oxal.org/#/problem/61]
```clj
;; 1
(fn [xs ys]
  (apply hash-map (interleave xs ys)))
;; 2 (from other solution the idea is the same with mine)
(fn [xs ys]
  (into {} (map vector xs ys)))
;; 3 from internet
(fn [xs ys]
  (apply merge (map hash-map xs ys)))  
```
(Problem 62, Re-implement Iteration
)[https://4clojure.oxal.org/#/problem/62]
```clj
;; 1
(fn iterate' [f init-val]
  (lazy-seq (cons init-val (iterate' f (f init-val)))))
```
[]()
```clj
(fn [pred coll]
  (reduce #(assoc %1 (pred %2) %2) {} coll))
```
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
    (= 1 (count xs)) true
    (= (first xs) (last xs)) (f ((comp rest drop-last) xs))
    :else false
    ))
```
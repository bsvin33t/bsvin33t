# On calculating PI programmatically.

I want to calculate Pi to the nth place. I figured, doing `22/7` would be sufficient. Apparently, that is not the value of Pi.

Thus started my adeventure on finding the value of Pi.

On the way, I discovered `Taylor Series` which tells, `Pi/4 = 1 - 1/3 + 1/5 - 1/7 + ...` from this [stackoverflow post](https://stackoverflow.com/questions/2654749/how-is-pi-%CF%80-calculated)

Oh man, what a mess. I programmed something similar and the test started to fail 😭😭😭

``` clojure

(defn pi-to-nth [number]
  (let [odd-numbers (filter odd? (iterate inc 1))]
    (* 4.0
       (apply + (map / (cycle [1 -1]) (take number odd-numbers))))
    ))
```

But it was fun writing this and discovering that I have been sorely mistaken with the approach 
where I should not just do the number of iterations based on the number that is passed,
but also use the method as an approximation for generating the digits.

As of now, I'm exploring the `atan` method of getting the value of pi

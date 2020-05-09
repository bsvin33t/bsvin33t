# Pre and Post in clojure

Woah! Nice feature, in clojure `pre` and `post` allows me to validate the input coming into the function and the output that is going out of the machine.

On one hand, I see that it raises an error when validating the input and output. Even though this seems like a nice feature, 
I'm not entirely convinced by raising an error whenever I find something wrong with my input, especially, when I expect the
"wrongness" in my input. 


I think having the `post` might be ok. But still, I'm not so sure if I will use this(but hey! what do I know, I have only written a handful of clojure code :) )


```clojure
(defn small-sqrt [x]
  { :pre [(pos? x)]
   :post [(< % 10)] }
  (Math/sqrt x)
  )
```


{:title "Foldr vs foldl"
 :layout :post
 :tags  ["functional-programming folding"]}

Folding is one important topic in functional programming. It is a pattern exploiting the higher-order capability to compose functions, i.e. functions can be passed other functions arguments or can return a function. This pattern is used to employ common iterative operations over lists which reduce to a single result. This is in fact the algorithm behind the common library function *reduce* implemented in most common programming languages nowadays. There are two variants of folding depending on the direction in which the computational process unfolds, so either right or left. This gives the names of *foldr* and *foldl*. The examples that follow will be written in Haskell for conciseness. I advice the book by Hutton [^1] to have an introduction to these concepts or the  edX MOOC [^2] which also provides plenty of exercises to consolidate the knowledge.

# Foldr
The formula used to express this pattern is the following one, written in Haskell [^1] (the type signature is omitted for simplicity purposes):
```
foldr f v [] = v
foldr f v (x : xs) = f x (foldr f v xs)
```
Even though it may look daunting at first sight, it becomes very clear and intuitive once you have grasped the meaning of it. This formula is written in recursive form, so the first line expresses the base case while the second line expresses the recursive case. The left-hand side of the formula is the application of the function `foldr` on parameters
 -  `f`, the name of the function
 - `v` , the initial value
 - `[]` is the empty list; the base case means that at this point of the computation there are no more elements in the list to consider
 - `(x : xs)`, which is the Haskell notation to express a list composed of head (first element) `x` and tail (all elements from second to last) `xs`

Now for the interesting part, the right-hand side of the formula. In the base case, the function simply returns the initial value. Easy. In the recursive case, function `f` is applied to the first element of the list `x`. After that, the `foldr` function is called recursively on the remaining elements of the list.
Now it is clear that the computational process of `foldr` has a recursive shape.
Let's make an example to illustrate what previously said.
Turns out that the common higher-order pattern `map` can be rewritten in terms of `foldr`:
`mapR f = foldr (\ x xs -> f x : xs) []`.
Here the application of function `f` over the list is defined in terms of an anonymous function (lambda function) taking two parameters `x` and `xs`. The empty list `[]` is  the initial value (`v` in the formula above). `x` represents the first item in the list starting from the end of the list, while `xs` represents the accumulator. So the lambda function returns a list composed of the function application on element `x` concatenated with the accumulator `xs`. To properly understand how the computation unfolds, I find it more intuitive to reason backwards, starting from the last element moving backwards to the first; the accumulator is then compounded starting with the empty list on the right and prepending the elements of the list one by one starting from the last element. For example applying `map` on list `[1,2,3]` taking function `(*2)` gives the list `[2,4,6]`:
```
map (*2) [1,2,3]
((*2) 1) : ((*2) 2) : ((*2) 3) : []
2 : 4 :  6 : [] = [2,4,6]
```

# Foldl
The formula used to express this pattern is the following one, written in Haskell [^1] (the type signature is omitted for simplicity purposes):
```
foldl f v [] = v
foldl f v (x : xs) = foldl f (f v x) xs
```
This function shares many similarities with the one expressed above for `foldr`. The difference lies in the right-hand side of the recursive case formula. `foldl` is called recursively, and it is given the following arguments:
 - `f`, the function
 - `(f v x)`, is the accumulator, which is given by the application of `f` on the previous value of the accumulator `v` and the first element of the list `x`
 - `xs`, the remaining elements of the list starting from the second one

It is clear that `foldl` follows an iterative shape instead, as the algorithm starts by applying the function to the base case and the first element of the list; this is the new accumulator. Then the function is applied to the next element and the accumulator, which results in a new accumulator. This process continues until the end of the list is reached. Note that I have not said that the accumulator assumes a new value at each step, because the evaluation is done after the unwrapping of the list starting from right to left, which gives the name to the pattern.
For symmetry, I am going to express the function `map` using `foldl`:
`mapL f = foldl (\ xs x -> xs ++ [f x]) []`.
The lambda function takes two parameters: `xs` is the accumulator, while `x` is the first element of the list. A list is returned, composed of the application of `f` on `x`, to which is prepended the accumulator `xs`. Note that the accumulator is the initial value `[]`. So the computation unfolds from left to right, and once the end of the list is reached, it starts folding back from right to left, hence the name. Applying `map` on list `[1,2,3]` taking function `(*2)` gives the list `[2,4,6]`:
```
map (*2) [1,2,3]
(([] ++ [(*2) 1]) ++ [(*2) 2]) ++ [(*2) 3]
[] ++ [2] ++ [4] ++ [6] = [2,4,6]
```




[^1] [http://www.cs.nott.ac.uk/~pszgmh/pih.html](http://www.cs.nott.ac.uk/~pszgmh/pih.html)
[^2] [https://www.edx.org/course/introduction-functional-programming-delftx-fp101x-0](https://www.edx.org/course/introduction-functional-programming-delftx-fp101x-0)
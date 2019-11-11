{:title "Function closures"
 :layout :post
 :tags  ["closures functional-programming"]}

The topic of this post is function closures. Closure refers to the context that is passed to a function when it is defined. Basically, the state of the variables that are in the lexical scope when the function is defined is captured and retained in the function. Thus, when the function is subsequently invoked, the variables referenced by the function retain the value they possessed in the lexical scope of the function when it was defined, even though the current scope may be completely different! In Javascript we could write for example:
```
let x = 4;
let f = y => y + x;
...
x = 7;
f(2); // this will return the value 6
```
As visible from this simple example, the variable `x` is in the lexical scope of the function `f` at the moment of its declaration and is bound to the value `4`. At a later point in the program the value of the variable `x` is changed to `7`, and the variable `x` is in the lexical scope when the function is invoked in the last line. However, the result of the function application is `6` instead of `9`. The reason for this is that function `f` had a closure over `x` when `f` was defined, so no matter what value `x` may have in the future, it is still bound to `4` any time `f` is invoked. The same would be valid even if `x` would not be in the current scope at the moment function `f` is invoked.
This simple example illustrated an important feature of closures: functions can store the information present in the lexical scope where they are defined. The implications of this are huge, and many idioms and patterns have found foundation from this concept.

# Currying

# Memoization
The memoization technique is useful when you want to cache the result of some expensive computation. It basically consists in storing a local reference inside a function to a variable defined outside the function; its value is going to be used in some expensive computation. The first time the function is invoked, you may check whether the variable is defined (you may also use a boolean flag for the purpose of checking), and since it is not, the function body is evaluated to produce the result of the computation which is going to be stored in a local variable. So, any subsequent times the function is called, the function will limit itself to return the result of the computation instead of recomputing it every time.

# Library wrapping
Another example of pattern commonly employed in Javascript is library wrapping, also known with the name of revealing module pattern, and it is used to create a module abstraction in an environment were every element would have public visibility otherwise.
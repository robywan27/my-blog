{:title "Programming paradigms explained"
 :layout :post
 :tags  ["fundamentals"]}

The topic of this post concerns something fundamental in the matter of programming: programming paradigms. Note that, while there exist other paradigms other than the ones considered here, these will not be treated as they are out of the scope of this post.
We will first consider the two main approaches overarching all the other paradigms: imperative and declarative. I also advice to have a look at the definitions provided in the very first chapter of *Structure and Interpretation of Computer Programs* [^1] for a very good explanation of the difference between the two.

# Imperative
Imperative is concerned with the *how-to* knowledge of an algorithm, i.e. it details the sequence of steps or instructions necessary to accomplish a certain algorithm. An analogy to visualise this could be for example the following sequence of instructions to go from point A to point B:
```
move two cells to the right
move one cell to the top
move five cells to the right
...
```

# Declarative
Declarative deals instead with the *what-is* knowledge, thus it provides a definition but does not specify the steps for a certain algorithm. This approach is more proper to mathematics, mathematical formulae are a very good example of declarative knowledge. For instance, to calculate the hypotenuse of a right triangle you could use the Pythagorean theorem `c^2 = a^2 + b^2"`. Note that it does not give you a list of instructions of how to calculate the hypotenuse, just a definition.

# Main paradigms
Now we will consider the most common paradigms.

# Procedural
This is the paradigm used to indicate those programs in which the code is organised into logical units called procedures. Contrarily to functions, procedures do not return any value, but act simply as groupings of instructions. This style of programming is the first to have been employed and dates back to Fortran. The main merits of this paradigm is that of introducing modularity and scoping into programs. Note that this style is purely imperative.

# Object-oriented
Object-oriented is perhaps the most well-known paradigm since it has been since the late '80s-'90s the de-facto standard in the industry. This style differs from the procedural in that it introduces several concepts such as class, interface, inheritance, polymorphism which add layers of abstraction to the program and model the reality with entities interacting between each others. Their interactions cause mutations in the state of the objects, which can lead to untameable complexity if not properly managed and kept under control with the proper amount of testing. A complete treaty of this paradigm is out of the scope of this post, as there are loads of good resources out there explaining exhaustively OO concepts [^2].  This style of programming is imperative.

# Functional
According to this paradigm, programs should be composed of pure functions and immutable data structures. Pure functions are functions which do not cause any side effect, i.e. they do not change the state of the program. Immutable data structures indicate that any data structure in the program is not mutated; in order to perform computations on these structures, copies are made and acted on. Another characteristic of the functional style is that functions are first-class citizens, i.e. they can be treated as any other value, thus assigned to variables, passed around in functions either as arguments or return values, etc. This makes the program more declarative since you define the specification of a computational process through pure functions and their composition instead of defining the sequence of instructions which implements the required computational process.
Note that for real applications a purely functional approach by itself is pretty much useless, as the program would just act as a box computing things but without any connection with the outer world. For this reason, even pure functional languages such as Haskell provide mechanisms to deal with state mutation or side effects. This comes to the cost of losing the declarative quality typical of functional programs.
An example of this in Haskell is the `do` block for monads, useful to deal with side effects:
```
do
	putStrLn "hello"
	putStrLn "world"
```
Another example is the `begin` block in Scheme or Racket to express sequences of instructions:
```
(begin
  (printf "hello")
  (+ 1 2))
```





[^1] [https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book-Z-H-10.html](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book-Z-H-10.html) 
[https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/video-lectures/1a-overview-and-introduction-to-lisp/](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/video-lectures/1a-overview-and-introduction-to-lisp/)
[^2] [https://www.goodreads.com/book/show/4845.Code_Complete](https://www.goodreads.com/book/show/4845.Code_Complete)
[http://propella.sakura.ne.jp/earlyHistoryST/EarlyHistoryST.html](http://propella.sakura.ne.jp/earlyHistoryST/EarlyHistoryST.html)
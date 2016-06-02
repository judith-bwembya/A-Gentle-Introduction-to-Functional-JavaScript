# A Gentle Introduction to Functional JavaScript #

Functional Programming tends to intimidate people at first with the scary names it borrowed from Category Theory to describe interfaces known as _"Algebraic Structures"_. It's application in JavaScript is further obfuscated by many different pre spec examples and implementations much the same way Promises developed pre A+ spec. The current de facto specification is called ["Fantasy-land"](https://github.com/fantasyland/fantasy-land) only dates back to April, 2013. With out a spec people create different names for the same functions and libs are not compatible.

JavaScript was not designed to be functional programming language. It had to adopt this paradigm from other languages. As it turns out JS is well suited to the the task thanks to first class, higher-order functions and now in ES2015 proper tail-call optimization.

The more abstract a concept is the harder it is to understand. Interfaces are abstract by nature. The more abstract they are the more powerful they become because they allow us to solve a wider range of seemingly unrelated problems with a surprisingly small set of patterns.

Functional Programming is worth striving for, and that's the good news. You don't have to flip a switch and go functional. You can apply bits and peaces as you learn them. I have been slowly building up my functional play book over the past 3 years. As a result every refactor becomes a lot more enjoyable.

__Why should I care about immutability?__ Transistors cannot get any smaller. Clock rates plateaued in 2004. Multi-core is currently the preferred strategy for improving speed. If your code is not thread-safe it cannot be distributed in parallel across multiple cores. Shared mutable state is not thread-safe. See [Robert Martin's talk](https://www.youtube.com/watch?v=7Zlp9rKHGD4) on this topic. Just note: an "assignment statement" is totally benign a "reassignment statement" is problematic.

When you reassign (mutate) a variable you are introducing state change. To reproduce a complex bug you often need the sequence of computations that lead to the failure. When you mutate variables you are throwing away that sequence.

__How do avoid state?__ Any time you need to model a state change you pass the previous value to a function that returns a new value.

Imagine a banking application. If you create an account object that holds a balance variable and mutates it every time you deposit or withdraw money you have no way generating a monthly bank statement listing all of your activity without implementing that functionality. If you return a new account object with an updated balance you will accumulate a history of the exact sequence that lead up to the current balance. That can be pretty useful ...

Check out "Time Travel Debug" from Redux DevTools
![redux](https://cdn-images-1.medium.com/max/1600/1*BTRxlHu8WuCF4Iep4R44lA.gif "Redux DevTools")

----------------
### Glossary ###

__First-Class Functions__ The ability to assign a function to a variable.

__High-Order Functions__ Functions that can take and return functions.

__Side Effects__ When a function mutates state outside it's scope.

__Purity__ A function with no side effects that maps every input to exactly one corresponding output. One of the many benefits of a pure function, and a good to test of purity, is that it can be cashed.

__Imperative vs. Declarative__ A `for` loop is a very specific solution to looping. We call this _"imperative"_ because we are explaining _how_ to do the loop. With `Array.prototype.map` we are declaring _what_ we want. If I discover a more optimal way to map I can refactor my map function with out breaking all the code that calls it. We call this _"declarative"_. So if you want to know if you are writing declarative code ask your self if you can refactor it with out breaking the code that calls it.

__Arity__ The number of parameters a function takes.

__Partial Application__ A function with an incomplete set of parameters.

__Currying__ A curried function that is passed fewer parameters than it's arity will return a partially applied function that will delay execution until it has been passed all of the required parameters.

__Point Free__ A style where we strive to pipe data from the output of one function to the input of the next avoiding named parameters. It is more concise, easier to read.

__Composition__ Chaining functions together by piping the output of one function to the input of the next in the composition. Composing pure functions will respect the law of associativity. This will allow us to safely apply some optimizations to our code.

__Associativity__ A binary operation in which the order of evaluation is not important. Addition of whole numbers is associative.

```
const a = ( 1 + 2 ) + 3; // 6
const b = 1 + ( 2 + 3 ); // 6
a === b; // true
```

Subtraction of whole numbers is not associative.

```
const a = ( 1 - 2 ) - 3; // -4
const b = 1 - ( 2 - 3 ); // 2
a === b: // false
```

__Container__ an object that you can place a value in with a function that takes a function as an argument that will allow use to perform transformations using that value as input and returning a new container with the result as output.


### Part One Homework ###

The patterns we will cover in Part Two are built on some simple and familiar building blocks. Probably the most common pattern in computing is the concept of and _Item_ and a _Collection_. When you write a function that will transform some input to some output it should be operating on an _Item_ not a _Collection_ because we have a way of mapping over a _Collection_ and applying that function to each _Item_.

[This is an excellent tutorial](http://reactivex.io/learnrx/) written by Jafar Husain, tech lead at Netflix. It should take you a few hours and will give you skills you can apply immediately.

Explore some of the FP utility libraries out there:

* [ramda](http://ramdajs.com)
* [lodash/fp](https://github.com/lodash/lodash/wiki/FP-Guide)

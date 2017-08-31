Functional programming produces programs by composing mathematical functions and avoids shared state & mutable data. Lisp (specified in 1958) was among the first languages to support functional programming, and was heavily inspired by lambda calculus. Lisp and many Lisp family languages are still in common use today.
In functional programming, a program is an expression that is composed by other function.

Pros:
- Using the functional paradigm, programmers avoid any shared state or side-effects, which eliminates bugs caused by multiple functions competing for the same resources. With features such as the availability of point-free style (aka tacit programming), functions tend to be radically simplified and easily recomposed for more generally reusable code compared to OOP.
- FP also tends to favor declarative and denotational styles, which do not spell out step-by-step instructions for operations, but instead concentrate on what to do, letting the underlying functions take care of the how. This leaves tremendous latitude for refactoring and performance optimization, even allowing you to replace entire algorithms with more efficient ones with very little code change. (e.g., memoize, or use lazy evaluation in place of eager evaluation.)
Computation that makes use of pure functions is also easy to scale across multiple processors, or across distributed computing clusters without fear of threading resource conflicts, race conditions, etc…

Cons:
- Over exploitation of FP features such as point-free style and large compositions can potentially reduce readability because the resulting code is often more abstractly specified, more terse, and less concrete.
- More people are familiar with OO and imperative programming than functional programming, so even common idioms in functional programming can be confusing to new team members.
- FP has a much steeper learning curve than OOP because the broad popularity of OOP has allowed the language and learning materials of OOP to become more conversational, whereas the language of FP tends to be much more academic and formal. FP concepts are frequently written about using idioms and notations from lambda calculus, algebras, and category theory, all of which requires a prior knowledge foundation in those domains to be understood.

## Pure Functions
A pure function's return value is determined only by its input values (arguments) with no side effects. When given the same argument, the result will always be the same.

In summary:
- Pure functions must take arguments.
- The same input (arguments) will always produce the same output (return): they are predictable and easy to test.
- Pure functions rely only on local state and do not mutate external state.
- Pure functions do not produce side effects.
- Pure functions cannot call impure functions.

## Impure Functions
An impure function mutates state outside its scope. Any function that has side effects (see below) is impure. Procedural functions with no utilized return value are also impure.

## State
State refers to the information a program has access to and can operate on at a point in time. This includes data stored in memory as well as OS memory, input/output ports, database, etc. For example, the contents of variables in an application at any given instant are representative of the application's state.

## Stateful
Stateful programs, apps, or components store data in memory about the current state.

## Stateless
Stateless functions or components perform tasks as though running them for the first time, every time. This means they do not reference or utilize any information from earlier in their execution. Statelessness enables referential transparency.

## Immutable
If an object is immutable, its value cannot be modified after creation.

## Mutable
If an object is mutable, its value can be modified after creation.

## Higher-order Function
A higher-order function is a function that:
- accepts another function as an argument
- returns a function as a result.

## Currying
A common technique in FP is currying. Currying is the process of converting a function that
takes multiple arguments into a function that takes one argument at a time, returning
another function.

Let's look at an example to clarify the concept.
Instead of writing:
```javascript
const add = (x, y) => x + y
```

We define the function like this:
```javascript
const add = x => y => x + y
```

And we use it in the following way:
```javascript
constadd1 = add(1)
add1(2) // 3
add1(3) // 4
```

This is a pretty convenient way of writing functions because since the first value is stored
after the application of the first parameter, we can reuse the second function multiple times.

## Composition
Functions can be combined to produce new functions with more advanced features.

## Structural sharing
In functional languages, every data is immutable by design. This can seems very slow for complex data, but this is can be healed using structural sharing: every time we do an action on a data, it recycle everything it can from the old data. This opens a new class of data strctures called persistent immutable data stractures.

## Memoization
Memoization is memorize a deterministic result of a pure function -> Pure.
Caching, is impure by design: we can cache something that change during the time. Deciding when change the cache is an indecidible problem.

## Referential trasparency ?

## Tail call elimination ?
Tail call is the last thing that a function does. Teoretically the compiler could figure out a tail call, so a function instead of returning itself can return the tail call. The elimination of that stack frame is tail call elimination.
It's really important in functional programming because we want to compose many function, but if we do not tail call elimination, this can cause the computer to crash do too many stackframes.

Benefit 1: Pure functions are predictable

When a function isn’t pure, it has the potential to act unpredictably. For example, in our calculateArea function in Example 2 from yesterday's lesson:

const PI = 3.14;
const calculateArea = (radius) => radius * radius * PI;
...you saw how this original impure function was reliant on a global variable PI to calculate the result.

What makes this function unpredictable, you might ask? Well, since the PI variable is global and anyone can update it, there’s nothing to stop your evil co-worker from changing it to 300,000. Outlandish results would ensue anytime we tried to use the function to calculate the area of a circle. No bueno.

Similarly, imagine a function with a side effect that logs to console or writes to a file. This is unpredictable because there’s no guarantee of success. For example:

const fs = require('fs');

fs.writeFile("/tmp/myFile", "Hey there!", (err) => {
  if(err) return console.log(err);
  
  console.log("File saved successfully!");
});
Above, we have a function that writes “Hey there!” to a file named myFile. But what if myFile doesn't exist? Or if the file has restricted access, making it not writeable? Or if the file path is incorrect? Or any infinite number of other I/O related failures that the function has no control over? The function would throw an error.

Long story short: impure functions tend be unpredictable. 

With that in mind, it’s easy to see why you’d want to avoid writing functions that rely on external state. The resulting functions are much more predictable. Ideally, the only things a pure function needs to work properly are the arguments passed to it explicitly. Full stop.


Benefit 2: Pure functions are easy to test

When you know that a function doesn’t ever rely on something outside it’s scope, it becomes easier to test. On the flip side, impure functions are much harder to test.

For instance, if we wanted to test our impure amountExceedsBuyLimit function, we can't simply pass in an amount and test that it returns the right output. Why? Because the function makes an external API call. We'd have to somehow mock the API call so that the function doesn't throw an error when we try to invoke it for the test:

describe('amountExceedsBuyLimit', () => {
  let scope, limits;
  
  /* Mock API call */
  before(() => {
    scope = nock('https://myApi.com');
    scope
      .get('/buyLimit')
      .matchHeader('Content-Type', 'application/json')
      .reply(200, {
        buyLimit: 5000,
      });
  });

  /* Clean up mock */
  after(() => {
    nock.cleanAll();
  });

  /* ... Finally, test the function */
  it('should be false', () => {
    const amountExceedsLimit = amountExceedsBuyLimit(200);
    expect(amountExceedsLimit).to.be.false();
  });

  it('should be true', () => {
    const amountExceedsLimit = amountExceedsBuyLimit(10000);
    expect(amountExceedsLimit).to.be.true();
  });
});
Not so pretty and expressive is it? Testing our pure function, on the other hand, is much easier because we can skip all the API mocking:

describe('amountExceedsBuyLimit', () => {
  it('should be false', () => {
    const amountExceedsLimit = amountExceedsBuyLimit(200, 1000);
    expect(amountExceedsLimit).to.be.false();
  });
  
  it('should be true', () => {
    const amountExceedsLimit = amountExceedsBuyLimit(10000, 1000);
    expect(amountExceedsLimit).to.be.true();
  });
});
Much better! Clean, short and simple. 😌

There are plenty of other reasons to use pure functions in functional programming. Beyond being easier to refactor and debug, pure functions are also deterministic and well-suited for parallel processing.

We won’t have time to cover each of these additional advantages in this course, but I’m currently working on in-depth material on them for my full course, “Mastering Functional JavaScript” (to stay up to date on details, sign up for the course here).

Overall, pure functions offer a lot. That being said, it’s not generally possible to completely eliminate impure functions from our code. In practical applications, there will always be use cases for pure and impure functions — both are necessary to model the real world. The trick is recognizing when to use them.

For example, calculating the area of a circle should always be a pure function. By definition, PI is a constant and always 3.14159… and the area of a circle with radius 2 should always calculate to 12.56636.

A function that calculates the conversion price of 1 Bitcoin to U.S. dollars, on the other hand, is impure by nature — because it’s dependent on the variable price of Bitcoin, which is determined by a number of external variables. There’s no way we can expect to get the same value for the conversion price at different times.

Our ultimate goal here as functional programmers is not to eliminate side effects, but confine them. We strive to minimize the amount of impure code, and segregate it from the rest of our program.

So far we’ve covered the “what” and “why” of pure functions. We’ll dive into the “how” side of things later in my full course — especially in the latter half, where we’ll start to build real-world applications with real-world interfacing… and all the side effects that entails. 

…But what exactly is immutable data, and why does it matter? What does “immutable” even mean, anyway?

Never fear — answering those questions is the topic of today’s lesson. 😊

If you look up “immutable” in the dictionary, you’ll get something like this:

“Unchanging over time or unable to be changed.”

When data is immutable, it’s state cannot change after it’s created. If you want to change an immutable object, you don’t. Instead, you create a new object with the changed value and point your reference to it. 
myString is immutable, so you can’t simply mutate the string from “hello” to “hello world”Instead, create a new string with the changed value and point your reference to it


Another way to think about this is that, in functional programming, there is no concept of a “variable” — meaning literally that data doesn’t “vary” over time. Instead, everything is a “constant.” Once created, nothing changes. 

This seems counterintuitive at first compared to the variable-based mutable data we all know from programming 101. 

In JavaScript, all primitive types are inherently immutable. Primitive types include String, Number, Boolean, Null, Undefined, and Symbol. 

Let’s take a deeper look at the implications here using strings as an example. 

Below, we have a simple string assigned to a variable firstName:

var firstName = "Preethi"
Let’s say I got a little bored one day and decided I want it to spice it up a bit by changing the second e in my name to an i.

firstName[3] = "i";
console.log(firstName[3]) // "e"
console.log(firstName) // "Preethi"
Hmm, looks like it won’t let me update my name.

The reason it won’t update to an i is because, as we just learned, strings are immutable.

Once I’ve created and assigned a string value to the variable firstName, I can't just tweak it’s value as I see fit. (Side note: In this example, the update failed silently. If we were in strict mode, we would've gotten a TypeError saying:

TypeError: Cannot assign to read only property '3' of string 'Preethi'
Suppose I had another boring day, but this time I decided to spice things by slicing off the thi from my name to make a nickname: Pree.

firstName.slice(0, 4);
console.log(firstName) // "Preethi"
What the?! I can’t do that either?

Once again, strings are immutable, and updating after creation isn’t an option. Any string manipulation methods (e.g. slice, trim, concat, etc.) will always return a new string without modifying the existing string.

So if I wanted to change my name for real, I’d simply have to create a new variable firstName2 for the purpose, and assign a new string to it:

var firstName2 = firstName.slice(0, 4);
// new string "Pree" is created and assigned to firstName2
console.log(firstName2) // "Pree"
Problem solved!

But wait, before we move on, let’s discuss one more subtle point. If you’ve been paying close attention, you might say, “Well, Preethi. You’re wrong. I can mutate firstName by simple doing…”

firstName = firstName.slice(0, 4);

console.log(firstName) // "Pree"
“Doesn’t this mean the string IS mutable??,” you ask.

Well, not really. Here’s why:

firstName is a JavaScript variable. At the beginning, it holds a reference to the value “Preethi”. Then what we did above is simply change the reference of firstName to be “Pree”. Nothing happened to the original value “Preethi” — it’s simply that but there wasn’t a reference to “Preethi” stored in firstName any more.

So, there’s two completely different things happening here: mutation vs. assignment. Mutation modifies the underlying object without affecting the link between the variable and the object, whereas assignment changes the link to a different object, but doesn’t modify any objects.

So by doing firstName = “something else all together”, we are simply reassigning and not actually mutating.

So now we know what it means for data to be immutable. We’ve seen how primitives in JavaScript — such as strings — are immutable. 

…The other data type in JavaScript, the big ol’ Object, is the opposite: objects are mutable in JavaScript. With Objects, the properties can be added and removed at will. Let's look at an example:

var me = {
  name: "Preethi",
  age: 26,
  city: "San Francisco",
};
/* ... 5 years later ... */
me.age = me.age + 5;
console.log(me) // { name: 'Preethi', age: 31, city: 'San Francisco' }
Here, we had an object that represented me with properties for my name, age, and city. 5 years later, I'm 5 years older (and in my 30s, yikes!), so we go ahead and update my age.

Whoa, whoa, whoa. So you're telling me we can just rewrite the history of my existence? I can't ever go back and check what my object looked like a year ago? or two years ago? or five years ago? 

Yep, that's right. That's what mutability means — it let's you update, rewrite or erase things over time.

So far, we talked about primitives and objects in JavaScript, but you might be wondering about Arrays. Are they mutable or immutable? Well, Arrays are just Objects in JavaScript. Like objects, they are mutable. 

Here’s where functional programming and JavaScript clash a bit: functional programming aims to use immutable data, but JavaScript doesn't have built-in immutable objects. Basically, we need a way to make objects in JavaScript immutable.

Luckily, there are a few different options: we can use Object.freeze, or turn to external libraries like Immutable.js and seamless-immutable. They both give us ways to create immutable objects in JavaScript.

A large library like Immutable.js is outside the scope of a small email course, but it’ll definitely be on the agenda for the full-length course. For now, let’s look at a quick example of how we can use Object.freeze to create immutable objects “on the fly.” 
Object.freeze

As you might guess, the Object.freeze method “freezes” an object. Existing properties can't be changed or removed and new properties can't be added. The object is literally frozen.

If you try to update it, it will either fail silently or throw a TypeError (if we’re working in strict mode.)

var me = {
  name: "Preethi",
  age: 26,
  city: "San Francisco",
};
var meImmutable = Object.freeze(me);
/* ...5 years later ... */
meImmutable.age = meImmutable.age + 5;
console.log(meImmutable) // 
{ name: 'Preethi', age: 26, city: 'San Francisco' }
Notice how this time, because we created a frozen/immutable version of the me object, the age property doesn't get updated. Instead, it fails silently and keeps the object intact.

If we were strict mode (add ‘use strict’ at the top to try for yourself), it would have thrown an exception saying:


TypeError: Cannot assign to read only property 'age' of object <span style="font-size: 11.34px;">'#<Object>'</span>



Why does immutability matter?

The obvious next question is: why does functional programming use immutable data in the first place?

In short, immutable data is important because we need to be able to attach dependable, unchanging values to our functions. Say you have a value 2. You can’t wake up one day and decide that the 2 is going to be a 22 instead. It just doesn’t make sense. 😆 

Something crazy happens when you treat all data as fixed values: the concept of time goes away.

Goodbye to side-effects that can change an expression’s value. Goodbye to worrying about whether some piece of data is the same as what you expected it to be. When you have this guarantee, functions can now be evaluated at any time and in any order and the result is guaranteed to always be the same. 

Let’s go back to the example with the object that represents me.

If I wanted to get the updated object 5 years later, I’m guaranteed that my reference to the me object has not changed in the last five years. I can safely update it by creating a new object with the updated age, simply pointing my reference to it.

… But if the me object allowed mutations, a mean-spirited coworker could update my age to 60 behind my back, leaving me at 65 when I unwittingly add 5 years to that value in 2021. Oh boy 🙄

Overall, there are many other benefits to immutability in functional programming. They make values easy to share, they make it safer and easier to do concurrent programming, they avoid temporal coupling, they eliminate defensive copies, and much more. I’ll cover some more of this concept in the full course, so hold tight! 😌 

Is mutability always a bad idea?


Perhaps I’ve given mutability a bad rap — it’s not all shaky foundations and accidentally turning 65!

Mutability isn’t always a bad idea — in fact, whenever you hear someone say something is “always” bad or “always” good in programming, I recommend you take it with a grain of salt.

In the case of mutability, there are situations where it’s more straightforward to implement the domain model using mutable objects to represent real-world entities that change over time. We’ll explore these situations in depth in the full-course, Mastering Functional JavaScript.

To recap, a pure function is one that only relies on what is explicitly passed to it as arguments and doesn’t cause any side effects. Purity, defined in this way, means that there is a pure mapping between a function’s inputs and outputs. There’s no other external input.



This mimics the notion of a “function” you probably learned in high school algebra. Operations like square, square root, sine, and cosine are actually pure functions. Which means you’ve been doing functional programming since grade school! 😏

So long as we’re bringing back high school references, we may as well use some algebra to demonstrate the concept we’ll be learning today: referential transparency. 

Let’s say we have a function that squares a number:

f(x) = x * x
If I were to pass 4 into this function, I’d get:

f(4) = 16
Let’s do that a few more times:

f(4) = 16
f(4) = 16
f(4) = 16
I can run this 100 times. I can run this 100 years from now. I can run it on the moon, in Antarctica, or dancing in my PJs. It will always return 16. 

Well, if that’s the case… then logically it follows that anytime we see the number 16, we can replace it with f(4), right? 

Surprise! You just learned what referential transparency is! 👏

If a function consistently yields the same result for the same input, it is referentially transparent. 

At this point you might be wondering: “well, doesn't every function return the same result for the same input?”.

…Well, not exactly. Consider this case:

function getRandomNumber(min, max) {
  return Math.random() * (max - min) + min;
}
f(10, 2) // 5.846786164614274
f(10, 2) // 2.408925447484215
f(10, 2) // 3.9486113543862214
In this example, the same inputs lead to vastly different output.

Let’s go back to the algebra for a second. We just saw how our function f takes a value x and returns the square of x. Now, let's say we have another function called g:

g(x) = f(x) + x
This function g adds x to the f(x), and remember, f(x) is a function that just calculates the square of x.

Now let’s test it out:

g(4) = f(4) + 4 = 20
Sweet! Now, since we know f(4) will always be 16, we can just say that g(4) = 16 + 4 = 20. No matter what happens, this will always be the case.

In other words, referential transparency gives us the ability to freely replace an expression with its value and not change the behavior of the program. f(4) can be replaced with 16, g(4) can be replaced with 20, and the result is not changed. 

Here’s a more general way to think about referential transparency:
Pure functions + immutable data = referential transparency

Translation: a function that doesn't rely on external states or mutable data will always return the same output for a given input.

Why should anyone care if a function is referentially transparent? Isn’t this all a bit nit-picky?

It may be nit-picky, but trust me that it proves useful. There are a lot of benefits to writing functions that are referentially transparent.

For one, it makes it much easier to refactor and rewrite programs. Since a pure, referentially transparent function can be freely replaced by it’s value, the only thing we have to worry about when we refactor it is that we get the same value for a given input.

Second, since referential transparency implies that a function is pure, we can assume that a given function doesn’t have any side effects or external dependencies. This lets us focus on refactoring the single function without having to worry about all the baggage associated with the function in the outside world. 

The benefits of referential transparency go on. It’s particularly helpful for optimizing code using memoization, common subexpression elimination, lazy evaluation, or parallelization.

Partial application is a way to turn a function that expects multiple parameters into one that will keep returning a new function until it receives all its arguments. In other words, if a function accepts multiple parameters, we can “partially apply” some of the arguments now, filling in the rest later. We do this by creating intermediate functions that have just the arguments we provided applied to them (while waiting for the rest of the arguments to be supplied). 

Sound crazy? Don’t worry, I’ve got some examples lined up to help make it more understandable. 

First, we’ll look at a function that cannot be partially applied. (Which is to say, basically all functions in JavaScript.) Below we have a simple function that apples tax to a given amount:

const applyTax = (tax, amount) => {
  return amount + (amount * tax);
};
Now, let’s say our tax rate was 8%. To use this function, we’d have to pass in both the 8% and the $ amount every time we use it:

applyTax(0.08, 100); // 108
applyTax(0.08, 200); // 216
applyTax(0.08, 190); // 205.2
applyTax(0.08, 10000); // 10800
…And if we forget to pass one of the arguments, we get back the opposite of a useful number:

applyTax(0.08); // NaN
A big fat NaN. Why? Because in JavaScript, any parameters that aren't supplied will have an undefined value. In this case, we didn't pass in the second argument, amount, and so when the function tries to calculate 0.08 + (0.08 * undefined), the result is NaN. Not helpful! 

Partial application can help us fix this mess. (Ramda.js to the rescue again!) I'm going to use the partial function from Ramda.js, which combines a function f and a list of arguments to return a new function g. 
const f = (a, b, c) => a * b * c;

const g = R.partial(f, [2, 3]);
We’re left with the function g, which is just the function f with some of its arguments already applied to it. So what do we do with g? Well, we can take g and provide the rest of the arguments to get a final result: 


const h = g(4); // 24
Ideally, we'd go through the underlying implementation for partial now so you can get a firm grasp of how partial works… But since this is an introductory email course, I want to focus on learning the concept at a high-level for now. (Don’t worry, we’ll be diving deeper on partial in the full course. Underlying implementation and other details will be waiting for you!)

Let's take a peek at a more realistic example to understand how this partial function looks in action:

const R = require('ramda');
const applyTaxOfEightPercent = R.partial(applyTax, [0.08]);
Here, we took our original applyTax function and partially applied the 8% tax rate. Remember that partial returns a new function, which we named applyTaxOfEightPercent. applyTaxOfEightPercent is a function that already has the first argument applied to it — that is, the tax rate.

Our original function took two arguments, and we applied one of them. So we have one more argument to apply (the amount) before we can get the final result:

applyTaxOfEightPercent(100); // 108
applyTaxOfEightPercent(200); // 216
applyTaxOfEightPercent(190); // 205.2
applyTaxOfEightPercent(10000); // 10800
Guess what, folks? You just learned partial application!! 👏 Not too painful, right?

Why partial application?

What’s the point of partial application?

In short, partial application allows us to partially apply certain argument to create new functions out of existing ones. The ability to take a generic function and specialize it by passing in certain arguments is incredibly useful.

Returning to our example, we can now use partial application to create three types of tax functions out of the original applyTax functions:

const R = require('ramda');
const applyTaxOfFivePercent = R.partial(applyTax, [0.05]);
const applyTaxOfEightPercent = R.partial(applyTax, [0.08]);
const applyTaxOfTenPercent = R.partial(applyTax, [0.10]);
Notice how I didn’t need to build a class… and then a constructor taking a tax percentage… and then create instances of the class for handling different types of taxes.

Instead, all I did was create a generic applyTax function and then partially apply it to different tax rates. Magic! 

Another good use case for partial application is to create simpler functions for commonly-used functions like event binding. Let's use addEventListener as an example. addEventListener takes in 2 required parameters: type, which is the string representing the event type to listen for, and listener, the object or function that receives the notification.

So what we’ll do is partially apply the “click” event type to create ourselves a listener specifically for “click” events:

const handleClick = R.partial(document.body.addEventListener, ["click"]);
Now that we’ve got ourselves a new function, handleClick, we have one less argument to pass to the function document.body.addEventListener. Instead, we can simply pass the listener function:

handleClick(() => console.log("You clicked me!"));
Versus doing:

document.body.addEventListener('click', () => console.log("You clicked me!"));
Isn’t partial application beautiful? I’ll go over more of its tricks and benefits in the full course.

…For now, you might be wondering: what about currying? After all, wasn’t currying in the title of this lesson?

Currying is the process of taking a function that accepts N arguments and turning it into a chained series of N functions that each take one argument. 

It sounds a lot like partial application, doesn’t it? It takes a function and an argument, and returns a new function with the argument applied to it. So what’s the difference? The difference is that with currying, you can never provide more than one argument — it has to be either one or zero.

const originalF = (a, b, c) => a + b + c;
const f = R.curry(originalF);
const g = f(1);
const h = g(2);
const i = h(3);
console.log(i); // 6
Remember that with partial application, we can apply more than one argument at a time. If a function takes 5 arguments, we can partially apply 3 of them. But with currying, we only pass one argument at a time. So if a function takes 5 arguments, we have to curry 5 times (😂) before we get the resulting value.

Let’s look at an example where we compare partial application to currying side-by-side. 

Below, I have a function that calculates the sum of 5 numbers:

const calculateSum = (a, b, c, d, e) => {
  return a + b + c + d + e;
};
Now, if we wanted to partially apply the first three arguments, and then pass in the last two later, we can do:

const calculateSumPartially = R.partial(calculateSum, [0, 1, 2]);
calculateSumPartially(3, 4); // 10
With currying, on the other hand, we’d incrementally pass in each argument one by one. Every time we pass in an argument, we get a new function, which we can pass the next argument too until we reach the last argument:

const calculateSumCurrying = R.curry(calculateSum); // creates my curried function
const applyFirstArg = calculateSumCurrying(0);
const applySecondArg = applyFirstArg(1); 
const applyThirdArg = applySecondArg(2);
const applyFourthArg = applyThirdArg(3);
const applyFifthArg = applyFourthArg(4); // 10
Or, done another way:

calculateSumCurrying(4)(3)(2)(1)(0); // 10
Does that make sense? Each time we pass in an argument, we get a new function with that argument applied to it. Keep doing this until you’ve passed in all 5 of the parameters, and you’ll reach the last function in the chain to get back the result value. 

We’ll be diving deeper into how this works in the full course, so don’t fret. More examples will help cement the concepts! 

As a side note, one thing I didn’t mention is that the curry function in Ramda.js is actually a teeeeny bit unusual—its arguments don't actually need to be provided one at a time. The library implements it this way just for our convenience, so don't worry. What you just learned about currying is still accurate.

We’ve already covered most of the overarching ideas behind functional programming, like purity, immutability and composition. There’s one more key concept I’d like to leave you with: the fact that functional programs are “declarative”. 

Do you remember learning about “declarative sentences” back in grammar school? Basically, a declarative sentence makes a statement or “declares” something. It states a fact. For example, “I love running!” or “He chews loudly.” 

…It’s no different in programming. A declarative program declares “what” the program does without necessarily telling us “how” it does it.

Instead of saying “I love picking up my foot and then landing on the ball of my foot and then using the momentum to lift off the foot I landed on and pick up the other foot and then landing on the ball of that other foot and repeating this motion really fast,” it simply says: “I love running”

The longer sentence above is a good example of “imperative” programming, which describes exactly how to achieve a result by using statements that specify control flow (e.g. for-loops, if-else statements, etc.) or state changes.

Long story short: 

Declarative = WHAT
Imperative = HOW 

Okay, enough talk, more examples. Let’s start with an example of an imperative function that takes an array and then multiplies all the items in the array by 3:

const multiplyByThree = (array) => {
  var result = [];
  
  for (var i = 0; i < array.length; i++) {
    result[i] = result[i] * 3;
  }

  return result;
};
Simple enough. First we tell the program to start with an empty result array. Then we tell it to start a loop that begins at index 0 and goes until the end of the original input array. In each iteration of the loop, we tell it to take the current item in the original array, multiply it by three, and then push it into the result array. Repeat this until we get to the end of the array, and finally return the result array.

This is an imperative program because we told it exactly how to perform the desired outcome. 

On the flip side, compare that to this example:

const multiplyByThree = (array) => array.map(item => item * 3);
This function does the same thing, in one-liner form. We take advantage of the built-in higher-order function map that exists on arrays to simply tell the program what we want: item * 3.

We already know that the higher-order map function takes an array and returns a new array which consists of the items in the original array mapped to whatever our mapping function does. So in our case, our mapping function multiplies every item by three, leaving us with a result array that has all the items multiplied by three.

The point here is that we don’t need to tell the program how to do that — the higher-order function map does this for us. All we're required to do is tell map what we want each item to be mapped to, and the rest is handled for us.

You’re probably wondering at this point: why does functional programming favor declarative code over imperative code?

Well, for starters, functional programming strives for expressive and easy to understand code. The declarative example above wins on both counts, being both expressive, short, and easy to understand at a glance. 

Secondly, functional programming strives to use small, independent, reusable, and composable functions as the primary unit of abstraction. Loops (such as those in the imperative example above) aren’t reusable artifacts.

If it’s not reusable, then we can’t really compose it with other functions either. The only way to make it reusable is to create an abstraction for the loop with functions — and this is exactly what map does for us in the imperative example. It abstracts the fact that we're looping over an array and executing some mapping function on it. We can reuse this map function anytime we need to transform an array from one thing to another. 

Lastly, declarative code typically leads to less code—and that means fewer places for bugs to hide. 

For me, writing declarative code vs. imperative code feels like the difference between riding an automatic vs. a manual transmission car. They both get us to the final destination. One just takes care of switching different gears for you, while the other requires you to stay focused and tell it how and when to go from one gear to another. 

There's obviously much more ground to cover with declarative vs. imperative code. For now, let’s save the details until the full course (don’t forget to sign up!).

Overall, because functional programming makes heavy use of higher-order functions and function composition, code tends to naturally end up more declarative. Once you get going, I promise it feels natural. 😊

Alright folks, I can’t believe how far we’ve come together! It’s been a fun (and quick!) journey through the land of functional programming.

This course by no means covers all the fundamentals, but we’ve made important progress in the journey towards functional ninja-hood. We’ll be building on these concepts in the full course, and introducing some more crucial principles that will help you write cleaner, stronger, more functional code.

To see:
- SICP
- The little schemer
- https://stackoverflow.com/questions/210835/what-is-referential-transparency/9859966#9859966
- https://github.com/MostlyAdequate/mostly-adequate-guide
- http://haskell.cs.yale.edu/wp-content/uploads/2015/03/HSoM.pdf
- https://github.com/stuartsierra/reducible-stream
- https://purelyfunctional.tv/
- Learn Clojure
- Learn Scala
- http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html
- https://www.youtube.com/watch?v=Dsd4pc99FSY&list=PLFrwDVdSrYE6dy14XCmUtRAJuhCxuzJp0
- https://mitpress.mit.edu/sicp/full-text/book/book.html
- http://raganwald.com/2017/04/30/transducers.html
- https://www.youtube.com/watch?v=qJgff2spvzM
- https://www.youtube.com/watch?v=Tn05cXrhBvg
- https://www.youtube.com/watch?v=br6035SKu-0
- https://www.youtube.com/watch?v=ROL58LJGNfA
- https://en.wikipedia.org/wiki/Memoization
- https://en.wikipedia.org/wiki/Common_subexpression_elimination
- https://en.wikipedia.org/wiki/Lazy_evaluation
- https://github.com/swannodette/logic-tutorial
- https://medium.freecodecamp.org/learning-the-fundamentals-of-functional-programming-425c9fd901c6
- https://davidwalsh.name/functional-programming
- https://medium.com/javascript-scene/iteration-a-gentle-introduction-to-functional-programming-c59fcb0ab58d

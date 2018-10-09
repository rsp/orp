# Object Reoriented Programming
Rafał Pocztarski<br>
@pocztarski<br>
pocztarski.com

Going back to the fundamentals of OOP
in JavaScript and TypeScript

---

The roots of object-oriented programming,
how we deviated from them over the years
and what can we do to rediscover the fundamental idea of objects
and make our code more maintainable.

---

# My first contact with OOP was with C++ when I was about about 12. I didn't like it. Came back to C.


I actually used a C++ compiler
to use the // comments instead of /* ... */
(It was before C99 that introduced // comments to C)
but I didn't get what those fuzz about objects was all about
as I could write everything I've seen in examples in C.

---

For me methods were just C functions
with an additional implicit parameter
and some dispatch magic that was not useful in what I did
and eveything else was just
ordinary procedural code.

Around 96 I started writing JavaScript
and discovered that its OOP model is much simpler
to have an object:
- you make an object
- vs. you make a class and instantiate it 

Shortly after I started writing Perl and found that 

Then some time later I found 

"Actually I made up the term Object-Oriented,
and I can tell you I did not have C++ in mind."
- Alan Kay

What did Alan Kay have in mind?
And why didn't we get it?

What the OOP is all about?

Classes?

Inheritance?

Method calls?

Message passing.

The message passing in languages like C++, Java, Perl, Python,
JavaScript, TypeScript
is usually implemented as method calls,

x.doSomething();

Conceptually it passes a message "do something" to the object x.
In reality it calls a special subroutine
that the object "x" knows how to dispatch
That subroutine in addition to its normal parameters gets
one extra parameter that is bound to the specific instance of object "x"

In Perl it is just passed as the first argument
that is often copied to a variable called $self by convention.
In Python it's bound to `self`.
In Java or JavaScript it's bound to `this`.
In Java or JavaScript it is bound to a special variable called this.

In C++ `this` inside of a method holds a pointer to the object.
Otherwise it is just an ordinary procedure.
It gets arguments and it returns a value or raises an exception.

My question is:
If you were asked to design a message passing
protocol in JavaScript
- would you do it synchronously?

Why it's a problem:

If we have a method that returns a value synchronously
in a single-threaded environment
then we can never refactor it to use a database or a file system
without breaking the API.

So the only way to deal with that is for every public method of every
object to be asynchronous even if it doesn't have to.

We cannot go the pother way.

It's easy to have a function that returns a promise:

function square(x) {
  return Promise.resolve(x * x);
}

or even better with new syntax:

async function square(x) {
  return x * x;
}

It's impossible for a function in JavaScript or TypeScript
to return a value 

I had 4 takes on that:

1. First was some kind of an object that gets messages and emits events.

I actually had some idea of 

2. Second was an object whose all methods take callbacks instead of returning values.

3. Third was that every method should return a promise instead of a value.

4. Fourth was using generator based coroutines to simplify promise handling
Every method had to be defined as a generator function wrapped in a special wrapper.

5. Then finally async/await came out

Now it can be expressed very easily:

Make all methods of the public interface async.
That's it.

I created a simple library (rsp on npm) to handle
calling methods on promises of objects easy.
I planned to add getting and setting properties
but every time I tried it became complicated and I didn't like it.

Recently I've read Elegant Objects by Yegor Bugayenko
and one of the rules is that no object should have any public
properties in the first place.

Now I am convinced that this is the way to do OOP
if we want to take full advantage of it
instead of just writing plain old procedural code
made of methods instead of functions.

In summary:
I started with procedural programming
Found out OOP which wasn't that different from procedural programming
Found out FP which was totally different and made a lot of sense
Rediscovered OOP 

"In the original object-oriented systems that were so successful,
messages aren't commands at all. What they are are desires."
- Alan Kay (a 1980s OOP lecture)

Object is not a data structure.
Assignment cannot be done from the outside.

We use object as data structures.
Even when we make properties private, we add getters and setters
which ruin the abstraction.
ORMs are a perfect examples of that.



I was always inspired by the books and lectures by
Gerry Sussman, Hal Abelson, Alan Kay, David West

Now I see a practical examples of that way of thinking
in the books and lectures by Yegor Bugayenko




I am currently trying to combine all that with by take
on asynchronous message passing in single-threaded environments
like JavaScript and TypeScript.

The trick is to make it 

Introducing the Stamp Specification
by Eric Elliott

composable factory functions

I am in the process of putting together an exact specification
Not everything is set in stone yet, follow me on Twitter to be updated.

I am creating a test assertion framework for JavaScript and TypeScript
that is going to be 





Talks and lectures:

SICP - Computational Objects
by Gerald Jay Sussman (1986)
https://www.youtube.com/watch?v=SsBxcpkyMMw

Object Oriented Programming
by Alan Kay (mid 1980s)
https://www.youtube.com/watch?v=QjJaFG63Hlo

Object Oriented Programming
by Daniel Ingalls (1989)
https://www.youtube.com/watch?v=Ao9W93OxQ7U

OOP is Dead! Long Live OODD!
talk by David West (2013)
https://www.youtube.com/watch?v=RdE-d_EhzmA

Design Thinking
by David West (2013)
https://www.youtube.com/watch?v=XPpWvoE-hk0

Interview with David West (part 1)
by Yegor Bugayenko (2016)
https://www.youtube.com/watch?v=s-hdZZzMCac

Interview with David West (part 2)
by Yegor Bugayenko (2016)
https://www.youtube.com/watch?v=bW5K5cJ-AVs

What's Wrong with Object-Oriented Programming?
by Yegor Bugayenko (2017)
https://www.youtube.com/watch?v=GMrjuuczZkQ

The Past and Future of Domain-Driven Design
by David West (2017)
https://www.youtube.com/watch?v=XH_awPS6hK4

Books:

Structure and Interpretation of Computer Programs
by Harold Abelson and Gerald Jay Sussman (1985, 2nd ed. 1996)
https://en.wikipedia.org/wiki/Special:BookSources/9780262510875

Object Thinking
by David West (2004)
https://en.wikipedia.org/wiki/Special:BookSources/0735619654

Programming JavaScript Applications
by Eric Elliott (2014)
https://en.wikipedia.org/wiki/Special:BookSources/1491950293

Elegant Objects (Volume 1)
by Yegor Bugayenko (2016)
https://en.wikipedia.org/wiki/Special:BookSources/9781519166913

Elegant Objects (Volume 2)
by Yegor Bugayenko (2017)
https://en.wikipedia.org/wiki/Special:BookSources/9781534908307




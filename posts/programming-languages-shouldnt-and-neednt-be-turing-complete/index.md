<!--
.. title: Programming languages shouldn't and needn't be Turing complete
.. slug: programming-languages-shouldnt-and-neednt-be-turing-complete
.. date: 2020-12-09 18:25:19 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

As we software engineers grow up, we are taught early on (like in kindergarten) to associate Turing (equivalent) machines with computation _per se_: It's the paradigm that the vast majority of programming languages aspire to and that many more which don't aspire to fall into [accidentally](https://beza1e1.tuxen.de/articles/accidentally_turing_complete.html). If you grew up like me, you probably came to believe that Turing completeness was necessary to build any serious programs and that Turing incomplete languages were either toys, parsing tools or config files. Well -- you maybe heard that _SQL_ was Turing incomplete but not thought much of it.

Well, I have come to tell you that these matters aren't quite the way they seem: Turing incomplete languages can in fact be powerful enough to support pretty much any programming task you or I or any web developer, or data scientist, or devops engineer would be faced with today. I will also tell you that Turing incompleteness is very promising to drive a true leap forward in the art of software engineering, on par with the likes of garbage collection or structured programming.

The goal is to leverage Turing incompleteness for:

* safe collaborative sandboxing
* predictable "serverless" cloud functions
* distriuted computing with provably less bugs 
* cryptocurrency "smart contracts" less full of money-losing surprises
* tractable automatic code generation from specification
* safer interaction of untrusted components

While the path to getting there is not completely clear, Turing incompleteness is both promising and easy enough to warrant much more intense investigation and experimentation than we currently have. In service of more widespread adoption we shall go through some very simple _dos and don'ts_ for Turing incomplete languages which hopefully will inspire you to build your own!

_This post is an adaption of a [paper](https://www.gabrielpickard.com/turing-incomplete_edited.pdf) and talk I gave at [HATRA 2020](https://2020.splashcon.org/home/hatra-2020?plenary=Hide%20plenary%20sessions), a workshop during the [SPLASH 2020](https://2020.splashcon.org/) conference._


## Ceding power to gain control

Computers do exactly what we tell them to do. Unfortunately human thinking is much less pedantic and we write programs which don't do what we think they should. These discrepancies are called _bugs_ and I'm here to get rid of them. We may also encounter the opposite problem: We are faced with a complex code base that does _something_ and we are tasked with changing it, without understanding what it _really does_. Either way, nobody sets out to write segfaulting code -- and yet we inevitably do _so long as the language allows it_... Which is why garbage collectors are so popular these days.

Hence the history of programming language design has been a history of removing powers which were considered harmful and replacing them with tamer, more manageable and automated constructs. Here are a few examples:

* Direct entry of binary code became assembly language.
* Direct access to CPU registers and instructions gave way to higher level compilers in the ALGOL tradition.
* The infamous _GOTO_ was banished in favor of structured programming.
* Manual memory management is still around in certain areas, but garbage collection made memory safety so popular that now we have borrow checkers to write memory safe code even if we can't afford the garbage collector overhead.
* OOP involved moving from arbitrary access to information hiding modularization.
* Functional programming afficionados removed side-effects and mutability in favor of pure functions and persistent data structures. Nowadays programming in _React_ is much better with immutability.

The list goes on and on... While not all application domains benefit from all the replacement steps above, it appears as if removing some expressive power can often enable a new kind of programming, even a new kind of application altogether. Unix was possible because of the _C_ compiler. Photoshop could hardly have been built on the basis of _GOTO_. The _JavaScript_ ecosystem would not have grown without garbage collection.
	
While we can't know exactly what the benefits will be, Turing incompleteness is a great candidate to achieve an _expansion in applicability_ by reducing expressive powers. Furthermore, there is cause for high hopes: compared to most of the changes listed above, Turing incompleteness is more sweeping and more fundamental.

## A great leap forward

[Rice's theorem](https://en.wikipedia.org/wiki/Rice%27s_theorem) states that we can't build automatic checkers that work on _all programs_ of a Turing complete language to extract any non-trivial property. These kinds of non-trivial properties are exactly what we would be looking for if we want to equip languages with smarter developer tools and more in-depth feedback about correctness, runtime complexity, optimization and security.

These kinds of benefits have not gone _completely unnoticed_. There are some success stories out there, applying Turing incomplete languages. The main one that most people have dealt with is _SQL_. I posit that _SQL_ would not have been as successful and widespread as it is, if database servers weren't as performant as they are -- and they wouldn't have been as performant if the input language had been less manageable, i.e. Turing complete.

In many ways we don't yet know exactly what the killer app for Turing incompleteness will be, but I do have some ideas for what I would like: Making the kind of stuff people do with fancy type systems more user-friendly. I want verification to become much more transparent and automatic. As anyone who has dealt with automation and transparent abstraction knows: It's easy to come away with a bad taste and it's all about the edge cases -- the parts that make the abstraction leaky. Turing incompleteness could be a very big step to cutting out the ege cases, making our abstractions more robust and making it easier and more widespread to build verification tools.

Nowadays mission critical applications like Microsoft Windows are automatically checked for bugs at great expense using SMT solvers. This process is laborious, incomplete and full of pitfalls, which is why hardly anyone does it who doesn't have to. I think we can find a way out of this by fundamentally rethinking our computing paradigm.

## What Turing incomplete languages can and can't do

I performed a small literature search and found two (2!) problems known to theoretical computer science which we cannot implement in a known Turing incomplete language. They are the following:

* Simulating a Turing machine (and equivalents)
* Building a self-interpreter for a language in itself, where the input code is a Gödel number (and there even is a [big caveat](http://compilers.cs.ucla.edu/popl16/popl16-full.pdf) to this)

If you can think of any others, let me know, but suffice to say the list isn't long. Notably, the Ackermann function, SAT, A* etc., searching and sorting can all be solved using a strongly normalizing (i.e. terminating) lambda calculus like [Gödel's System T](https://en.wikipedia.org/wiki/G%C3%B6del_system_T).

While almost any known problem is clearly solvable in a known Turing incomplete language, the matter of _efficient algorithms_ is  a different matter. Though it's clear that for _any specific given_ problem we can come up with a set of Turing incomplete formalisms to model it efficiently, we cannot assume that there is _one_ Turing incomplete language capable of representing _all_ known algorithms as efficiently as _C/C++_ would on a _von Neuman_ style computer. There are some caveats. Luckily though, these issues are akin to how it's hard to represent an efficient mutate-in-place algorithm like as _quicksort_ in a pure/immutable functional language like _Haskell_ or _Clojure_ -- and people still find a lot of use for those languages.

Algorithms of the type _"do X until condition Y holds"_, often found in numerical computing, which do not iterate over a collection, are hard to model in a Turing incomplete language. Doing so in the current state of the art requires complex type systems and proofs of termination which from my perspective take us farther from the goal of user friendly assisted programming..

Luckily, _the reality of modern application development_ is often _extremely_, _extremely_ light on "capital A algorithms". I.e. for very broad swaths of the software engineering workforce it is entirely irrelevant whether they can efficiently implement in-place sorting or the Newton-Raphson method. In fact, rolling your own fundamental algorithms is generally considered an anti-pattern and bad industry practice. That is what, by and large, we have libraries for. It's not by accident that many fundamental numerical libraries are comprised of decades-old Fortran code. Why mess with something that works? Furthermore, the widespread adoption of virtual machines as compilation targets has made it much easier to bootstrap new (e.g. Turing incomplete) languages, while hitting the ground running with access to a full suite of practical libraries to draw on.

Turing incomplete languages can trivially handle anything having to do with conditionals, iterating over collections, trees or performing a transformation repeatedly for a pre-determined number of steps. As such, I believe that a very simple set of constructs can handle anything a common full-stack web developer needs to do for most of their carreer. In the rare edge case one can always expand the range of language primitives or implement escape hatches.

## How to stay total

It's not too hard to take an imperative or functional language and turn it Turing incomplete. Mainly one just needs to remove unconstrained loops and recursion and replace it with more constrained constructs such as list comprehension, _foreach_ loops, or the _map_, _reduce_ and _filter_ suite of collection processing functions.

Here's a set of choices that will work for a Turing incomplete imperative programming language:

* Mutable data structures
* No mutable references to first class functions
* No unconstrained _for_ or _while_ loops
* A modified version of _foreach_ loops, with a cycle checker and a way to iterate through nested data structures / trees

If instead you want to make a Turing incomplete functional language you could choose the following:

* Immutable names and variables, with acyclic data structures
* First class functions
* No recursion
* _map_, _reduce_ and _filter_ (with some variants for handling nested data structures and trees)

In both cases one would want a system of event listeners to handle user input without needing infinite loops. Any conditionals will work for either scheme, as well as list comprehensions and lazy data structures. Handling more complex loops than iterating over a list requires some beefed up variant of _reduce_: One could have a _reduce_ operator that gets called for every _nested_ element of a collection, i.e. not just the immediate members of a list, but also their members, if they themselves are collections. For trees it might be handy to support a reduce function with two components: one transformation for descending and one for ascending in the tree.

Guido van Rossum is famously not a fan of _reduce_:

> [reduce] is actually the one I've always hated most, because, apart from a few examples involving _+_ or _*_, almost every time I see a _reduce()_ call with a non-trivial function argument, I need to grab pen and paper to diagram what's actually being fed into that function before I understand what the _reduce()_ is supposed to do

He has a point, but consider the following code:

```Python
reduce(lambda x,y: foo(x,y), coll, val)
```

This is equivalent to / syntactic sugar for:

```Python
x = val
for y in coll:
    x = foo(x, y)
```

As such it of course makes sense to _not_ use the explicit _reduce_ function througout most Python code and instead use the pretty syntax. Any Turing incomplete language aiming for user friendliness would aim for similarly readable constructs, either via macros or built-ins. Here's an example _pythonic_ nested reduce:

```Python
def flatten(nested_list):
	for item nested in nested_list with result = []:
		result.append(item)

	return result
```

## Leveraging Turing incompleteness

Above I have outlined some _very simple_ constructs without fancy type/termination checking, which already can handle the vast majority of retail programmer use cases. This is good news, because once we start down the happy road of tractable language semantics and gain more experience, it stands to reason that even more intricate, efficiency sensitive "capital A algorithms" will be supported.

I have shown that it's not too hard to build a Turing incomplete language. What I haven't yet outlined is how to leverage Turing incompleteness. Partially, this is due to the fact that we don't yet know exactly. This would be a great realm for many different approaches to compete.

We can surmise that Turing incompleteness will help us write more correct software, but doing so will likely necessitate better ways of building specifications against which correctness should be checked. In my very own opinion, expanding on type systems in the _ML_ and _Haskell_ tradition will not be the way to go, or at least not the _only_ way to go.

I'm interested in metalogics that talk about program behavior, which do not follow the _intuitionistic_ type theoretical approach. I.e. I'm interested in specifications with negations. The logic programming literature is full ideas about stratification and the like, in order to make negation a tractable part of a solver, checker or inference system.

Any metalogic or type system can suffer from the aesthetic problem that it increases the surface area of the language and adds more and different syntax to the operational core. In light of this, I have been interested in expressing _program metalogic_ as _code patterns_ and _underdetermined traces_. But this is a topic of active inquiry, with more to come...

## Back to Gödel: historical remarks

The above concludes the core of my argument. If you are now wondering "Why, if Turing incompleteness is so promising and accessible, haven't I heard more about it?" let me give you my selective reading of the history of computer science as an attempt at explanation:

Well before computers became a thing, the logicians who invented computer science were more concerned about well-foundedness in mathematics than writing bug-free software. Initially the most widespread definition of "effective procedure" was actually a terminating language: Gödel's seminal incompleteness theorem used a _strictly terminating_ definition of _effective procedure_: That which we now call _primitive recursive functions_.
	
This definition was far from settled though: A convincing _negative_ answer to the _Entscheidungsproblem_ (whether there is an _effective procedure_ to prove or disprove any mathematical statement) required a satisfying definition of "effective procedure" beyond all doubt, one for which the scientific community could agree that there was no "larger" sensible definition of "algorithm" in which the _Entscheidungsproblem_ could happen to be true _after all_. Following considerable scientific debate, the _general recursive functions_ as well as Turing machines and the lambda-calculus were accepted as equivalent, encompassing conceptions of _effective procedures_.

The choice of Turing machines as definition was not based on _user-friendliness_ or manageability, rather it was chosen to be _maximal_, so as to eliminate all doubt with regards to an uncomfortable negative result. Particularly, making no claims about whether the _difference_ between Turing machines and the terminating languages (such as the primitive recursive functions or _Gödel's System T_) contained any valuable or sensible algorithms.

Turing machines perhaps might have been relegated to a position of less prominence, relative to other (including total) formalisms in the lambda-calculus family, if early computers had not come about so swiftly and the _von Neuman architecture_ hadn't so closely resembled a Turing machine. The comparison is apt: Computer memory functions as (unfortunately finite) read-write tape, while registers roughly correspond to machine state and the CPU to the transition function.

Programming in binary and assembly obviously mirrored the von Neuman architecture in Turing completeness. Languages with abstract control structures soon followed. These _programming languages_ roughly fell into two camps: those with loops (_Fortran, COBOL, BASIC, C_) and those using recursion for code repetition (_Lisp, ML_). Unfortunately, both approaches, in their chosen form, also entailed Turing completeness. 

Why did the earliest programming languages all default to being Turing complete?

* Turing completeness (accidental or not) is so easy to achieve that without focus on the matter it becomes inevitable in programming language design.
* The Turing machine had a head start as predominant paradigm for computation. Lambda calculi were hard to implement (for lack of complex data structures) and underdeveloped: The _simply typed lambda calculus_ was _too_ simple for real computation and _Gödel's System T_ was not published before 1958 -- the same year that _Lisp_ was invented.
* For lack of meta-reasoning capabilities, complex type systems, abstract data structures and processing power, the early programming languages were unable to take advantage of the benefits of Turing incompleteness.
* Infinite loops are an attractive concept for managing system-level tasks.
	
By the time calculi like _System F_ were developed, the paradigm of arbitrary recursion had become so entrenched that almost by default Haskell became Turing complete, even though its type system is ostensibly based on _F_. Turing completeness has become synonymous with computing, whereas virtually no software in use requires the full arsenal of Turing completeness.

We largely owe this state of affairs to the popularity of arbitrary loops and unrestrained recursion. Nevertheless there is hope of escape: Turing incomplete constructs such as _list comprehension_, _foreach_-style iteration (together with lazy data structures and generators) and functions in the family of _map_, _reduce_ and _filter_ are gaining popularity and actually considered the more idiomatic means of writing repetitions in many popular programming languages such as _Python_ and _JavaScript_.

We find ourselves in a situation where those who know about Turing incomplete languages are mostly academiccs who think that "computing" is about "capital A algorithms" (which are harder to represent efficiently). The hordes of software engineers in industry who know that most programs are really rather simple, think that Turing completeness is computing _per se_. I see an oportunity here. 

## So, what are you waiting for? Let's start terminating!

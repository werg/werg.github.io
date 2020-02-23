<!--
.. title: Developer Experience: Fundamentally harder than UX
.. slug: developer-experience-fundamentally-harder-than-ux
.. date: 2020-02-22 23:34:01 UTC-06:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

Many (maybe most) of us Software Engineers are deeply involved in projects where UI and UX are very important concerns (or at least they should be). Throughout the short history of our profession, we have become more and more focused on understanding and serving the people who will actually be subjected to the stuff we build:  **users**. In many cases, this focus on UI/UX isn&#39;t because we particularly enjoy worrying about such matters -- no, it&#39;s simply because we have to if we want to build successful products!

There has been tremendous growth in the field of UX/UI. Without a doubt, today&#39;s applications are much more user-friendly than those from 30 years ago. Back then, users were given  **features**, interface be damned. It was only over time that customers came to appreciate, expect, demand and reward those applications that actually cared to consider their needs.
_Consumer demand drove UX as a discipline_.

This process has been fast in some areas, slow in others. Nowhere has it been slower than in the realm of programming tools. We coders still put up with horrid UX/UI when programming.

# Why DX lags behind

Iin my view the User Interface of programming encompasses a lot, from the type system of the programming language that you use, its error messages, to the editor you&#39;re writing code in, the websites you go to in order to get help, all the way to the cloud hosting systems you deploy on. Developer Interface / Developer Experience is comprised of all of this.

- Counter to any UI/UX philosophy, as programmers we find ourselves maintaining vast background knowledge about the structure and dynamics of our programs, with nary a visual cue to help us.
- It&#39;s often so hard to figure out what _exactly_ went wrong when something goes wrong.
- A lot of tools are truly ugly!

When was the last time you heard of a programming language discussed in terms of discoverability, succinctness, relevance, let alone beauty?

I believe there are two reasons for the discrepancy between general UX and DX:

![ENIAC Computers](/images/eniac1.jpg "The good old days")

1. . **Coding tools were around before UI/UX was a thing**.
We&#39;ve simply gotten used to them: Dealing with the idiosyncracies of bash, vi, or the JavaScript type system have become a part of the professional hazing process.
They may be suboptimal, _but they're ours!_
This is compounded by the fact that the history of technology is so path dependent. In so many cases it is much easier and more profitable to build on something existing rather than reinvent the wheel. -- Even if the existing wheel is full of arbitrary decisions and in fact impediments to what you are trying to do. Just look at the long reign of the x86 architecture, or consider the fact that basically all Operating Systems these days follow the Unix architecture. The fact that JavaScript is what it is. -- I don&#39;t mean to say that these technologies are without merit, however they also have considerable flaws and it has been more efficient to work with and around than to replace them entirely.
Certainly every mature technology will have to deal with technical debt in the inner workings of its guts. I have no bones with that. However, if the gory details are in the guts, then we coders are the GI surgeons having to deal with them. -- And we need sharper scalpels, better imaging and protective gear. In short: better tools.

![Chomsky Hierarchy](/images/chomsky_hierarchy.png "Theoretical CS was fun")

2. **Fundamentally, programming is a Turing Complete business.**
Compare most GUIs -- in terms of language complexity, the different states that the application interface can find itself in, would in the majority of cases correspond to regular languages (some may be context-free, but that&#39;s pushing it). The visual languages are &quot;flat&quot;, predictable, without feedback loops or long distance dependencies. It is in such an environment that UI/UX principles have been able to thrive.
But what did our _Intro to Theoretical CS_ course teach us in college? You can&#39;t assume that statements about regular languages will still hold for Linearly Bounded Automata, let alone Turing Machines.
Fundamental principles in conventional UI/UX design no longer apply when it comes to programming. DI/DX is a very, very special case UI/UX.

So, what I believe has happened is that in many cases we programmers have tilted at windmills of trying to improve our tooling -- the eternal yak shave -- only to be thwarted by the complexity of our own work, inevitably giving up and going with the most rudimentary system capable of doing the job somehow, even if it sucks.

# Toward better DX

deal with them. -- And we need sharper scalpels, better imaging and protective gear. In short: better tools.

![Ironman interface](/images/futuristic_interface.jpeg "This could be us but you coding")


So, what&#39;s the alternative? Here are my suggestions for a world with better Developer Experience:

1. _Watch what coders actually do_ -- this is one principle from UX that applies readily. Library developers rarely know what error messages users most commonly get stuck on; How about user studies? We track every click that people make on our website and agonize over button sizes, but know precious little about how common which call paths in our framework are.
2. _Address the many components that make up programming in concert_: Editor, shell, repl, language, version control host, cloud host and framework. Generally these pieces are not very aware of each other.
3. _Search_ -- It&#39;s our dirty little secret how much programming nowadays depends on Google. I find this topic fascinating and I&#39;ll write much more on it -- coming up!
4. _Standardize fundamental questions_ -- How do I run this thing? Where does the code start? Is my system configured correctly?
5. _Intelligently hide details_ -- Coding is about control, however understanding is not. Most environments throw up their hands and overwhelm you with the entire pile of everything the program does, in minute detail. Others take a different tack and try to hide the bitter realities behind magic -- impenetrable and beautiful until you inevitably _do_ have to care about what's behind the curtain. Why do we have so few systems that would allow us to zoom in and out? _Get you a coding environment that can do both_.
6. _Programming Languages are User Interfaces_ -- The most fundamental unit of Developer Experience is the programming language. The Elm language is one of few examples where this reality was considered explicitly in the design process.
7. _Programming is about empowering_ -- dumbing things down is _not_ enough. I believe minimalism is a cheap approach to UX in general, but it definitely doesn&#39;t work for DX -- it fundamentally misses the point of what programming is about: expressive power. I believe this is why many &quot;graphical&quot;/beginner programming languages have failed.
8. _Engage with Theoretical Computer Science_ -- In a way we are hunting for UI widgets (or other kinds of artifacts) that can faithfully represent the full computational complexity of algorithms. This is the one area where [Bret Victor&#39;s](http://worrydream.com/) excellent work may have fallen short of what we ultimately need.


![UX Meme](/images/why-ux-research-is-important.png "Just ship it!")

# DX is worth it

Interest in this topic is growing. It&#39;s definitely worth looking into. The software industry is so big and expensive that even small improvements can have considerable impact. Furthermore, Software Engineers actually _do_  respond to better UX -- and they wield considerable purchasing power. Consider the following example:

I once worked at a small-to-midsize company which for regulatory reasons couldn&#39;t use the normal cloud-hosted GitHub. Our engineering department strong-armed the rest of the company to purchase on-premise GitHub Enterprise at a cost equivalent to hiring one or two additional engineers, _just so we could use Pull-Requests!_ We recognized the difference it made in our productivity and we demanded it -- only the best of tools would do.
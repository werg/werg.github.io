<!--
.. title: AI is Computation
.. slug: ai-is-computation
.. date: 2026-06-03 07:23:42 UTC-05:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
-->

The original framing for machine learning was *function approximation*. This framing was of course accurate, but it does fail to capture what has been going on at our current juncture, where ML has turned into something we a lot more justifiably can call: Artificial Intelligence.

I remember getting quizzical looks from colleagues interested in machine learning when I complained that you couldn't do general-purpose computation with a specific model. I think we were talking about word embeddings -- Word2Vec had just arrived, and the potential for operating on words in a continuous semantic space was immediately apparent. Without compositionality beyond simple concept arithmetic, though, a semantic space was merely interesting, useful perhaps for search, but nowhere near sufficient for computation in any meaningful sense.

A favorite interview question of mine back in the day -- which no interviewee ever answered satisfactorily, and which bedeviled me too -- was this: how do you cram a variable-size input into a fixed-size vector in a workable way, such that you can run it through a neural network without drowning in vanishing gradients? (The recurrent neural network was the non-solution of record) Transformers answered the question decisively by saying: you simply don't do that (by that I mean cram it all in a fixed-size vector). You maintain a representation that grows with the input, at the cost of quadratic computation on it.

With that, we were no longer beholden to the fact that while neural networks may be universal function approximators in theory, they were not, in their original form, designed to handle variable-size data with variable computational effort.

Or handle variable-size data at all.

LLMs can obviously compute. Computation, understood 'properly', is modeled by following the rules of a formal language -- LLMs are simply extending this notion to instead follow the informal rules of an informal language. This may not meet the strict definitional requirements that logicians worked out roughly a hundred years ago, but it likely captures the spirit of what they were trying to define much better than we typically give it credit for.

Like the physical computers we are familiar with, language models are limited by finite context and memory. They are and remain imperfect models. (The interesting question -- as an aside -- is whether the imperfection lies in the theory or the implementation.)

The things we do around context compaction, subagents and discoverable context point in the same direction as the original argument for why we could treat practically finite computers as models for theoretically infinite machines: as long as you have a non-exponential algorithm, you can always add more -- more memory, more processing power and machines -- once you hit the limits of the original setup for a specific workload.

This holds for LLMs in an agentic setting too, and it is quite telling that the means we have used so far -- agentic harnesses -- are very direct adaptations of classical computing primitives, with next to no additional machine learning fancy business. All we are using is the actor model, trees, a Unix file system and OS state, a shell and the ability to execute arbitrary code.

This underlines the fundamentally computational character of AI as it stands today. LLMs are, arguably, much better at performing computation -- albeit informally defined -- than at doing the other thing people historically associated with AI: acting like, impersonating, perhaps even *being*, a person. Memory, continual learning, caring about anything, having intentionality in any durable sense -- these may be simulatable over short local contexts, but at even medium scales they are more notable for their absence than their presence, and this in an era when programmers like me continue to be genuinely amazed at what these systems can accomplish on the tasks I, an actual person define, premeditate and set for them.

The AI we have today is much more *informal computation* than it is *artificial person* -- and our ability to now instantiate informal computation is surfacing this distinction, much like the chess computers of the GOFAI era showed us the subtle difference between formal reasoning and actual intelligence.

Which brings me to programming languages -- a topic deeply intertwined with computation and near and dear to my heart. Andrej Karpathy is known for pointing out that English is now the biggest programming language. In a lot of ways I agree, or at least: a computable, computation-focused subset of English. But let's unpack this: English is not a formal language. It has no strict syntax, no formally defined computational semantics. To capture anything equivalent to a programming language, we need to rework the terminology.

To that end I would like to introduce a new kind of programming language, which I will call *Verplankalkül* -- a portmanteau. Konrad Zuse, who built the first programmable computer, named his first programming language *Plankalkül*, literally "plan calculus." The German colloquial term *verplant* means disorganized, messy -- literally "mis-planned." Verplankalkül, then: a *messy plan calculus*. An informal programming language.

The most popular Verplankalkül right now is English-language instructions formatted in skill files with executable script sidecars, with input data "types" that range over user prompts in natural language. When defining a non-formal language for expressing and controlling computation, we also need to define the virtual machine it runs on -- much like the Turing machine stands to the lambda calculus, or the JVM to Java. A widely-used term for this already exists, one I don't particularly love: *the agent* (including the agentic harness).

If we were going to stay permanently at this stage, we wouldn't need new terminology at all. We could simply say: files and prompts, tools and code execution. My impetus for defining Verplankalkül as a concept is to anticipate -- and call for -- other kinds and variants of such informal programming languages.

I don't think we'll stay at this stage -- I see movement on two fronts.

First: the agentic harness and its attendant software, as currently defined, is in a fundamental way *not learned* -- it is fixed, non-gradient-optimized formal scaffolding. I believe this will change. Harnesses will wither away, absorbed into learned behavior.

Second: imperative English is a poor proxy for many large-scale computational tasks. This is particularly true for the kinds of parallel work on large data, optimization and numerical computation where pre-LLM machine learning currently dominates.

"Agent" still carries a very single-threaded, single-person connotation. What we now call apps -- the user-facing surface of a much wider computational substrate -- may be the analog to what we will eventually call agents, and a different term should be created for the general, learned, informally programmable effective computational machine of the future.

Perhaps we can come up with a portmanteau of machine and monster to describe it. Monstchine? That sounds awful.

Composed with [Noren](https://usenoren.ai/) -- a really cool AI assisted writing system that I to flesh out my thoughts while maintaining my own voice -- check it out.

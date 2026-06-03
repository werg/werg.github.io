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

Our first encouter with AI in the form of LLMs, within the product of ChatGPT was very much like an oracle. You ask a question, the oracle speaks, and that is the transaction. 
This story of course has been less and less applicable as we march on to the glorious future of agentic AI which, somehow, *does* things -- maybe even *computes*.

The original framing for machine learning was *function approximation*. This framing was of course accurate, but it does fail to capture what has been going on at our current juncture, where ML has turned into something we a lot more justifiably can call: Artificial Intelligence.

I remember getting quizzical looks from colleagues interested in machine learning when I complained that you couldn't do general-purpose computation with a specific model. I think we were talking about word embeddings -- Word2Vec had just arrived, and the potential for operating on words in a continuous semantic space was immediately apparent. Without compositionality beyond simple concept arithmetic, though, a semantic space was merely interesting, useful perhaps for search, but nowhere near sufficient for computation in any meaningful sense.

A very well-organized dictionary is still just a dictionary.

A favorite interview question of mine back in the day -- which no interviewee ever answered satisfactorily, and which bedeviled me too -- was this: how do you cram a variable-size input into a fixed-size vector in a workable way, such that you can run it through a neural network without drowning in vanishing gradients? (The recurrent neural network was the non-solution of record.) Transformers answered the question decisively: you simply don't do that (by that I mean cram it all in a fixed-size vector). You maintain a representation that grows with the input, at the cost of quadratic computation on it.

With that, we were no longer beholden to the fact that while neural networks may be universal function approximators in theory, they were not, in their original form, designed to handle variable-size data with variable computational effort.

Or handle variable-size data at all.

Naive function approximation gives you a mapping, but ignoring the inherent scale of algebraic compositionality. Informally, computation is algebraic compositionality incarnate. The difference may seem pedantic right up until you need the latter.

## Loops and compositionality

LLMs can obviously compute. Computation, understood 'properly', is modeled by following the rules of a formal language -- LLMs are simply extending this notion to instead follow the informal rules of an informal language. This may not meet the strict definitional requirements that logicians worked out roughly a hundred years ago, but it likely captures the spirit of what they were trying to define much better than we typically give it credit for.

Like the physical computers we are familiar with, language models are limited by finite context and memory. They are and remain imperfect models. (The interesting question -- as an aside -- is whether the imperfection lies in the theory or the implementation.)

Here is a fact about the history of computation worth holding onto: the most powerfu:l -- and indeed as I have argued before: excessively powerful -- thing we ever did was introduce arbitrary looping.

Primitive recursive functions are already remarkable -- you can compute a great deal within bounded recursion, with a termination guarantee on every call. But the decisive leap, the thing that opened up the full landscape of what is computable at all, was unbounded iteration: the mu-operator, the WHILE loop, the ability to say keep going until some condition is met and make no promises about when that will be.
The things we do around context compaction, subagents and discoverable context point in the same direction as the original argument for why we could treat practically finite computers as models for theoretically infinite machines: as long as you have a non-exponential algorithm, you can always add more -- more memory, more processing power and machines -- once you hit the limits of the original setup for a specific workload.

Now consider what a single forward pass through a language model actually is, computationally. A transformer with a fixed context window and finite-precision arithmetic computes a bounded function from an input sequence to an output distribution. The architecture is a circuit of fixed depth, not a machine with unbounded working memory. Each token attends to previous tokens, yes, but the computation terminates after a bounded number of operations determined by layer count, context window and implementation constraints.

This is not a criticism. The constraint is part of what makes training tractable. But it is a fact worth holding clearly when we ask what these systems can and cannot do structurally, as opposed to empirically.

A single forward pass is not computation with arbitrary depth. It is a very sophisticated bounded function application.

This is where agentic AI becomes interesting as a technical matter rather than just a product category. The loops that make computation powerful are being introduced -- they are just being introduced at the harness level.

The model gets called, produces output, that output modifies some state -- a file, a tool call result, a memory store, a plan, a test log -- and then the model gets called again with updated context, while the model itself stays fixed. The computation happens in the wrapper.

The harness provides the WHILE loop that the model itself cannot.

This also explains why the agentic harness looks so suspiciously classical. Context compaction, subagents and discoverable context point in the same direction as the original argument for why we could treat practically finite computers as models for theoretically infinite machines: as long as you have a non-exponential algorithm, you can always add more -- more memory, more processing power and machines -- once you hit the limits of the original setup for a specific workload.

I.e. for now, all we are using is the actor model, trees, a Unix file system and OS state, a shell and the ability to execute arbitrary code. Next to no additional machine learning fancy business.

This underlines the fundamentally computational character of AI as it stands today. LLMs are, arguably, much much better at performing computation -- albeit informally defined -- than at doing the other thing people historically associated with AI: acting like, impersonating, perhaps even being, a person. Memory, continual learning, caring about anything, having intentionality in any durable sense -- these may be simulatable over short local contexts, but at even medium scales they are more notable for their absence than their presence.

And this in an era when programmers like me continue to be genuinely amazed at what these systems can accomplish on the tasks I, an actual person define, premeditate and set for them.

The AI we have today is much more informal computation than it is artificial person -- and our ability to now instantiate informal computation is surfacing this distinction, much like the chess computers of the GOFAI era showed us the subtle difference between formal reasoning and actual intelligence.

## Entropy Is Friction

The standard objection to looping stochastic systems is that errors compound.

And sometimes that is exactly what you get.

In a deterministic program, a loop does what you wrote. In a stochastic decoder running for hundreds of steps, the trajectory through semantic space can drift, curl back or diverge in ways that have no clean equivalent in classical software -- a hallucination in step three can condition everything that follows. Naively, you should expect catastrophic degradation over long agentic runs.

But the empirical record is more interesting than the additive-error model predicts. When grounded by external feedback, long agentic runs sometimes self-correct -- a model writes code, runs tests, sees a failure, updates its representation of the task and repairs the mistake. It searches, finds contradictory evidence and revises its plan. A failed tool call produces an error message that flows back into context, and the model adjusts.

The entropy is real, but it is not always monotonically increasing.

Tests, tools, search results, execution traces and persistent state constrain the trajectory -- they prevent the system from drifting arbitrarily by forcing it to collide with the world.

So the entropy problem is real, but it is not a hard wall. It is more like friction -- degrading performance, setting practical limits and demanding engineering attention without preventing useful long-horizon computation from happening.

## Training The Loop

The harder question is what it would mean to integrate computational structure not at the harness level but at the optimization level.

Right now, the loops live outside the gradient.

While the model is trained primarily on next-token prediction or instruction following, the looping and state management happen at inference time, in scaffolding the training process never saw -- the model has to generalize from its training distribution to an execution context that is architecturally different from anything it was explicitly optimized for, and it works better than it should.

But there is an obvious mismatch -- and what makes gradient descent powerful is that it finds structure in exactly the distribution you train on. If the distribution you care about is multi-step agentic execution -- procedures over state, loops, error recovery, backtracking, tool use -- then training on that distribution, with the computational structure baked in rather than bolted on, should produce qualitatively better results. The optimization pressure would be applied to the right thing.

There are obvious practical reasons this has not happened at scale. Training infrastructure for looping, stateful execution is considerably more complex than for fixed-context next-token prediction -- compute scales badly over long rollouts rather than isolated forward passes, and credit assignment across dozens or hundreds of steps is genuinely hard. You need to know which early decisions caused success or failure much later, and that signal gets diluted fast.

These are real obstacles, not excuses.

So we defaulted to the cleaner decomposition: train the model on next-token prediction, add the loops afterward and hope the capability generalizes. The hope has been partially vindicated. "Partially" is the operative word.

What we do not yet have is a model whose internal representations have been deeply shaped by the experience of iterating, failing, self-correcting and succeeding across long computational trajectories. The loop still lives mostly in Python files, shell tools, orchestration code and prompt conventions.

We have trained the transducer, then wrapped it in a program.

## Verplankalkül

Which brings me to programming languages -- a topic deeply intertwined with computation and near and dear to my heart.

Andrej Karpathy is known for pointing out that English is now the biggest programming language. In a lot of ways I agree, or at least: a computable, computation-focused subset of English. But let's unpack this.

English is not a formal language. It has no strict syntax, no formally defined computational semantics. To capture anything equivalent to a programming language, we need to rework the terminology.

To that end I would like to introduce a new kind of programming language, which I will call Verplankalkül -- a portmanteau. Konrad Zuse, who built the first programmable computer, named his first programming language Plankalkül, literally "plan calculus." The German colloquial term verplant means disorganized, messy -- literally "mis-planned." Verplankalkül, then: a messy plan calculus.

An informal programming language.

The most popular Verplankalkül right now is English-language instructions formatted in skill files with executable script sidecars, with input data "types" that range over user prompts in natural language.

We already met the virtual machine it runs on above.

A widely-used term for this already exists, one I don't particularly love: the agent.

Including, of course, the agentic harness.

If we were going to stay permanently at this stage, we wouldn't need new terminology at all. Files and prompts, tools and code execution -- that vocabulary would suffice. My impetus for defining Verplankalkül as a concept is to anticipate -- and call for -- other kinds and variants of such informal programming languages.

I don't think we'll stay at this stage. I see movement on two fronts.

First: the agentic harness and its attendant software, as currently defined, is in a fundamental way not learned -- it is fixed, non-gradient-optimized formal computational cruft. I believe this will change. Harnesses will wither away, absorbed into learned behavior.

Second: imperative English is a poor proxy for many large-scale computational tasks -- particularly the kinds of parallel work on large data, optimization and numerical computation where pre-LLM machine learning currently dominates. The computational substrate is already broader than the language we currently use to steer it.

"Agent" still carries a very single-threaded, single-person connotation. What we now call apps -- the user-facing surface of a much wider computational substrate -- may be the analog to what we will eventually call agents, and a different term should be created for the general, learned, informally programmable effective computational machine of the future.

Perhaps we can come up with a portmanteau of machine and monster to describe it. Monstchine? That sounds awful. :)

Composed with [Noren](https://usenoren.ai/) -- a really cool AI assisted writing system that I to flesh out my thoughts while maintaining my own voice -- check it out.

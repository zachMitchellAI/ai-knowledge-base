# Youtube

Youtube channels that talk about AI

## Technique

These are people that are in the weeds with AI, or have an ear on the floor with people that are developing with it.

### Nate B Jones

Nate speaks like a coach to people who are on the edge of AI. His favorite models to talk abut at least from my personal memory are claude models

https://www.youtube.com/@NateBJones

### Theo - t3.gg

He creates a space to talk about AI through the lense of a discussion with co-workers and personal experience

https://www.youtube.com/@t3dotgg

### The primagen

Talks a little about everything; he hosts his own twitch channel, with these being interesting clips about various happenings in the AI space

As I'm writing this in real time it looks like he does other things outside of AI too

- https://www.youtube.com/@ThePrimeTimeagen
- https://www.youtube.com/@ThePrimeagenHighlights

### The Neuron

They have a dedicated website, along with this youtube channel - they find the scoup on some very niche sources with both the current position of AI, and the future of it

- https://www.youtube.com/@theneuronai
- https://www.theneuron.ai/newsletter

### Two Minute Papers

https://www.youtube.com/@TwoMinutePapers

They talk about large language models in great detail, and how scientists and others are either putting it to work, or discovering common patterns & pitfalls.

"What a time to be alive!"

## Objective

People that are looking at the numbers & finances, asking "why". They may or may not like ai... but either way display a very blunt opinion and understanding.

### The Tech Report

They are looking at the industry with the lense of finance & stocks. A lot of what I hear from them stems on data centers not being built, the business model behind OpenAI and Anthropic, and what would happen to companies like Oracle, should they choose to continue down this path of an alleged AI Bubble

His opinions are strongly towards "AI will fail" - big statement, but nonetheless shares big takes on the money side of it all.

https://www.youtube.com/@TheTechReportTR

### Awesome

Love this guy. He's not purely an AI youtuber, in fact he does much more than that. He talks about javascript development too!

https://www.youtube.com/@awesome-coding/

# Individual videos

I have a strong feling this will break down into smaller files later. Will I talk about specific videos here? I'm not sure; if there's something big that jumps over my way, I'll view it and put down my notes if the impact is large

## Anthopic, OpenAI Should Not Be Allowed to IPO, Says Ed Zitron

This essentially is the summary of what [The Tech Report](#the-tech-report) is constantly pumping out, except his journalism is shared with Bloomberg

https://youtu.be/zbKDmkJPVvI

## The brain eating machines

From the Channel - Emergent Garden

This is an interesting video where there's creative AI being used to errode human skills, relationships and other things.
A big premise here is that, without practicing things, that stuff becomes weak. There's a high suggestion to continue building such skills, despite everything being able to be created on a whim.

Paraphrasing:

> Craft is slow, and grueling, and there's nothing quite like it.

It also talks about the very common (right now) situation where there's a lot of low-effort content that is designed to provide dopamine over actual value, basically like sugar.

The author himself uses models to do things as well, so he tries to remain grounded on where we can go.

https://youtu.be/kVjhV-In25c

## "It Finally Happened" - Primagen

Really good video about how ethics behind LLM coding are being challenged right now by major projects such as zig and FreeBSD

In a nutshell, for the sake of education and strongly understood systems, both of these projects are not accepting AI contributions. I completely understand this, in fact someone's understanding can only create results of said understanding.

Primagen also talks about something called `Vouch`, which sounds really interesting. Basically he talks about a system where people can be trusted to build with AI in ways that make sense

https://www.youtube.com/watch?v=pkndFYSTr0Y


## I guess we're writing loops now?

Theo t3

Very fascinating take on solving code issues. The video itself goes over the concept of agentic looping, in other words a way to have agents create their own coding & feedback loops

* an agent begins to solve a problem
* commits code to a branch & creates a PR
* subsequent agents self-review the code and *another* agent goes back to fix things
* This loop recurses upon itself until there are no more changes that the review agent requires (even after several rounds of PRs)
* Repeat based on phases of the problem being solved (phase 1, phase 2, phase 3), with each of *those* having their own loop

Costly? Yes. Impressive? Yes.

https://youtube.com/watch?v=iJVJwmCKW9o

These problems are particularly interesting because they try to tackle the ambiguity issue of problem solving itself with code.

Below I'd actually like to share a *different* side of the equation too

## Stop making models bigger, make them behave

Kobie Crawford

I really appreciate this take here - a lot of people are making use of > 500B param models. However this person points out that it's possible to specialize a model with specific training. By doing this, a 4B parameter model can outpace tasks that a very large model can take.

It's being able to harness the usefullness of models, while optimizing them for well-defined, concrete tasks. It plays on another level over just simply a harness. The context is instead baked in, in contrast to being tacked-on. (long-term / short-term?)

There are some places here that talk about training a model as well. It talked about being able to train a model for 500$; which is fascinating.

https://youtube.com/watch?v=TNwJ1LMiENk

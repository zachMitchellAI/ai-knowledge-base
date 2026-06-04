# Discovering Use Cases

Large Language Models are prediction machines. In other words they receive an input and attempt to mirror an output based on training and reward.

"Mirror" is an intentional word here, because it's baked into how these systems work fundamentally. One of the first notable examples of this was a project called "talk to transformer", by early OpenAI (GPT stands for "Generative pre-trained *transformer*"). Talk to transformer's abilities were primitive compared to today, but the way it would work is:

* User types in an input "Oh my gosh! I just saw"
* and the model completed it: "a rabbit cross the street!"

That's all there was to it. Now that companies have experimented on this greatly, they've learned much more about how to optimize this technique.

The overall point made here is, *models are a mirror of the inputs, but with a agent-like, conversational flow in it's training*.

---

What does this mean for possible uses? Well, if you can think it, the seed of output is more than you can human-ly conceptualize. That's a lot of different outputs, useful or not.

Models have gotten a lot stronger at determining the use-cases we'd like out of them, but even so, we should also be reflecting that back just as they do to us. In other words - how do we know what they would be good at?

Let's break this down, because I think there can be a good systematic way to determine the uses. It depends on a lot of things, so each will be talked about in detail.

# Motivation for writing this

The biggest complaint I hear either up the grapevine or from news sources, is that uses of Large Language Models very much get "shoved in" without giving it much second thought. It's clear to me that when something is new, it's easy to go swinging with the new tool, fail quickly and learn quickly. It's also clear, that when something is ambiguous with context on how to use something, that *also* causes mistakes, trial and error.

Not that either of these are bad, but the math is pretty simple right? Ambiguity + Ambiguity = Lots of Ambiguity.

It'll take a while for us to really fight this fog the right way, and that's me saying this even though we've already found tons of use-cases already!

The worry I see out of people is that use-cases will be assembled poorly and executed poorly. It's already happened and has tarnished a very disruptive and cool technology.

What I aim to do is to not just figure out how to "use it right", but rigorously and systematically test pieces, then execute *working* patterns. Not a hope & promise, but lots, and lots of trial, and error.

So here's a way to do that - perhaps not *the way*, but *a way*.

# First: Determine high-level details

* What are you looking to do?
* Can you do this already?
* *Are* you doing this already?
* And can you do it faster?

Applied example:

> I'm a software engineer that's building a change and needs a pull request... those PRs, oof. They take a while to do when I could be doing work, and then I have to let my co-workers on slack know the PR exists... hey wait a minute!

This here would be an example of something I'm already doing, but perhaps could go faster? There's a lot of work that I have to dance around in order to just, submit work for eyeballs to see. I think it would be ideally better to have a lot of handoff from this, since it's also something I've done hundreds, if not thousands of times. It's a roadblock regardless of how fast someone can do it.

We'll trail off this example for the rest of the page, but it's also worth keeping in mind, that this is a tested example of automation

## What if you're trying to automate something new?

We already know that above process extremely well, it's a great candidate for making already what we know faster.

Yet it also makes sense to figure out things we *might* not know. Yet, that introduces ambiguity right?

There needs to be a systematic way to cut through the fog. The Software Development Life Cycle (SDLC) is a decent compass for something like that. These will usually share:

* What is the expected problem to solve
* Where we are now
* What's the expected outcome

If we know a few of those things it's then possible to assess the next part:

# Second: Determine what you have

* What's in our *tool*belt [get it? tools?]
* How would these behave together?
* What do we not have?
* What would it take to learn how to use what we do and don't?

Applied example:

> I have a few tools available to me: the code editor's built-in tools, the GitHub MCP server (or CLI), the slack MCP server, and the rovo (atlassian) MCP that has access to jira tickets.

Already there's a lot we can do here - and you can easily see how this can come together for a process you already know about.

In fact one of my favorite things about thinking about it in MCPs (or specific tools), is that they compartmentalize possible steps with an action that can be taken. The actions are known and known well! When you understand how the actions would behave, based on the platform you're connecting to, that reduces a lot of ambiguity, especially when these actions have some pre-baking with tool execution.

---

Maybe the process isn't MCP reliant, but instead requires an API call or a CLI-command, that's where building agent skills, guidelines, and/or harnessing go into play.

It's hopefully clear what's trying to be done right? Even if there's not a carved out "LLM-shaped square hole", it's still possible to extend context, whether that be describing how to use a command in detail for a model, carving out maybe a *new* MCP through something like FastMCP, or perhaps even building a shell-script that does a few pre-defined things that you absolutely know the model will need.

The more clear intents are, the better both you, and the machine can figure out tasks, regardless of how big or small the AI may be. Speaking of which:

# Third: Determine how much

* How much of the LLM do we need?
* No, really - how much do we *really* need?
* How many tools are required for the job?
* Required context window?
* Does it require a big LLM? Smaller?
* *can we do this with an on-device model?*

Applied example:

> I only need a handful of tools from each MCP, the "Jira ticket" tool for updating ticket status, the "send message" tool from slack, the "pull request" tool from GitHub, and the commands for `git commit` and `git push` in order to send my changes out to the target branch

> I *could* use opus for this task, but that's a lot of tokens and it likely would not be as fast. It might make more sense to use the composer model or a smaller one like gemma (gemma runs on my local machine).

So, a few things here worth noting in this - a lot of IDEs will enable all the tools on an MCP server by default. In the context window, it *has* to read all those tools to understand what it can do, unless you're reading this in the future and we took the route of the "tool search tool" (which indexes related tools instead of bloating the context with everything at once).

Given this, present you might benefit from only turning on what's absolutely required. Larger models do a better job at retaining the context for more tools at once, though every bit of context window counts, because the more space it has, the more accurate the task execution will be.


---

A lot of small models will really struggle if you give it 10 tools, but you only need 1-3. (We're talking 8B parameters & up). They'll see 10 tools and think about each one, sometimes a little too much. They might not even come to a conclusion on what to use because of choice paralysis! (Humans do the same thing actually, more choice has less satisfaction / efficiency over more clear choices) 

This concept does in fact scale, which means we have to keep a model's context window efficient if you want good results.

## Selecting a model / set of frameworks

If figuring out tooling and context wasn't enough, there's the aspect of getting the model right as well.

I get a very strong impression that production use-cases may select a small model, but flood it with too much context. If that's the case (and I could definitely be wrong), then the model may presume something that isn't actually there (hallucinate) or not be able to handle certain intricacies that a larger model may have done better with (Wait... was a larger model rigorously tested and then a smaller model thrown in there last minute? Oh dear... I hope not)

Because perhaps ideas *are* good, and *do* work in practice, but then that doesn't work when we throw it into our supposed compression chamber of model distillation. That's not good, so perhaps we should be changing a few things, or asking some questions:

* a big model can handle X amount of context and provides Y result
* A small model took X, but gave us Z instead
* Could we give the small model A, B, and C, but ultimately provide Y just like the bigger model?

That's what we gotta find out, but that also means that the context changes, available tools change, or simply being more specific with the model changes ("use the git.create_pr tool", instead of "create a pull request")

I already shared with LinkedIn my EEPC Seashell, the laptop with 2GB of RAM but can still do many things a modern-day laptop can with enough oomph. I can't put windows 11 on it, the processor is too old, and there's no TPM. I unfortunately can't play tetris effect on this laptop with an NVIDIA ION, and can't even run opencode because bun is compiled for an updated instruction set for x64.

What I can do though, is change the frameworks to get a result that actually works. Windows 11 -> Arch Linux with sway; Tetris Effect -> Nullpomino, viteteris, or apotris; opencode -> kit or ollmcp.

Same intent, but different frameworks.

# Fourth: Delegate and compartmentalize

* Can a task be broken down into different steps at once?
* Does the model or IDE support sub-agents?
* If not, *can we still make it happen*?

"Zach there's been a ton of breaking down already!" - That's the point! We gotta keep going!

Each part of breaking it down clears up more & more confusion. As per the other half of the Unix philosophy aims to do:

> Do one task, and do it well

The more that task is shaped out, the more clear our intents will be. This doesn't mean that each individual task requires a shell-script or a binary telling the model what it needs to do, but it's worth rounding it out so that the task can be accomplished with clear intentions.

In the applied example, it's mostly a sequential process - commit, push, change ticket, PR, send message. However we could indeed optimize it further if we'd like to.

The process is simple enough that a model can just grab the tool context, receive basic instruction and do it all in one go. Though if this were a bigger task, is it worth breaking it down into parts?

It might, but just as previously mentioned with model selection, testing is important to figure this out. A bigger task might involve invoking smaller models to do reading & writing to the disk. If you want to go *all the way*, you could even use something like langchain, create a tool-call that possibly in itself invokes one or many models, then return a result based on *their own* tool calling. All wrapped up in a single python or JS routine. ( By doing this, in theory it could mean even smaller, distilled models could call sub-agents. Is that a good idea? That's an iffy one, but worth trying out )

That is in fact something I forgot to touch up above - You might not even need to make the model the forefront of the process, but rather have a script that then calls the model for your task. This could be good for example when you're trying to ambiguously figure out some text, and pair it with a built-in selection of your application.

Intentions nonetheless in either should be clear. How much clarity? Good question, but if you walk that tightrope effectively, it'll do much better than just going in, guns-ablazing all the time.

# Fourth: Test & Verify (Please!!!)

* Does it work?
* Are you sure?
* Did you test that one edge-case?
* Does it reflect those design interviews with real customers?
* What about your stakeholder group that uses your product early and uses it all the time?
* And like, is there a fallback plan?

For the simple PR example, this part might have less tension on it, mainly because the stakeholder and customer is you. Though, it's still important to consider no matter at what scale "does thing work?"

There are hundreds of unit, and component tests in codebase for a reason - the system needs to vigorously work at all costs. That kind of care is something we need in handling LLMs too. It's a big tool, yes, but that also means a big impact if something isn't done right.

Infamously to me, that's where I've heard on the street - "If you don't know how to do something, a tool could help you fail at that harder".

Wheatly, from Portal 2 very much reminds me of that. As an AI himself, he tried taking the place of GlaDOS - but he has literally no experience with maintaining a facility and almost caused it to explode near the end of the game. (And literally right after GlaDOS brought it back into working condition).

Needless to say, it sounds like doing something, and doing it right may be crucial. That gets harder with tools like this, but it also means very good treatment should be done to ensure this will flow and purr.

See how the process runs, not just with yourself, but with customers / stakeholders, vigorously, tirelessly, and effectively. The workflow will be really nice at the end, and trust & rapport by definition will scale with that.

# And you're done!

Well... not really, because then the process will change again when the new model or tool comes out. Worth keeping up, or otherwise the methods we know now, will differ later. It should be obvious though given we're changing a lot as we speak.

I can now finish that PR workflow within seconds while I grab a cup of water, but is that workflow going to stick later? Does this process maybe look different or becomes obsolete later?

Good question - we'll have to keep iterating and stay awake, it's the best way after all to do that one task, and one task well: implementing the workflow with strong accuracy.

# What are tools and MCPs? (Also how do you select the right ones?)
 
There is someone I think about quite a bit in the realm of tech. His name is Ton Roosendaal, the original creator of blender. He was once asked a question on YouTube, something around the lines of: "Do you care for money? Even if others are banking off of your software?". He replied: "Nah, [...] Money is a means to an end."

Profoundly, he certainly has a goal being done. The way he manages said money is used to further develop something *good*, which is 3D rendering software that actively competes against some of the most ambitious projects in the world. It's a testament to open source software and it's mission: bring people together through quality efforts, not necessarily profit. (In fact a lot of software is indeed constructed by literally, non-profits)

---

What exactly does this have to do with the title of this article? Well, Ton treats his efforts in the direction of an educated movement in it's rawest form: render 3D objects, and do that very well. In the context [of a previous post for discovering LLM use-cases](./discovering-usecases.md) , ... gee that sure tends to amplify it's complexity when that "tool" is effectively a creative generator of outputs based on inputs (vague if not careful, discrete if intentful). Though, this time I find it worth the effort to describe this effort for the utilities themselves; the components that bring a little more order to an otherwise chaotic system.

These, while they bring more focus, are just one component of the entire ecosystem engineers, or otherwise coordinators of a fleet, will have to learn how to wrangle depending on the tasks desired to be solved. In addition to tools, and MCPs, there's also scaffolding, contextual awareness, sub-agents, and more.

For this *single slice* of the puzzle, a few things will be discussed:

* What is a tool?
* What are MCPs?
* How does one decide to use tools?

This will be communicated from an engineering perspective. It dives into technical details, but drives them forward in human explanations.

Let's get into it.

## What is a tool?

I think it's worth breaking this down into a fundamental piece because when I first started, I focused a lot on the bigger pieces first. Doing it at that level didn't really help me understand ways to help optimize resources at first, and made an "MCP" this nebulous concept: "This thing makes the LLM do a lot of things"

Which those "things", are **tools**. A **tool**, is a singular function that may hold the second half of the Unix philosophy:

> Do one task and do that task well

Examples may include:

* list the files in a user's directory / folder / path
* download a webpage
* check the health on the device's battery
* Move a game character in a certain direction (LRUD)
* Apply the bucket-fill in a paint program to coordinates `X,Y`
* Convert Celsius to Fahrenheit
* Count how many values in a CSV file start with the letter "J"

Clear, directional instructions that the LLM can run, which give it further direction and information on it's surroundings. On Unix, programs at this level of simplicity are strung together in `scripts` that can be combined in a way to solve bigger things, very well in fact (because they do one thing well), and bring out a highly educated result more than the sum of it's parts can or ever could.

What if though... you have a direction, but *don't know*  the remaining parts of the outcome? You have the utility, but the remaining problems are ambiguous, unknown, or even "stretchy" or highly variable? Well, LLMs are pretty stretchy and creative, and you've now provided very clear & defined tasks and building blocks to follow.

A chaotic creativity and a strong order may now be combined into a unified coordination. *That* is where the power absolutely resides. It unlocks a lot of things! You're using a computer right now to do exactly this - combine things like google chrome, spotify, and your productive program of choice, and what's present is an amplification of intent and action, not just *playing pretend*.

LLMs don't need to pretend either when they have the real deal, which is what's being provided in this context.

We can take it a step-up though, but before that, a step before that one:

### How might an LLM read these tools?

This is an interesting part of the equation. In the context of "langchain" (embedded LLM tool-set) LLMs will read tools *like a list*. That means, out of the box it may not know where these tools come from, just that it has them.

From the engineering perspective, it's literally putting a list of functions & classes into an array in langchain itself. It might behave differently under the hood of something like langchain, but at minimum, an initial prompt for a language model is going to include these list of tools, and a light description, along with parameters that the models knows exists in order to use it correctly. There's no "need" to search because the LLM will remember what they are from the automatic scaffolding. 

This pseudo-code should describe roughly the way it would be internalized:

```json
{
    "name": "math_operation",
    "description": "Add, subtract, multiply, or divide two numbers, based on the desired request",
    "parameters": {
            "operator": "string", // add, sub, mul, div
            "num1": "number",
            "num2": "number"
        }
}

// Output may be JSON, YAML, or Plain text. Ideally the developer should at least supply something friendly format for the model. The more clear, the better
```

It's a clear direction on intent & action, and more specifically, the LLM will know precisely how to interface with it. In Unix land, the analog for humans is running a command's `--help` flag. It also gives us a good idea on what everything does:

```
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all
         do not ignore entries starting with .
  -A, --almost-all
         do not list implied . and ..
      --author
         with -l, print the author of each file
  -b, --escape
         print C-style escapes for nongraphic characters
      --block-size=SIZE
         with -l, scale sizes by SIZE when printing them;
         e.g., '--block-size=M'; see SIZE format below
  -B, --ignore-backups
         do not list implied entries ending with ~
  -c
         with -lt: sort by, and show, ctime
           (time of last change of file status information);
         with -l: show ctime and sort by name;
         otherwise: sort by ctime, newest first

[...]
```

Depending on the command, their format might differ, because well, life is messy and we have a bunch of programs, written by different authors, built upon different scaffolding we call programming languages. They all have differences in printing out this help page (either a library, just straight-up print instructions, etc), but ultimately the goal is to use at minimum, parameters, and if you're more cordial: flags, which tell the program to look for something specific.

`tool`s, unify this concept in an otherwise messy world. And yes if you're wondering, it's absolutely possible to have a tool directly call a traditional Unix command, through a designated programming language like python or typescript. The goal here would be to provide similar scaffolding shown previously instead of the help file, so that the model can fluently understand what it's getting itself into.

(And worth noting, in practice at least on desktop-class workflows, this might not be necessary since people just run `bash`, but the point still stands. It *especially* stands in production environments where things need absolute certainty that it'll work as intended, protecting against things like prompt injection)

---

So then, tools are:

* highly re-usable tools
* that are clearly defined
* contain parameters that are well understood
* (hopefully) output a result that is easy to understand, or has the required context

## What are MCPs?

Nice, we now have tools which clearly define what we want to do on a fundamental level. Though, how do the bigger problems get solve *in relation to the specific field?*

> Ok, we want the ability to use the entire file system (create, read, write, update, delete, sort, filter)

> Ok, there needs to be a birthday card created (`insert_image`, `set_title`, `apply_bg`, `set_subtext`, `set_body`)

> Ok, the adventurer is moving around in a text-based RPG (`get_item`, `attack`, `move`, `eat`, `open_backpack`)

This is a *collection of tools* to solve a more general problem

* file-system MCP
* birthday MCP
* adventurer MCP

It's tempting after this to say "that's it!", and in it's rawest form, that's true. But there are some more interesting parts I'd like to touch on that make it more interesting, namely:

* How does it talk to the LLM?
* How does the LLM know an MCP is for a certain task?
* Resources
* Prompts

### How does it talk to the LLM?

There are two main ways, and 3 that are not as common:

- Remotely - You connect to an MCP through the web (https://agenttools.wolfram.com/mcp), more specifically through `post` requests
- Locally - Via STDIO (Standard input/output), namely text

Remote servers allow for companies to share information through clearly defined tool definitions as previously seen. Only, we can't actually see how they do it, we simply expect to get something back in the shape they told us they would. Since we're making `post` requests, that means we're sending a call to a web-address, but also  what we'd like to do, most likely in a JSON format the AI will send out.

---

**STDIO** on the other hand, are for operations that run on your computer. It has the potential to change things on your device if you want, or just be a way to talk to things on the web either officially or unofficially. It uses the same inputs/outputs as a Unix terminal, meaning latency is *very* fast. It also means if there are things happening to the MCP, it can't be logged to the output like a normal program might do. It instead must output logs, and errors through the "error" pipe (that includes 'server started' messages)

[Edit - NOPE! Stderr is no more, according to the newest specification changes: https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/ - things are changing quickly]

---

In addition, there's also [In Memory](https://ts.sdk.modelcontextprotocol.io/classes/inMemory.InMemoryTransport.html) MCP servers. Of all variations, I was surprised to see this one. I don't really know a lot about it, but from the looks of things, it's possible to have MCPs that live directly in the same process, without having to execute anything external, such as a local `npx` execution in the terminal, or connecting to an outside, remote address. This could potentially be useful if the goal is to create an internalized environment where it wouldn't be necessary to distribute a collection of tools outside it's embedded workflow. By doing this, extra packaging wouldn't be required, and it would be possible to also link up resources and prompts to go alongside the tool collection.

The provider (MCP client) of the tools itself is responsible for gathering this information in a uniform way. With langchain, it runs a method called `get_tools()` to obtain the designated tools, and place both local, and remote tools, into a single pool that the LLM will have access to upon a request being created.

In any of these cases, it doesn't really matter *how* the LLM gets the information, all it knows is that a designated `tool` exists, it puts something in, and it gets something out.


### How does the LLM know an MCP is for a certain task?

Uh... well you see, they don't really, that's the thing.

At least out of the box they don't. Remember earlier when it was mentioned that *tools* are passed to the LLM? Well, it's just those tools. Not in a vacuum mind you, resources and prompts might *also* be there in a separate list, but MCPs? For LLMs it's out of the picture.

But then when you're talking to the model about what it can do, how does it know? Well for this I can share some output from a program running on my netbook: ollmcp

```


╭─ S4. ✓ filesystem ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                                                                                        │
│ 13. ✓ filesystem.read_file         14. ✓ filesystem.read_multiple_files  15. ✓ filesystem.write_file                16. ✓ filesystem.edit_file                         │
│ 17. ✓ filesystem.create_directory  18. ✓ filesystem.list_directory       19. ✓ filesystem.directory_tree            20. ✓ filesystem.move_file                         │
│ 21. ✓ filesystem.search_files      22. ✓ filesystem.get_file_info        23. ✓ filesystem.list_allowed_directories                                                     │
│                                                                                                                                                                        │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 11/11 tools enabled ─╯

[...]

╭─ S6. ✓ wolfram ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                                                                                        │
│ 68. ✓ wolfram.WolframContext  69. ✓ wolfram.WolframLanguageEvaluator  70. ✓ wolfram.WolframAlpha                                                                       │
│                                                                                                                                                                        │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── 3/3 tools enabled ─╯
```

Dot notation. So in other words, the model will know what this is for based on a prefaced name, followed by the tool name itself.
Now, it's possible that this is purely how ollmcp handles it. Other MCP clients may handle this in a different fashion or describe where they came from through other means, via it's initial prompt or scaffolding.

If we use something like `opencode`, gemma4 tells me that it sees the tools like this:

```
[...] from my perspective, these tools are provided as a single, unified collection. There is no metadata, prefix, or namespace (such as server_name__tool_name) that indicates which specific MCP server provided which tool. They all simply exist within my available toolset.

🌐 Web & Information Retrieval
These tools allow me to gather real-time data and documentation from the internet:
*   webfetch: Fetches the content of a specific URL.
*   brave-search_brave_web_search: Performs general web searches.
*   brave-search_brave_local_search: Finds local businesses and places.
*   brave-search_brave_video_search: Searches for video content.
*   brave-search_brave_image_search: Searches for images.
*   brave-search_brave_news_search: Searches for current news articles.
*   brave-search_brave_summarizer: Generates AI summaries of web search results.
*   brave-search_brave_llm_context: Retrieves high-density text chunks from the web optimized for LLM reasoning.
*   brave-search_brave_place_search: Provides detailed POI (Point of Interest) data.

📋 Trello Integration
A large suite of tools specifically for managing Trello boards, lists, and cards:
*   Board Management: trello_list_boards, [...]
*   List Management: trello_get_lists, [...]
*   Card Operations: trello_get_cards_by_list_id, [...]
*   Card Content & Interaction: trello_add_comment, [...]
*   Checklists: trello_create_checklist, [...]
*   Members & Labels: trello_get_board_members, [...]
*   Attachments: trello_attach_image_to_card, [...]
*   System Health: trello_get_health, [...]

As you can see, while I can logically group these by their functionality (e.g., "everything starting with trello_ obviously belongs to a Trello server"), there is no official "server ID" attached to the tool definitions themselves. They are simply tools in my belt!
```

So over here, an *underscore*? Interesting. Depending on the program, it interprets a way to differentiate the tools along with the MCP. Not explicitly saying "this is an MCP server", but a specific way to at least nod "This tool goes along side this collection of others". Could an IDE possibly just... not include them at all? Probably, but this best-practice being done at some capacity certainly does help with ambiguity it seems.

In fact we can touch one more place that does exactly this - langchain:

```
for item in tools: print(item.name)

brave_web_search
brave_local_search
brave_video_search
brave_image_search
brave_news_search
brave_summarizer
brave_llm_context
brave_place_search
```

And from here, the raw output stands out. On the brave tools, just like in ollmcp or opencode, we see that it has `brave_` at the beginning of at least, the tool name. (Not an MCP name) On the wolfram MCP, it follows a similar practice, except their MCP server is using `PascalCase ` instead of `snake_case`. Unfortunately, it seems like the third-party MCP servers *do not* have a prefix of any sort, which means an IDE would need to pick up the slack, just as ollmcp and opencode did. (opencode: `brave-search_brave_web_search`, ollmcp: `brave_search.braave_web_search`)

---

In general, tools are provided - for what exactly? Well the MCP client (talking to the LLM) should somehow get this done, either through that dot notation that ollmcp uses, or through it's scaffolding (e.g "you are an agent that possess the following MCP servers: Wikipedia, git, file-system")


### Resources

**Resources** are similar to the concept of "skills"; they are markdown snippets that tell an LLM tips & tricks for making use of their tool-set. Take for example this pseudo snippet:

> If brave search fails to execute after a few tries, it's possible that it's rate limited. Please take a pause if this happens, then attempt another search. If the problem persists after this, let the user know that they may need additional authentication, or payment method to bypass the rate limit.

Tips like these can guide the model into a more generally available direction when using some of the tools. They are only ever called for "when necessary", so if there is a related tool in-use, the model may pick up this resource to better understand how to use it.

### Prompts

**Prompts**, are interesting. They are not seen by the model directly. Instead, they may be either a static string, or a dynamically generated one, specifically tuned for the context of the situation. These literally inject thoughts of conversations that *didn't actually happen* between the user, and the LLM. Rather, they emulate a hypothetical conversation for a best-case scenario to steer any LLM into a more desirable outcome before running any tools.

Here's an example [from the GitHub MCP](https://github.com/github/github-mcp-server/blob/63d313a9735e3b353dedc153c441b749c36daad4/pkg/github/workflow_prompts.go#L68)

System Prompt:

> You are a development workflow assistant helping to create GitHub issues and generate corresponding pull requests to fix them. You should: 1) Create a well-structured issue with clear problem description, 2) Assign it to Copilot coding agent to generate a solution, and 3) Monitor the PR creation process.

"User"'s prompt:

> I need to create an issue titled '%s' in %s/%s and then have a PR generated to fix it. The issue description is: %s%s%s

And then the "Model"'s prompt:

> I'll help you create the issue '%s' in %s/%s and then coordinate with Copilot to generate a fix. Let me start by creating the issue with the provided details.

Back to the "User":

```
Perfect! Please:
1. Create the issue with the title, description, labels, and assignees
2. Once created, assign it to Copilot coding agent to generate a solution
3. Monitor the process and let me know when the PR is ready for review
```

And finally, the last fabricated transaction with the "Model":

```
Excellent plan! Here's what I'll do:

1. ✅ Create the issue with all specified details
2. 🤖 Assign to Copilot coding agent for automated fix
3. 📋 Monitor progress and notify when PR is created
4. 🔍 Provide PR details for your review

Let me start by creating the issue.
```

---

Crazy right? Much of this is a lot of under the hood operations before the tool actually runs. It touches upon something specific, in that when you're using *anything* in a model, it'll never just be your own words. Much of it isn't, and in fact, tools like langchain, or even just using the raw API for a model, allows for manipulation of conversation text itself, just on it's own. It's not only feasible, but a necessity at times when the developer wants to tailor a specific experience for the user.

One extra trick, not necessarily related to prompts, but just the concept of *prompt fabrication*, is that it's entirely possible to share the conversation history from one model, to another. That means, one language model can perform some initial answering of questions, but a *different* model could continue it all-together. Big model? Small? Doesn't matter. Very strange to think about, especially when on the consumer side, there is a lot of vendor lock-in, and you can only talk to a GPT model on OpenAI's website, and a Claude model on Anthropic's. If you're running a third-party application such as opencode, cline, or openclaw, this can be mitigated, and models can basically share a soup of past thoughts and actions.

### In Summary

That was a large amount of information, but it's because MCPs are quite extensive. They are:

- A collection of tools, "prompts", and resources
- Each of which together, help to achieve a specific task
- Can be connected to, either locally (STDIO), remote (http[s]), or in-memory (RAM)

## How does one decide to use tools?

This is a very broad question, but a fascinating one. At this point we've touched already on some interesting concepts about how tools, MCPs, prompts, and resources all behave:

- Each tool is capable of doing one thing and one thing well
- MCPs encompass a collection of these Unix philosophy functions
- While also storing dynamic "prompts", and resources for the LLM to perform it's best

With all of this, it actually brings me to the first point:

### 1. Be selective with what you use

Does the above sound like a lot of information to send to an LLM with limited context? It most certainly is, and in fact there are a lot of reasons to be selective with tools:

- More tools = more context (at least as of now)
- Which affects input token costs, therefore money
- But also affects output quality, which also means *more* money spent if the output isn't strong

Plain & simple that's genuinely a literal cost factor to getting this done right. If you're paying per-token usage, this is going to hurt the bottom line. It's like asking the intern "Hey can you grab a file out of the cabinet? Oh and don't forget your heavy tool belt of 70 tools you must wear while opening it. I put the key in the tool-belt somewhere, good luck". I uh, have seen very small models work with just this scenario (8B-12B), and they panic very hard on what's available. There's too much noise, and it's clunky to even walk around in the first place.

Conversely, if you're more optimized, and the intern only has the key - they can very quickly get that task done. No extra weight to carry, the context is clear, and the objectives and how to unlock the drawer is good to go.

Context window, tools, and additional resources are a big deal; they literally are time & money savers if performance can be optimized. How does this work in an IDE though? Well, IDEs like cursor and VSCode allow individual tool toggling, permitting you in-app to turn things on and off. Some programs, like kit, opencode, and cline however, need more explicit toggling of tools, either in a designated JSON file, or through a wizard in cline's case.

Once your tool-belt is streamlined, let's move on to the second step:

### 2. What tools are needed cross-ecosystem?

MCPs are powerful when combining ecosystems across each other. For example figma and confluence go great together, because developers can view the contents of a jira ticket, view the figma details of a design, then identify the part of their codebase as to where the component should land.


That's all well & good, however the thing is, that ultimately we need to actually solve some problems. There's a lot of potential in this collection of items, but we need to figure out how to turn that potential energy into kinetic.

I'll be open about something here! When I was quite young, I started using a laptop with Linux on it back in 2013. Young me wanted to do stuff with that Linux laptop because it received a fresh hard-drive (thanks dad!). What did I wanna do exactly? Well, honest to goodness I wanted to play adobe flash games and hook up my gamepad. Flash isn't around anymore now, but that was the quest - run some flash games and control them with my gamepad.

Though, for a work environment I'd imagine the situation would be a *pinch* different. We certainly aren't using flash anymore (I hope) or use google chrome plugins, such as pepper flash for a 32-bit system. Though there might be things that are in fact useful for the business side, such as compiling and SDLC to jira tickets, or perhaps on the consumer side of things, they may be constructing a workflow that holds a lot of data points in varying areas.

If this was personal work, you might be tempted to get all the things on your system, for all those "what if"s, though the more we understand what customers are looking for, the more we can optimize and construct a process as a first-pass to gather additional feedback. The more these intents show up, the more it's possible to say "Hey, not only should an MCP gather this context from our SQL database, but it should be clearly cut-out, so as not to experience any prompt injection during retrieval"

In addition to gathering one tool, you sharpen it where possible. It's then possible to Select that for the next task. "We have the items queried from the database, it now needs to be imposed into other workflow portions. Based on previous context, the next tool should be shaped to query fluid information about a, b, and c".

An old robot from 2004 once said "see a need, fill a need" - that to me spells out how one would need to take in these problems. If you find something that could be optimized, these tools that you routinely use every day might relate more to what you're looking to solve than you think. As tempting as it is to just "throw it into the soup" of AI, finding that moment to say "I use these things all the time, they might logically go together in a potentially straightforward, yet creative way", is going to shine quite a lot.

### 3. More rigidity or more creativity?

I titled it that, but there are plenty of analogs here: order & chaos was the original header for example. What I mean to this by the way, is figuring out what works best for business situation.

For consumer grade products, there's high expectation for something to operate like clockwork. It's a high-class product, while it's possible it may be able to do a lot, the components provide the ability to do it with strong accuracy.

Would this pose for the tools, and the LLM to take more of a back-seat over the entire workflow? Well, let's think about it for a moment:

- The task we managed to define above - let's presume that's: collect ambiguous information from a database, then spread it out to other parts of a proposed workflow
- Can we do it with more "user facing" AI? Probably so.
- Is there a non-zero chance of it *not* doing that task? (whether that be parameter size, training data, other anomalies), that's wroth testing
- Could this task be further hardened? For example can categories be collected, then more effectively registered as regex to better accommodate a customer's needs? If so, we could almost mirror the philosophy of a just-in-time compilation (JIT)

If we make ambiguity front-facing, there are challenges that may approach the user. Whether or not this *actually* happens, depends on how it's engineered. Maybe it's not necessary to put ambiguity in first, perhaps a straightforward UI can help, and then ambiguity fills in any gaps. Maybe perhaps it's somewhere in the middle, and you *do* share ambiguity, but a much more hardened process (through langchain, MCPs, and strong routines take the wheel), and the problem is solved.

Depends on the customer, what their expectations are, and if their inputs can be trusted depending on the ambiguity you're willing to allow the interfacing of.


---


Now, as the person actually putting in the work - the position might be a little different. An engineer's entire job after all is to deal with high ambiguity in order to drill a problem into solvable bits. In this case, ambiguous-facing components might actually *help* an engineer, so as long as it's able to help clear up a problem in a way that's transparent, effective and follow-able.

You could also be a product manager, or a data engineer that would like to collect intentionally ambiguous information because it already comes from all over the place. In this case, creative problems promote creative solutions, to people who are ready to take things on in that regard.

This dynamic, is fascinating, because as knowledge workers, we have the goal to turn ambiguity into clearly, solvable bits. It may honestly be opposite facing to what a customer is looking for - in other words a solution that might be straightforward, and might benefit from steering into the right place in the right time.

That isn't to say, perhaps the customer *is* another knowledge worker or one that needs a truly, fuzzy problem to be solved. In this case - the LLM might honestly *be* that interface their looking for. However, I'd argue that simply putting in a chatbot and saying "problem solved" would be disingenuous if there's more to something a customer needs.

You, as a knowledge worker may genuinely benefit from the ambiguity, and that can be fantastic should we learn how to optimize our own workflows. Conversely, if we ourselves figure out how to then say "Oh we can make this much faster and more clear", we practice the ability to make even more use out of resources. The LLM as the primary interface can start us on this journey, and can be truly powerful. Yet the more we learn about ourselves, the environment, and what we need to do - it'll be quick to discover that we not only can make our one of a kind workflows stronger, but more effective, in the process.

---

I'll be honest and say this - I really didn't give a clear answer up there. And that's because everyone's problem is unique! You might thrive in ambiguity, but the customer might benefit from more straightforward decisions and a clear outcome. Although, it could additionally be the opposite. We must assess the environments being worked in, in order to attune to "what will clear up the bottlenecks", and perhaps those prompts from the customers (yourself included) might turn out to be *great* optimization opportunities for people, and they may not even realize they needed it.

## Embark on that MCP journey

This accidentally became a flow of "Ok MCPs are incredibly detailed", to "select your tools, use them well". In fact this article could easily be split into two. At the same time though, there's a direct translation to what I just said there: "with great power, comes great responsibility"

So, this post will hold both of these in tandom. MCP is powerful, it helps people do many things, whether that be customer facing, or as a process behind the scenes through langchain. With this much power, just as programming languages already help us with, we do have to acknowledge that if we make something sharp, we can responsibly build something, and build it well, so the user can have clear goals, and intentions, with the investment and time they were willing to share, by clicking "sign up", or "contact sales".

---

Thanks for checking this out, hope the day is a good one!

# LLM

## Synopsis

A Large Language Model - it's purpose is to generate useful text-based output based on a [prompt](./prompt.md) given by a user.

- LLMs come in many different shapes and sizes. Typically the size of an LLM is measured in [parameters](./parameter.md)
- They predict the next word of their generation using [tokens](./tokens.md)
- There might be many models sandwiched in one model, this is called [Mixture of Experts](https://en.wikipedia.org/wiki/Mixture_of_experts)


## Use-cases

LLMs have a vast range of uses. While they can be used for a lot of things, to find a dedicated use-case takes a lot of trial and error.

Near the start of the AI-Adventure, [chatbots](./chatbot.md) were the very easy cookie-cutter implementation. Though, the noevelty of this has worn off in modern day if the user-case is *purely* just a chatbot with basic information.

As the industry has grown, more methods have appeared as [agentic](./agent.md) use-cases. Examples include:

- Coding
- File management
- Using the command line / terminal
- Querying & deep research of information
- Creating & implementing new web-ui designs
- Constructing slideshows
- Visualizing information (via mermaid diagrams or ascii)
- Documenting a codebase
- Delegating communications via slack/email based on previous, chained actions
- Browser automation
- Creating, describing, and reviewing PRs
- Repetitive tasks
- Creating new tasks for kanban or scrum, based on contextual info
- Assist the human in learning something new!
- Chaining & delegating any of the above, in any order, to create one large custom macro

Non-agentic use-cases may include:

- helping to remember a word you might have forgotten (e.g what is that one word that means the affirmation of a statement? ["yes"] )
- Assist in fixing grammar and punctuation
- General conversation (They should not be a human replacment!)
- Translating a message from one language to another
- OCR Capabilities - reading text off paper and using that for other use-cases
- Formatting text into a markdown table or different format all together
- Roleplay - simulate a social scenario you might encounter in real life
- Food Recipes

---

In general, it's when LLMs are combined with real resources & information, that they are able to accomplish real things. The more context is gathered & balanced out, the more efficient it will become at an ambiugous task

"Balancing out" is vague, but intentional. You can either provide too little context, or too much. *The model* might be able to handle X amount of context, while another could handle y. Figuring this out depends on many things, such as the model itself, the context (some context might behave better or worse for a model), the [harness](./harness.md), etc.

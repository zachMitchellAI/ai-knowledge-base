# Harness

A harness is a single unit of, or a collection of: Large Language Model Context, in order for said model to perform actions in a desired style or fashion.

While simple ones can be static, harnesses can be queryable, don't all have to be in-context all at once, fluid, and dynamic. Harnesses may include information such as:

* purpose (`You are a coding assistant, named HAL`)
* intent (`Your goal is to quickly, and concisely provide coding solutions to the end-user`)
* rules (`You have access to the user's directory: (./path/to/directory), please remain within the scope of the designated path. You must not be overly-chatty, rather, responses must have intent in each line, and address each concern of the user in a balanced, thoughtful, yet non-verbose fashion.`)
* delegation (`Further instructions can be found in: (./skills/harness/README.MD), which should provide further navigation based on inferred user-intent`)

[Pseudo example]

# Use

Harnesses are important because they help regulate a model's behavior by:

* Providing examples of coding do's / dont's (e.g separation of concerns, preferred syntax)
* Explain the process of doing a coding task (e.g write code, test, verify it works)
* Provide more direct access to context (e.g more harnessing, code locations)

This concept is different from **code inferrence**, where a lanaguage model views the code, and it's patterns, in order to guess how to output new code. Code inferrence alone has issues when implementing new code. For example, the model might try to use:

```js
if(statement)
    return true
```

Instead of using the *preferred* method of:

```js
if(statement){
    return true
}
```

When for example, neither of these examples exist in the target file.

# Commands / Workflows

[Commands](./commands.md) / **Workflows** are also a harness, or at the very least harness-like. It takes the concept of a harness, and operates more like an agentic workflow. These files tell exactly what a model to do, what tools it requires for the job, and how to perform steps in order to solve a problem. *An entire* process can be created using plain english using this method. Instead of:

> Grab me a list of elements from figma

it may become:

```
This command is designed to grab components from figma.

# Process

1. Use the search tool to discover the element based on user-input following this command
2. provide resulting output in a descrete markdown table with the following columns:
    * Name (name of the element)
    * Description (What the element does)
    * Instances (The # of times this element appears in the figma page)
    * Varibles (The variables used in the tree of this element)

# You may stop when:

The amount of elements searched has reached either 20, or another ammount supplied by the user.
---
```

# Achille's heel

When done improperly, harnesses have been known to cause more problems than productive output. As of this writing it's commonly known that harnesses have accidentally been used on *the wrong model*.

* When a new model releases, and it uses a previous harness, it's output may be warped to have un-ideal output.
* Conversely, If a old model uses a new harness (made for a new model), the output quality of that model may also suffer

As such, it may be good practice to tailor a harness to specific models depending on the use-case. A general harness may be useful for a wide range of models, but if a harness gets more specific, that's when attention to detail is required.

**OpenCode** is an example of "selling a good harness". For OpenCode Zen, they talk to each vendor to figure out how to best way to treat a large language model. This allows the results to be tuned to the best of either their abilities, or quirks.

Too much of a harness may pose a risk of quality shifting, thought this depends on the model's ability to use it's context window, big or small.

# Without a harness

Models have a strong tendency to speak in strong verbosity and say everything that comes to mind. They have an "internal harness" where their training / weights attempt to prevent them from going overboard at times. Otherwise output is going to be incredibly large.

From personal experience, this behavior of verbosity will vary depending on how many parameters the model has. Gemma (M parameters), and granite models for example will be very short and concise with their outputs, while larger models will gladly output as much as they can.
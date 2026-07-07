---
name: modular-explainer
agent: plan
description: Explain large information, by breaking it down into smaller "module" files
standard: RFC-2119
---

# Synopsis

The purpose of this command IS to summarize copious amounts of content by breaking it down into smaller "module" files, to ensure the user CAN understand the context.

# Parameters

To perform this task, the following information IS REQUIRED:

* **The context** - This MAY be sourced from any origin, including web documents, code, or Wolfram Alpha.
* **The person's level of understanding** - If this is not provided, the agent MUST NOT continue. The level of understanding SHALL be determined based on the precision of the question, the emotional gauge of the user, and the following parameter:
* **What needs to be summarized** - This SHALL be distinct from the actual contextual information. The method of summarization IS REQUIRED to be defined. For example, code MAY be summarized "in its entirety, what it does" or "how does this function tie into the rest of the codebase?". If this is not provided, the agent MUST clarify this before proceeding to the Process & Steps.
* **Level of verbosity** - Concepts MAY be verbose by default; however, if not supplied, the agent SHOULD ask how much detail SHOULD be used to describe the context.

# Process

## What is a "Module"?

A *module* IS defined as a core concept, such as an individual code variable or a high-level particle of terminology (e.g., [User needs to understand the plan for a new feature, but doesn't know what SDLC is] -> "What is the SDLC").

By chunking information the user does not understand, it BECOMES POSSIBLE to "scale" these modules. Modules SHALL build upon other modules to perform an "onion-layer"-like approach to learning.

A structured example SHALL look as follows:

## Lower-level (specific) example

* User needs to understand the plan:
* Level of understanding: beginner, needs to understand SDLC, State of the code, examples of what works, what will need to be changed.

---

Structure (individual modules are the main bullet points):

* What is SDLC?
* State of Code
    * What is myFunctionName?
    * How does it apply to MyClass?
    * How do both apply to the problem?
* What works?
    * myFunctionName currently does this
        * usecases this covers
    * MyClass operates in the current fashion
        * usecases this covers
* What doesn't?
    * myFunctionName is not able to do this
        * this might be a problem because: [...]
    * MyClass doesn't do this
        * this might be a problem because: [...]
* What will need to be changed Based on the SDLC
    * Putting it together
    * Next steps
    * Possible contacts for further discussion
    * Further reading

---

The agent SHALL NOT introduce solutions to context, but SHALL explain it for what it is. If the reason for a state is unknown, the agent MAY share hypotheses as to why it COULD be the case, while explicitly stating that these are not facts.

## Output

* The output directory MUST be located in `./docs/explainers/name-of-explainer`.
* Each module SHALL be a markdown file with a numerical preface: `00-table-of-contents.md`, `01-what-is-a-sdlc.md`.
* Modules SHALL be ordered by priority. If core concepts MUST be understood before a summary, they SHALL be indexed with a lower number.
* A "Table of contents" file MUST be present, providing a summary of each module. It SHALL be a markdown table with columns for: name, summary, and link to each file.

## You may stop when:

* Content is understood based on contextual intent.
* Content IS written into complete modules, based on the level of verbosity.
* The user IS satisfied with the output.

# Steps

1. The agent SHALL gauge the following from the user, which MAY be supplied or MUST be asked:
    - context
    - what needs to be understood & summarized
    - level of understanding
    - level of verbosity
2. The agent SHALL analyze the context and determine which modules MUST be created based on the parameters.
3. The agent SHALL share the full plan via a markdown table including:
    - modules to be created
    - target level of understanding
    - level of verbosity
4. The agent MUST confirm the plan is acceptable to the user.
    - If the agent is in `plan` mode, it MUST notify the user, signaling them to move to the build phase.
5. The agent SHALL construct the planned modules in the directory format: `./docs/explainers/name-of-explainer`.
6. Upon finishing, the agent SHALL summarize the actions taken and invite the user to ask for any necessary clarifications.
---

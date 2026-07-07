---
name: rfc-2119-language
description: Convert a document into RFC-2119 language
agent: build
standard: RFC-2119
---

# Synopsis

This command transforms a body of text to conform to the [RFC-2119 standard](https://www.rfc-editor.org/rfc/rfc2119.txt). RFC-2119 defines terms used to specify requirements in technical documents, ensuring absolute and unambiguous language for specifications or LLM instructions.

# Parameters

* **Context** - The body of text provided by the user, sourced from direct input, the internet, or the filesystem.

# Steps

1. Analyze the provided text to determine its purpose and intended outcome.
2. If the input originates from a file on disk, the agent MUST create a backup copy of the original file (e.g., `original-file.bak.md`) before replacing the original file with the transformed text.
3. Rewrite the context using RFC-2119 terminology (e.g., MUST, MUST NOT, REQUIRED, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, MAY, CAN, OPTIONAL).
4. If the input does not originate from the filesystem, the agent SHALL print the transformed text as the output.
5. The agent SHOULD prompt the user to verify if any further adjustments are required.

---

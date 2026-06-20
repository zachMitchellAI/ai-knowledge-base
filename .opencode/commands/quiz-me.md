---
description: Creates a quiz from any given context! Presents it in multiple choice format
agent: plan
---

# Quiz me

The purpose of this command is to provide a series of multiple choice questions based on the context provided. This is done to provide an interactive learning method, allowing the user to parse and comprehend the content rather than just reading it.

# Parameters

A reference to the content, either by link, reference to an on-device file, or the content pasted after the command

# Steps

* Using the `qusetion` tool, present three questions to the user about the content. Each quetion has four different possible responses. Users are allowed to ask about a question to help better guage it.
* When the finishes responding, indicate if answers were correct or incorrect
* present the answers and explain the reasoning for why it is the correct answer

## Tailored qusetions

Given the correctness of the last few questions, take one of the following routes:

* If the user doesn't fully understand the previous questions (e.g they got close or the answer was incorrect), help them to understand the topic better by presenting new, related questions
* If the user got the question rights, move on to a unique question

---

Repeat sending questions in this style until the user chooses to skip the question (in other words they've wrapped up)

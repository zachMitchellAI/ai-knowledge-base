---
name: sort-inbox
description: View the contents of a cluttered inbox and sort them out into folders (thunderbird)
---

# Synopsis

This command is designed to sort out a cluttered inbox. There will be many different emails that can be sorted out into sub-folders

Each subfolder will be under the `Inbox` folder. They will have pre-set names which should correlate to relate to themes the email may convey

# Parameters

The mailbox that should be sorted out

# Steps

This is a **recursive subagent** task. This means that context MUST be delegated over to subagents each time a portion of the task is accomplished.

Before delegating, Identify the inbox sub-folder names. In the message to subagents they MUST be told not to create new subfolders.

## For each subagent [one subagent only runs at a time]:

1. View the headers of *all* inbox messages. It should include the subject, who it's from, etc. The actual contents of the message doesn't have to be gathered
2. Based on the list of sub-folders, Identify where each messages should go
3. Use the *bulk* parameter in the move tool to move many messages at once into a sub-folder
4. Keep moving messages until all messsages are no longer in the inbox
5. Report how many messages are left in the inbox, and if there are messages left that don't fit into any category

## After the subagent runs

1. Confirm the subagent was correct for how many messages are left
2. If they were not correct, delegate another subagent to perform the exact same task as the previous one.
3. Repeat this process of checking, and delegating subagents until the inbox is clean

## If a subagnet reports a message that doesn't fit into a subfolder

Prompt the user if they would like a new category created based generally on what the message subject is about! If so, there is permission to create a new one from scratch.

# You may stop when:

* Inbox is empty!

---
name: md-to-tts-stripped
description: convert a corpus of markdown text into text that's easy for a TTS to interpret
---

# Synopsis

Files received by LLMs most commonly use markdown, a readable, human friendly markup language that can be formatted to be viewed nicely on most machines. For a text to speech though, it's not as ideal

This skill receives context from the user, and changes it into a TTS readable format.

# Steps

1. Read the context, file, or corpus the user provides. The remaining are directions specifically for markdown
2. Strip *all* hashes that create subheaders (`#`) Replace with - `:`
	- E.G: "# My Header" -> "My Header:"
3. Remove all asterisks for bold/italics. Depending on context, use a comma `,` in place of bolded or italics to pause for emphasis.
4. Strip links entirely, replace content with `(link)`
	- e.g: "https://example.com" -> "(link)"
5. Replace unordered lists, with lists containing commas

e.g:

```md
* item 1
* item 2
* item 3
```

Replaced with:

```
item 1, item 2, item 3
```

6. Replace ordered lists, with numerical numbers, followed by a colon, then a comma

e.g:

```md
1. first item
2. second item
3. third item
```

Replaced with:

```
1: first item, 2: second item, 3: third item.
```

7. Tables must be entirely verbalized. It must go left-to-right, stating the column name, and value each time, until the row is complete

e.g:

```md
|name|age|
|--------|
|Zach|28 |
|John|30 |
```

Replaced with:

```
Name: Zach, Age: 28.
Name: John, Age: 30.
```


8. Line breaks must be stripped
9. The entire corpus may be chunked into paragarphs that are reasonable, based on sentence count and thought chunking.

# Output

Once finished, agents must output their file into the same path unless otherwise specified. The file itself should have the suffix `_tts.md`. For example if the input file was `research.md` - the output should by default be in the same directory and be named: `research_tts.md`

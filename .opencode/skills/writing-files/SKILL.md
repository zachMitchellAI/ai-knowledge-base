---
name: writing-files
description: Assists nemotron with writing files when something goes wrong
---
# Writing files

**Applies to**: nemotron models

The `write` tool requires that input MUST be a string. It MUST NOT be an array or object. Implementers SHALL ensure before doing any file writing, that this format is used, in order to produce adequate outputs for files.

## Context for why

It has been discovered that when JSON, JS, TypeScript, MarkDown, syntax (or other related syntax) is used, the output from the write tool SHALL become corrupted, and proceeds to generate output on a single line that is NOT usable.

## Your past-self wrote this:

> The write tool expects a string for the content parameter, not an array or object. Here's the exact format from the tool definition:

```json
{
  "filePath": "/absolute/path/to/file.js",
  "content": "your file content as a plain string"
}
```

> The issue is I passed an array/object ([{...}]) instead of a plain string. 

## Critical Rules

### ✅ CORRECT - Pass content as a plain string
```json
{
  "filePath": "/path/to/file.ts",
  "content": "import React from 'react';\n\nexport function MyComponent() {\n  return <div>Hello World</div>;\n}"
}
```

### ❌ WRONG - Passing JSON/array/object (causes corruption)
```json
{
  "filePath": "/path/to/file.ts",
  "content": [{
    "import": "React",
    "from": "react"
  }]
}
```

### ❌ WRONG - Passing markdown code block syntax as content
```json
{
  "filePath": "/path/to/file.ts",
  "content": "```typescript\nimport React from 'react';\nexport function MyComponent() {\n  return <div>Hello World</div>;\n}\n```"
}
```

## Common Mistakes to Avoid

1. **Never wrap content in arrays**: `[{...}]`, `["line1", "line2"]`
2. **Never wrap content in objects**: `{"code": "..."}`
3. **Never include markdown fences**: \`\`\`typescript ... \`\`\`
4. **Never use JSON.stringify()** on the content
5. **Always escape newlines** as `\n` in the JSON payload, not literal newlines

## Proper Format Examples

### TypeScript/React Component
```json
{
  "filePath": "/src/components/Button.tsx",
  "content": "import React from 'react';\n\ninterface ButtonProps {\n  onClick: () => void;\n  children: React.ReactNode;\n}\n\nexport function Button({ onClick, children }: ButtonProps) {\n  return (\n    <button onClick={onClick}>\n      {children}\n    </button>\n  );\n}"
}
```

### Plain Text / Config File
```json
{
  "filePath": "/config/settings.json",
  "content": "{\n  \"apiUrl\": \"https://api.example.com\",\n  \"timeout\": 5000\n}"
}
```

### Markdown File
```json
{
  "filePath": "/docs/guide.md",
  "content": "# Guide\n\nThis is a **markdown** file.\n\n## Section\n\n- Item 1\n- Item 2"
}
```

## Quick Checklist Before Writing
- [ ] Content is a single string (not array/object)
- [ ] No markdown code fences (\`\`\`)
- [ ] Newlines are `\n` in the JSON
- [ ] Quotes inside content are escaped (`\"`)
- [ ] File path is absolute

---

**Remember**: The tool receives your JSON, parses it, and passes the `content` string directly to the filesystem. Any non-string content will be corrupted.
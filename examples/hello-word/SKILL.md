---
name: hello-world
description: >-
  Prints a greeting in a fixed format. Use when the user asks for hello world,
  a greeting demo, or wants to try a minimal Agent skill.
disable-model-invocation: true
---

# Hello World

## Instructions

When this skill is invoked:

1. Reply with exactly one greeting line.
2. Use this format (replace `{name}` only if the user gave a name; otherwise use `World`):

```text
Hello, {name}!
```

3. Do not add extra commentary, lists, or follow-up questions unless the user asked for more.

## Examples

**User:** hello world  
**Agent:** Hello, World!

**User:** hello runoops  
**Agent:** Hello, runoops!

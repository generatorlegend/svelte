---
title: Working with TypeScript in Svelte
---

# Working with TypeScript in Svelte

Svelte supports TypeScript out of the box, allowing you to enhance your development experience with static typing. This guide will walk you through setting up a Svelte project with TypeScript, writing components using TypeScript, and understanding how the Svelte compiler handles TypeScript code.

## Setting up a Svelte project with TypeScript

To start a new Svelte project with TypeScript:

1. Create a new Svelte project using the template:
   ```bash
   npx degit sveltejs/template svelte-typescript-app
   cd svelte-typescript-app
   ```

2. Add TypeScript support:
   ```bash
   node scripts/setupTypeScript.js
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

## Writing Svelte components with TypeScript

To use TypeScript in your Svelte components, simply add the `lang="ts"` attribute to your `<script>` tags:

```svelte
<script lang="ts">
  let count: number = 0;

  function increment(): void {
    count += 1;
  }
</script>

<button on:click={increment}>
  Clicks: {count}
</button>
```

## How Svelte compiler handles TypeScript

The Svelte compiler has built-in support for TypeScript. When compiling your Svelte components, it performs the following steps:

1. Parses the component source code.
2. If TypeScript is detected, it removes TypeScript-specific nodes from the AST (Abstract Syntax Tree).
3. Analyzes the component structure.
4. Transforms the component for output.

Here's a simplified overview of how the compiler processes TypeScript code:

```javascript
// From packages/svelte/src/compiler/index.js
if (parsed.metadata.ts) {
  parsed = {
    ...parsed,
    fragment: parsed.fragment && remove_typescript_nodes(parsed.fragment),
    instance: parsed.instance && remove_typescript_nodes(parsed.instance),
    module: parsed.module && remove_typescript_nodes(parsed.module)
  };
}
```

The `remove_typescript_nodes` function strips out TypeScript-specific syntax, allowing the rest of the compilation process to work with standard JavaScript.

## Type checking in Svelte files

To enable type checking in your `.svelte` files, you need to add a special comment at the top of your component file:

```svelte
<!-- src/App.svelte -->
<script lang="ts">
// @ts-check
// ...
</script>
```

This comment tells TypeScript to check the types in this file.

## Using TypeScript with Svelte's template syntax

Svelte's template syntax also supports TypeScript for better type inference:

```svelte
<script lang="ts">
  let items: string[] = ['apple', 'banana', 'cherry'];
</script>

{#each items as item}
  <p>{item}</p>
{/each}
```

## Best practices

1. Use TypeScript for complex components or when working on larger projects.
2. Leverage TypeScript's interface and type alias features for props and events.
3. Use the `$: ` reactive declarations with TypeScript for better type inference.
4. Utilize TypeScript's enums for managing state machines or sets of constants.

By following these guidelines and understanding how Svelte works with TypeScript, you can create more robust and maintainable Svelte applications.
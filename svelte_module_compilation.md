# Svelte Module Compilation

## Introduction

Svelte 5 introduces a new feature called "runes" that allows you to write JavaScript modules with Svelte-specific functionality. This document explains how to compile Svelte modules, including the use of runes, and provides examples of how to write and use Svelte modules effectively in your applications.

## Compiling Svelte Modules

To compile a Svelte module, you can use the `compileModule` function from the Svelte compiler. This function takes your JavaScript source code containing runes and transforms it into a standard JavaScript module.

### API

```javascript
function compileModule(source: string, options: ModuleCompileOptions): CompileResult
```

- `source`: The JavaScript source code containing runes.
- `options`: Compilation options (see below for details).
- Returns: A `CompileResult` object containing the compiled code and other metadata.

### Compilation Options

The `ModuleCompileOptions` object can include the following properties:

- `filename`: (optional) The name of the file being compiled.
- `name`: (optional) The name of the component (if applicable).
- `format`: The output format (e.g., 'esm' for ECMAScript modules).
- `generate`: (optional) Whether to generate code or just perform validation.

## Writing Svelte Modules with Runes

Runes are special markers in your JavaScript code that the Svelte compiler recognizes and transforms. They allow you to use Svelte's reactivity system and other features directly in JavaScript modules.

### Example: Basic Svelte Module with Runes

```javascript
import { $state } from 'svelte';

export function createCounter() {
  let count = $state(0);

  function increment() {
    count++;
  }

  return {
    get count() {
      return count;
    },
    increment
  };
}
```

In this example, we use the `$state` rune to create a reactive state variable `count`. The `createCounter` function returns an object with a getter for `count` and an `increment` method that updates the state.

## Using Compiled Svelte Modules

After compilation, you can import and use the Svelte module in your application like any other JavaScript module.

### Example: Using a Compiled Svelte Module

```javascript
import { createCounter } from './counter.js';

const counter = createCounter();
console.log(counter.count); // 0
counter.increment();
console.log(counter.count); // 1
```

## Best Practices

1. Keep your Svelte modules focused on specific functionality.
2. Use runes judiciously to create reactive state and computed values.
3. Export functions or objects that encapsulate the module's behavior.
4. Consider using TypeScript for better type checking and editor support.

## Conclusion

Svelte module compilation with runes provides a powerful way to create reusable, reactive logic outside of Svelte components. By understanding how to write and compile these modules, you can build more modular and maintainable Svelte applications.

For more information on specific runes and their usage, refer to the Svelte documentation on runes.
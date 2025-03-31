# Svelte Compiler Options

This guide provides a comprehensive overview of the available compiler options in Svelte, explaining their purpose, default values, and how they affect the compilation process.

## Table of Contents

1. [Introduction](#introduction)
2. [Basic Options](#basic-options)
3. [Advanced Options](#advanced-options)
4. [Custom Element Options](#custom-element-options)
5. [TypeScript-related Options](#typescript-related-options)
6. [Examples](#examples)

## Introduction

The Svelte compiler converts your `.svelte` source code into a JavaScript module that exports a component. The `compile` function in the Svelte compiler accepts various options to customize the compilation process. These options allow you to fine-tune the output, enable or disable certain features, and control how your Svelte components are processed.

## Basic Options

### `filename`

- Type: `string`
- Default: `'(unknown)'`

Specifies the filename of the component being compiled. This is used for debugging and error reporting purposes.

```javascript
const result = svelte.compile(source, {
  filename: 'MyComponent.svelte'
});
```

### `name`

- Type: `string`
- Default: `'Component'`

Sets the name of the compiled component. This is used when creating a custom element.

```javascript
const result = svelte.compile(source, {
  name: 'MyCustomComponent'
});
```

### `format`

- Type: `'esm' | 'cjs'`
- Default: `'esm'`

Specifies the output format of the compiled component. Use `'esm'` for ECMAScript modules or `'cjs'` for CommonJS.

```javascript
const result = svelte.compile(source, {
  format: 'cjs'
});
```

## Advanced Options

### `generate`

- Type: `'dom' | 'ssr' | false`
- Default: `'dom'`

Determines the type of output to generate. Use `'dom'` for client-side rendering, `'ssr'` for server-side rendering, or `false` to skip code generation (useful when you only need the AST or metadata).

```javascript
const result = svelte.compile(source, {
  generate: 'ssr'
});
```

### `dev`

- Type: `boolean`
- Default: `false`

When set to `true`, the compiler will include additional debugging information in the compiled output. This is useful during development but should be set to `false` for production builds.

```javascript
const result = svelte.compile(source, {
  dev: true
});
```

### `css`

- Type: `boolean`
- Default: `true`

Controls whether to include styles in the JavaScript class or as a separate CSS file. Set to `false` to emit styles as a separate static `.css` file.

```javascript
const result = svelte.compile(source, {
  css: false
});
```

## Custom Element Options

### `customElement`

- Type: `boolean | { tag: string }`
- Default: `false`

Enables compilation as a custom element (web component). When set to `true`, the compiler will use the `name` option or the component's filename to determine the custom element's tag name. Alternatively, you can specify a custom tag name by passing an object with a `tag` property.

```javascript
const result = svelte.compile(source, {
  customElement: true
});

// Or with a custom tag name
const result = svelte.compile(source, {
  customElement: { tag: 'my-component' }
});
```

## TypeScript-related Options

### `enableSourcemap`

- Type: `boolean`
- Default: `true`

Determines whether to generate sourcemaps for the compiled output. This is particularly useful when working with TypeScript or when debugging compiled Svelte components.

```javascript
const result = svelte.compile(source, {
  enableSourcemap: false
});
```

## Examples

### Basic Component Compilation

```javascript
import * as svelte from 'svelte/compiler';

const source = `
  <script>
    let count = 0;
    function increment() {
      count += 1;
    }
  </script>

  <button on:click={increment}>
    Clicks: {count}
  </button>
`;

const result = svelte.compile(source, {
  filename: 'Counter.svelte',
  name: 'Counter',
  format: 'esm',
  dev: true
});

console.log(result.js.code); // Compiled JavaScript code
console.log(result.css.code); // Compiled CSS code
```

### Server-Side Rendering (SSR) Compilation

```javascript
import * as svelte from 'svelte/compiler';

const source = `
  <script>
    export let name;
  </script>

  <h1>Hello, {name}!</h1>
`;

const result = svelte.compile(source, {
  filename: 'Greeting.svelte',
  generate: 'ssr',
  format: 'cjs'
});

console.log(result.js.code); // SSR-compatible JavaScript code
```

### Custom Element Compilation

```javascript
import * as svelte from 'svelte/compiler';

const source = `
  <script>
    export let color = 'blue';
  </script>

  <style>
    button {
      background-color: var(--color);
    }
  </style>

  <button style="--color: {color}">
    <slot></slot>
  </button>
`;

const result = svelte.compile(source, {
  filename: 'ColorButton.svelte',
  customElement: { tag: 'color-button' },
  css: false
});

console.log(result.js.code); // Custom element JavaScript code
console.log(result.css.code); // Separate CSS code
```

By utilizing these compiler options, you can tailor the Svelte compilation process to suit your specific needs, whether you're building traditional web applications, server-rendered sites, or web components.
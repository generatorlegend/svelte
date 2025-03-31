---
title: Understanding Svelte Compiler Warnings
---

# Understanding Svelte Compiler Warnings

When working with Svelte, you may encounter various compiler warnings. These warnings are designed to help you write better, more efficient Svelte code. This guide will help you understand common warnings, their meanings, and how to resolve them.

## Common Svelte Compiler Warnings

### 1. Unused CSS selector

**Warning message:** Unused CSS selector

**Meaning:** This warning occurs when you have a CSS selector in your component's `<style>` block that doesn't match any elements in your component's markup.

**How to resolve:** 
- Remove the unused CSS selector
- Ensure that the selector correctly targets the intended elements in your component

**Example:**
```svelte
<script>
  // Component logic
</script>

<div class="container">
  <h1>Hello, Svelte!</h1>
</div>

<style>
  .container {
    background-color: #f0f0f0;
  }
  .unused-class { /* This will trigger a warning */
    color: red;
  }
</style>
```

### 2. A11y: Avoid using autofocus

**Warning message:** A11y: Avoid using autofocus

**Meaning:** This accessibility warning suggests avoiding the use of the `autofocus` attribute, as it can be disorienting for users, especially those using screen readers.

**How to resolve:** 
- Remove the `autofocus` attribute
- Consider alternative ways to draw attention to the element, such as using ARIA attributes or focus management in JavaScript

**Example:**
```svelte
<!-- Instead of this: -->
<input autofocus>

<!-- Consider this: -->
<input>
<!-- And use JavaScript to focus the input if necessary -->
```

### 3. Reactive statement has no dependencies

**Warning message:** Reactive statement has no dependencies

**Meaning:** This warning occurs when you have a `$:` reactive statement that doesn't depend on any reactive values.

**How to resolve:** 
- Add dependencies to the reactive statement
- If the statement doesn't need to be reactive, convert it to a regular statement

**Example:**
```svelte
<script>
  let count = 0;

  // This will trigger a warning
  $: console.log('This statement has no dependencies');

  // Correct usage
  $: console.log('Count is now:', count);
</script>
```

### 4. Component has unused export

**Warning message:** Component has unused export

**Meaning:** This warning indicates that your component has an exported variable that isn't being used by its parent component.

**How to resolve:** 
- Remove the unused export
- Use the exported variable in the parent component

**Example:**
```svelte
<!-- ChildComponent.svelte -->
<script>
  export let usedProp = 'default';
  export let unusedProp = 'unused'; // This will trigger a warning
</script>

<!-- ParentComponent.svelte -->
<script>
  import ChildComponent from './ChildComponent.svelte';
</script>

<ChildComponent usedProp="value" />
```

## Best Practices for Avoiding Warnings

1. Regularly review and clean up your component's styles, removing any unused selectors.
2. Be mindful of accessibility concerns and avoid using attributes like `autofocus` unless absolutely necessary.
3. Ensure all reactive statements have appropriate dependencies.
4. Only export variables that are actually used by parent components.
5. Use TypeScript or JSDoc comments to improve type checking and catch potential issues early.
6. Regularly update your Svelte version to benefit from the latest optimizations and warning detections.

By following these best practices and addressing warnings promptly, you can improve the quality and maintainability of your Svelte code.

Remember that while warnings are important to address, they don't prevent your code from compiling. However, resolving them can lead to better performance, accessibility, and overall code quality.
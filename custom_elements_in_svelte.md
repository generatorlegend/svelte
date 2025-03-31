---
title: Custom Elements in Svelte
---

# Custom Elements in Svelte

Svelte provides support for creating and using custom elements (also known as Web Components) in your applications. This guide will walk you through the process of creating custom elements using Svelte and how to use them in your projects.

## Creating Custom Elements

To create a custom element using Svelte, you need to use the `customElement` compiler option. This option allows you to define a Svelte component as a custom element that can be used in any HTML page, regardless of whether it's a Svelte application or not.

### Using the `customElement` Option

When compiling your Svelte component, you can specify the `customElement` option in the component's `<svelte:options>` tag or in the compiler options.

#### In-component Declaration

```svelte
<svelte:options customElement="my-element" />

<script>
  export let name = 'World';
</script>

<h1>Hello {name}!</h1>
```

#### Compiler Option

When using the Svelte compiler programmatically, you can pass the `customElement` option like this:

```javascript
import { compile } from 'svelte/compiler';

const result = compile(source, {
  customElement: true
});
```

Or, for more control:

```javascript
import { compile } from 'svelte/compiler';

const result = compile(source, {
  customElement: {
    tag: 'my-element'
  }
});
```

## How Custom Elements Affect Compilation

When you use the `customElement` option, the Svelte compiler generates JavaScript that extends the `HTMLElement` class instead of creating a regular Svelte component. This allows the component to be used as a custom element in any HTML context.

The compiled output will include:

1. A class that extends `HTMLElement`
2. Custom element registration using `customElements.define()`
3. Shadow DOM initialization
4. Attribute observation for props

## Using Custom Elements

Once your Svelte component is compiled as a custom element, you can use it in your HTML like any other HTML element:

```html
<my-element name="Svelte"></my-element>
```

### In Svelte Applications

You can also use custom elements within Svelte applications. However, keep in mind that they will behave like regular HTML elements rather than Svelte components. This means:

- You use attribute syntax instead of property syntax for passing data
- Events are listened to using `addEventListener` or `on:event` syntax

Example usage in a Svelte component:

```svelte
<script>
  import './MyElement.svelte';  // Make sure the custom element is registered
  let name = 'Svelte';
</script>

<my-element name={name}></my-element>
```

## Best Practices and Considerations

1. **Naming**: Custom element names must contain a hyphen (-) to avoid conflicts with existing HTML elements.

2. **Props and Attributes**: Remember that custom element attributes are always strings. If you need to pass complex data, consider using properties instead.

3. **Styling**: Styles defined in your Svelte component will be scoped to the shadow DOM of the custom element.

4. **Events**: Custom events can be dispatched using the `CustomEvent` API.

5. **Lifecycle**: Custom elements have their own lifecycle methods like `connectedCallback` and `disconnectedCallback`. These can be implemented in your Svelte component using the `onMount` and `onDestroy` lifecycle functions.

## Conclusion

Custom elements provide a powerful way to create reusable components that can work across different frameworks or in vanilla HTML/JavaScript applications. By leveraging Svelte's `customElement` option, you can create efficient and easy-to-use custom elements while taking advantage of Svelte's intuitive syntax and powerful features.

Remember to consider the trade-offs between using custom elements and regular Svelte components, and choose the approach that best fits your project's needs.
# svelte-scrollto-next

Animating vertical and horizontal scrolling in Svelte.

**NOTE:**

This is a fork of [svelte-scrollto][svelte-scrollto],
which has been archived. Changes are:

- Set `{ type: 'module' }` in `package.json`.
- File extensions added to extension-less relative imports.
- Set `touchstart` events to `passive` as per Lighthouse.
- Updated to Svelte 4

**Future?:**

- Typescript
- Tests
- Other Modernizations

## Install

```bash
npm install --save-dev svelte-scrollto-next
```

## Usage

```html
<script>
  import * as animateScroll from "svelte-scrollto-next";
</script>

<a on:click={() => animateScroll.scrollToBottom()}> Scroll to bottom </a>
<a on:click={() => animateScroll.scrollToTop()}> Scroll to top </a>
<a on:click={() => animateScroll.scrollTo({element: 'scroll-to-element-selector'})}> Scroll to element </a>
<a on:click={() => animateScroll.scrollTo({element: 'scroll-to-element-selector', offset: 200})}> Scroll to below element 200px </a>
<a on:click={() => animateScroll.scrollTo({element: 'scroll-to-element-selector', duration: 2000})}> Scroll to element over 2000ms </a>
```

Using as a action:

```html
<script>
  import { scrollto } from "svelte-scrollto-next";
</script>
<!-- Parameter is element selector or options -->
<a use:scrollto={'#scroll-element'}> Scroll to element </a>
```

## API

### Global Options

|    Option    | Required |                                         Default value                                          |                                                                                   Description                                                                                   |
| :----------: | :------: | :--------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| `container`  |    ✔     |                                            `"body"`                                            |                                                                                Scroll container                                                                                 |
|  `duration`  |    ✔     |                                             `500`                                              |                                                           The duration (in milliseconds) of the scrolling animation.                                                            |
|   `delay`    |          |                                              `0`                                               |
|   `offset`   |          |                                              `0`                                               |                                            The offset that should be applied when scrolling. This option accepts a callback function                                            |
|   `easing`   |          | [`cubicInOut`](https://github.com/sveltejs/svelte/blob/master/src/runtime/easing/index.ts#L67) |        The easing function to be used when animating. Can pass any easing from [`svelte/easing`](https://svelte.dev/docs#svelte_easing) or pass custom easing function.         |
|  `onStart`   |          |                                             `noop`                                             |                        A callback function that should be called when scrolling has started. Receives the target element and page offset as a parameter.                        |
|   `onDone`   |          |                                             `noop`                                             |                         A callback function that should be called when scrolling has ended. Receives the target element and page offset as a parameter.                         |
| `onAborting` |          |                                             `noop`                                             | A callback function that should be called when scrolling has been aborted by the user (user scrolled, clicked etc.). Receives the target element and page offset as parameters. |
|  `scrollX`   |          |                                            `false`                                             |                                                                Whether or not we want scrolling on the `x` axis                                                                 |
|  `scrollY`   |          |                                             `true`                                             |                                                                Whether or not we want scrolling on the `y` axis                                                                 |

Override global options:

```javascript
import * as animateScroll from 'svelte-scrollto-next'

animateScroll.setGlobalOptions({
  offset: 200,
  onStart: (element, offset) => {
    if (element) {
      console.log('Start scrolling to element:', element)
    } else if (offset) {
      console.log('Start scrolling to page offset: (${offset.x}, ${offset.y})')
    }
  },
})
```

### Functions

#### `scrollTo(options)`

Accepts all global options and:

- `element`: The element you want scroll to
- `x`: The offset we want to scrolling on the x axis
- `y`: The offset we want to scrolling on the y axis

#### `scrollToTop(options)`

Shortcut of use scrollTo with `x` equal to `0`.

#### `scrollToBottom(options)`

Shortcut of use scrollTo with `x` equal to _`containerHeight`_

### Actions

Svelte action that listens for `click` (`touchstart`) events and scrolls to
elements with animation.

- `scrollto`

- `scrolltotop`

- `scrolltobottom`

### Troubleshooting

If you want to use Lazy and want to scroll to elements, you need to give your
lazy components (images, v.v..) fixed dimensions, so the browser known the
size of the not loaded elements before scrolling.

### License

[MIT][mit-license]

Copyright (c) 2019-2021 [langbamit][langbamit] (original author).

[easing]: https://github.com/sveltejs/svelte/blob/master/src/runtime/easing/index.ts
[langbamit]: https://github.com/langbamit
[mit-license]: https://mit-license.org/
[svelte-scrollto]: https://github.com/langbamit/svelte-scrollto

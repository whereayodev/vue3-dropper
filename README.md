# Currently in development stage

## How to use:

1. Import component and styles

```js
import { DropDown } from 'vue3-dropper';
import 'vue3-dropper/dist/base.css';
```

2. Insert DropDown component

```vue
<DropDown :bottom="true" :label="Label" theme="auto">
    <span>any tag item</span>
    <a>any tag item</a>
</DropDown>
```

3. ✨ You got it!

## Props

### The dropper component accepts the following props:

 - `label` (required): The label to be displayed on the button that toggles the dropdown.
 - `top` (optional): A boolean value indicating whether the dropdown should appear on top of the button. Default value is false.
 - `bottom` (optional): A boolean value indicating whether the dropdown should appear below the button. Default value is false.
 - `width` (optional): A string representing the width of the component. This can be any valid CSS width value. Default value is undefined.
 - `theme` (optional): A string indicating the theme of the component. Possible values are 'dark', 'light', or 'auto'. Default value is 'dark'.

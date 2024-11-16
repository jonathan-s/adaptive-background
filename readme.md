## Adaptive background

A JavaScript script to analyze the dominant color of an image and apply it to the background of its parent element, with various customization options.

This script is an adaption of [jquery.adaptive-backgrounds.js](https://github.com/briangonzalez/jquery.adaptive-backgrounds.js/) and removes the necessity of jquery. This script is purely using vanilla javascript.

### Installation

Simply include the script in your HTML file:

```html
<script src="path/to/your/script.js"></script>
```

### Usage

Ensure that the elements you want to process have the appropriate `data-ab` attributes.

```html
<img src="path/to/image.jpg" data-ab>
```

### Options

Customize the behavior of the script using `data-ab-*` attributes:

- `data-ab-normalize-textcolor`: Normalize text color based on the background color.
- `data-ab-normalized-light`: Custom light text color.
- `data-ab-normalized-dark`: Custom dark text color.
- `data-ab-shade-percentage`: Percentage to shade the background color.
- `data-ab-shade-variation`: Enable or disable shade variation.
- `data-ab-shade-dark`: Custom dark shade color.
- `data-ab-shade-light`: Custom light shade color.
- `data-ab-transparent`: Set transparency for the background color.

### Example

```html
<img src="path/to/image.jpg" data-ab
     data-ab-normalize-textcolor="true"
     data-ab-normalized-light="#fff"
     data-ab-normalized-dark="#000"
     data-ab-shade-percentage="0.5"
     data-ab-shade-variation="true"
     data-ab-shade-dark="rgb(0,0,0)"
     data-ab-shade-light="rgb(255,255,255)"
     data-ab-transparent="0.5">
```

Moreover the CSS class `ab-transition` can be used to customize the transition of the background so it isn't abrupt.

### Events

- `ab-color-found`: Is an event that is triggered when the dominant color is found. The event detail includes:
  - `color`: The dominant color.
  - `palette`: The color palette.
  - `normalizeTextColor`: Whether to normalize text color.
  - `normalizedTextColors`: The light and dark text colors.
  - `shadeVariation`: Whether shade variation is enabled.
  - `shadePercentage`: The shade percentage.
  - `shadeColors`: The light and dark shade colors.
  - `transparent`: The transparency level.

#### Example:

```javascript
document.querySelector('img[data-ab]').addEventListener('ab-color-found', (ev) => {
  const data = ev.detail;
  console.log('Dominant Color:', data.color);
  console.log('Color Palette:', data.palette);
});
```

### Methods

- `shadeRGBColor(color, percent)`: Shades an RGB color by a percentage.
- `blendRGBColors(color1, color2, percentage)`: Blends two RGB colors by a percentage.
- `getYIQ(color)`: Calculates the YIQ value of a color to determine brightness.

### Defaults

The script uses the following default settings:

```javascript
const DEFAULTS = {
  selector: '[data-ab]',
  parent: null,
  exclude: ['rgb(0,0,0)', 'rgb(255,255,255)'],
  shadeVariation: false,
  shadePercentage: 0,
  shadeColors: {
    light: 'rgb(255,255,255)',
    dark: 'rgb(0,0,0)'
  },
  normalizeTextColor: true,
  normalizedTextColors: {
    light: "#fff",
    dark: "#000"
  },
  lumaClasses: {
    light: "ab-light",
    dark: "ab-dark"
  },
  transparent: null
};
```

### License

MIT License.

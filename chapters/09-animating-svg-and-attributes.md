# 09. Animating SVG and attributes

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Animating CSS and transforms](./08-animating-css-and-transforms.md) | [Notes index](../README.md) | [Next: ScrollTrigger foundations](./10-scrolltrigger-foundations.md) |

## Animate inline SVG elements

GSAP can target SVG elements with selectors just like HTML elements. Keep the SVG's viewBox coordinate system explicit so shapes scale predictably.

~~~html
<svg viewBox="0 0 160 80" role="img" aria-labelledby="diagram-title">
  <title id="diagram-title">Circle moving along a path</title>
  <path d="M10 40 H150" stroke="#888" stroke-width="2" />
  <circle class="moving-dot" cx="10" cy="40" r="8" fill="#e85b24" />
</svg>
~~~

~~~js
gsap.to(".moving-dot", {
  x: 140,
  duration: 0.7,
  ease: "power2.inOut",
});
~~~

GSAP applies SVG-aware transform handling. Transform shortcuts such as x, y, rotation, and scale can move or turn a shape without manually editing the SVG transform string.

## Animate SVG attributes

Use the attr property for SVG attributes such as cx, cy, r, and viewBox-related coordinates.

~~~js
gsap.to(".moving-dot", {
  attr: { cx: 150, r: 12 },
  duration: 0.5,
});
~~~

CSS properties and SVG attributes are different. A property such as opacity can be animated as a normal tween value; geometric attributes belong under attr when the SVG attribute itself should change.

## Draw a path with DrawSVGPlugin

DrawSVGPlugin animates which portion of an SVG stroke is visible. In current GSAP releases it can be imported from the package and registered like other plugins.

~~~js
import { gsap } from "gsap";
import { DrawSVGPlugin } from "gsap/DrawSVGPlugin";

gsap.registerPlugin(DrawSVGPlugin);

gsap.set(".check-path", { drawSVG: "0%" });
gsap.to(".check-path", {
  drawSVG: "100%",
  duration: 0.65,
  ease: "power1.inOut",
});
~~~

The SVG path needs a visible stroke. A path with only a fill does not show the same line-drawing effect.

~~~html
<svg viewBox="0 0 48 48" aria-hidden="true">
  <path
    class="check-path"
    d="M8 25 L19 36 L40 11"
    fill="none"
    stroke="#e85b24"
    stroke-width="4"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>
~~~

For simple SVG movement, use core GSAP features first. Add DrawSVGPlugin only when revealing part of a path is the effect the interface needs.

## Keep SVG meaning available

Give an informative SVG an accessible name using a title or suitable ARIA label. Mark a decorative SVG aria-hidden="true". Do not use animation as the only signal that a value changed or an action succeeded.

## Practice questions

1. How can GSAP select an inline SVG element?
2. What does viewBox define?
3. Which transform shortcuts can move or rotate an SVG shape?
4. When should an SVG attribute be placed under attr?
5. Which plugin can reveal part of an SVG stroke?
6. What should an SVG path have for a line-drawing effect?
7. How should an informative SVG be named for assistive technology?
8. When should an optional SVG plugin be added?

## Main references

- [GSAP SVG](https://gsap.com/resources/svg/)
- [CSSPlugin and SVG transforms](https://gsap.com/docs/v3/GSAP/CorePlugins/CSS/)
- [AttrPlugin](https://gsap.com/docs/v3/Plugins/AttrPlugin/)
- [DrawSVGPlugin](https://gsap.com/docs/v3/Plugins/DrawSVGPlugin/)
- [Plugin registration](https://gsap.com/docs/v3/GSAP/gsap.registerPlugin/)
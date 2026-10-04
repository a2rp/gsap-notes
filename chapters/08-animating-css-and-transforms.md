# 08. Animating CSS and transforms

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Controlling tweens and timelines](./07-controlling-tweens-and-timelines.md) | [Notes index](../README.md) | [Next: Animating SVG and attributes](./09-animating-svg-and-attributes.md) |

## Animate common CSS properties

GSAP can animate numeric CSS values, opacity, colors, and many other CSS properties. Use values that match the property and the element's style.

~~~js
gsap.to(".notice", {
  opacity: 1,
  backgroundColor: "#242424",
  borderColor: "#e85b24",
  duration: 0.3,
});
~~~

For properties with units, GSAP can use values such as "24px" or "50%". Use a consistent unit when a property needs an explicit unit, especially when the browser cannot infer one from the current style.

## Use transform shortcuts

GSAP provides transform properties such as x, y, xPercent, yPercent, scale, rotation, and transformOrigin. These compose movement and rotation without replacing the entire transform string.

~~~js
gsap.from(".dialog", {
  x: 24,
  y: 8,
  scale: 0.98,
  autoAlpha: 0,
  transformOrigin: "center",
  duration: 0.28,
  ease: "power2.out",
});
~~~

autoAlpha combines opacity with visibility. When opacity reaches zero, visibility becomes hidden. This can be useful for removing an invisible element from pointer interaction, but do not apply it to focused content without moving focus appropriately.

## Animate CSS custom properties

GSAP can animate a CSS custom property. Define the property in CSS, then change it from a tween.

~~~css
.progress {
  --progress: 0%;
  width: var(--progress);
  height: 6px;
  background: #e85b24;
}
~~~

~~~js
gsap.to(".progress", {
  "--progress": "100%",
  duration: 0.8,
  ease: "power1.out",
});
~~~

A custom property can drive more than one visual style. Keep its initial value in CSS so the element has a usable appearance before the tween runs.

## Clear inline styles deliberately

GSAP writes inline styles for animated properties. clearProps removes selected inline properties when a tween completes.

~~~js
gsap.to(".temporary-panel", {
  x: 120,
  opacity: 0,
  duration: 0.25,
  onComplete: () => {
    gsap.set(".temporary-panel", { clearProps: "transform,opacity" });
  },
});
~~~

Clearing an inline property returns control to the stylesheet. Make sure the stylesheet provides the intended resting appearance, or the element may jump to an unexpected value.

## Keep layout changes understandable

Animating a transform usually moves an element visually without changing its position in document flow. Animating height or width changes layout and can move surrounding content. Choose based on whether surrounding elements should reflow, and test with real content.

## Practice questions

1. Which types of CSS properties can GSAP animate?
2. Why can an explicit unit such as px or percent help?
3. Name four GSAP transform properties.
4. What does autoAlpha combine?
5. Why can autoAlpha require care when content has keyboard focus?
6. How can GSAP animate a CSS custom property?
7. What does clearProps do?
8. How does animating height differ from animating a transform for document flow?

## Main references

- [CSS properties](https://gsap.com/docs/v3/GSAP/CorePlugins/CSS/)
- [CSSPlugin](https://gsap.com/docs/v3/GSAP/CorePlugins/CSS/)
- [gsap.set() and clearProps](https://gsap.com/docs/v3/GSAP/gsap.set/)
- [Tween vars](https://gsap.com/docs/v3/GSAP/gsap.to/)
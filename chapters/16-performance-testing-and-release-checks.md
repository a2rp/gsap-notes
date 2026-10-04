# 16. Performance, testing, and release checks

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Accessibility and reduced motion](./15-accessibility-and-reduced-motion.md) | [Notes index](../README.md) | [Next: All code samples](./98-all-code-samples.md) |

## Prefer properties that avoid repeated layout work

Transforms and opacity can often animate without recalculating the full page layout. Properties such as width and height may cause surrounding content to reflow. Choose based on the visual behavior and test the result with realistic content.

This is a guideline, not a rule that forbids layout animation. Sometimes content should expand and push later content down. In that case, test performance and make sure the change remains readable.

## Reuse setters for high-frequency input

When a pointer or another high-frequency event repeatedly updates one property, gsap.quickTo can reuse a tween instead of creating a new tween for every event.

~~~js
const moveToX = gsap.quickTo(".cursor-marker", "x", {
  duration: 0.2,
  ease: "power2.out",
});

function handlePointerMove(event) {
  moveToX(event.clientX);
}

window.addEventListener("pointermove", handlePointerMove);

// Remove this listener when the feature is removed.
function cleanup() {
  window.removeEventListener("pointermove", handlePointerMove);
}
~~~

Keep the listener scoped to the feature that needs it. Remove listeners when that feature is removed, and consider touch input and reduced-motion preferences before adding a pointer-following effect.

## Refresh scroll measurements after layout changes

ScrollTrigger measures start and end positions from document layout. If application code adds content, loads images, or changes a region's size after setup, refresh measurements when the layout is ready.

~~~js
image.addEventListener("load", () => {
  ScrollTrigger.refresh();
});
~~~

Avoid refreshing on every scroll frame. Refresh after a meaningful layout change, and remove event listeners when the component or page is discarded.

## Inspect real performance

Use browser performance tools while reproducing the real interaction. Check for dropped frames, long tasks, excessive layout recalculation, and repeated work from event callbacks.

Test realistic text lengths, image sizes, screen widths, and device input. A short local example may not expose layout shifts or performance issues on the actual page.

## Check the production build

Register imported plugins so build tools do not remove them during tree shaking. Run the production build and confirm that each plugin used by the page is present.

Remove development markers, temporary logging, and test-only controls. Confirm that ScrollTrigger positions still work after fonts and images load, and that animations clean up when a React route or component is removed.

## Release checklist

Before release, verify that the page works with reduced motion, keyboard focus stays visible, controls remain usable while animation runs, layout changes do not hide content, event listeners are removed, and the production build contains registered plugins.

When a performance issue appears, reduce the example to the smallest interaction that reproduces it. This makes layout, timing, and cleanup problems easier to identify.

## Practice questions

1. Why are transforms and opacity often preferred for frequent animation?
2. When can animating width or height still be the right choice?
3. What does gsap.quickTo help avoid?
4. Why should high-frequency event listeners be cleaned up?
5. When should ScrollTrigger.refresh be called?
6. Which performance signs should be checked in browser tools?
7. What should be checked after images and fonts load?
8. Which items belong in a final release check?

## Main references

- [GSAP performance](https://gsap.com/resources/)
- [gsap.quickTo()](https://gsap.com/docs/v3/GSAP/gsap.quickTo/)
- [ScrollTrigger.refresh()](https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.refresh())
- [Plugin registration](https://gsap.com/docs/v3/GSAP/gsap.registerPlugin/)
- [Accessibility guidance](https://gsap.com/resources/accessibility/)
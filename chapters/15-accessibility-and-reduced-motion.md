# 15. Accessibility and reduced motion

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Event-driven animation in React](./14-event-driven-animation-in-react.md) | [Notes index](../README.md) | [Next: Performance, testing, and release checks](./16-performance-testing-and-release-checks.md) |

## Respect the reduced-motion preference

gsap.matchMedia can respond to the prefers-reduced-motion media feature. Add movement only when the user has not requested reduced motion.

~~~js
const motionPreference = gsap.matchMedia();

motionPreference.add(
  "(prefers-reduced-motion: no-preference)",
  () => {
    gsap.from(".intro-art", {
      y: 12,
      duration: 0.25,
      ease: "power1.out",
    });
  }
);
~~~

The content starts visible and remains useful if no animation runs. This example limits movement to a small entrance. Large parallax movement, rapid scaling, and long travel should be removed or greatly reduced for users who prefer less motion.

## Keep controls semantic and keyboard operable

Use native controls and preserve a visible focus style. Motion should add feedback without replacing the browser's keyboard behavior.

~~~html
<button class="save-button" type="button">Save changes</button>
~~~

~~~css
.save-button:focus-visible {
  outline: 3px solid #e85b24;
  outline-offset: 3px;
}
~~~

A button already supports keyboard activation. If an animation is attached to an action, trigger the same behavior from its click event rather than requiring pointer hover.

## Do not make motion the only signal

Pair visual movement with text, color, or a semantic state that communicates the result. A check mark animation can accompany a visible "Saved" message, but the animation alone should not carry the meaning.

Avoid flashing or rapidly alternating colors. Repeating motion should be necessary, limited, and stoppable when it could distract from reading.

## Handle focus when content changes

When a panel closes, move focus out of its content before it becomes hidden. Keep aria-expanded in sync with the disclosure state. Avoid hiding a focused control with visibility or opacity while leaving keyboard focus inside it.

Large pinned sections can interfere with reading and keyboard navigation. Keep the normal page content available, provide a reduced-motion path, and test the experience without a mouse.

## Review motion with user settings

Test the operating system's reduced-motion setting, keyboard navigation, browser zoom, and narrow layouts. Check that focus remains visible during movement and that content is readable while a transition runs.

For an application-wide motion preference, use matchMedia around the animations that should change. Revert or remove animations when the query no longer matches so the page does not retain stale inline styles.

## Practice questions

1. Which media feature represents the reduced-motion preference?
2. How does the example decide whether to add movement?
3. Why should content start visible before the animation?
4. Which HTML element is appropriate for a save action?
5. What does :focus-visible style?
6. Why should motion not be the only signal for a result?
7. What should happen to focus when a panel closes?
8. Which user settings and input methods should be tested?

## Main references

- [GSAP accessibility guidance](https://gsap.com/resources/accessibility/)
- [gsap.matchMedia()](https://gsap.com/docs/v3/GSAP/gsap.matchMedia/)
- [ScrollTrigger and accessibility](https://gsap.com/resources/accessibility/)
# 02. Targets, methods, and animation values

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: GSAP setup and first tween](./01-gsap-setup-and-first-tween.md) | [Notes index](../README.md) | [Next: Tween timing, repeats, and callbacks](./03-tween-timing-repeats-and-callbacks.md) |

## Choose animation targets

A target can be a CSS selector, a DOM element, an array of elements, or a JavaScript object. A selector can match more than one element.

~~~js
import { gsap } from "gsap";

const cards = document.querySelectorAll(".card");

gsap.to(".notice", { opacity: 1, duration: 0.25 });
gsap.to(cards, { y: -8, duration: 0.3 });
~~~

Prefer a selector or element reference that identifies only the intended elements. When the page contains repeated components, scope selection to the component that owns the animation instead of querying a broad class across the whole document.

## Use to, from, and fromTo

gsap.to animates from the current rendered values to the values you provide. gsap.from animates from the provided values back to the current rendered values. gsap.fromTo defines both endpoints.

~~~js
import { gsap } from "gsap";

gsap.to(".to-card", {
  x: 80,
  opacity: 1,
  duration: 0.4,
});

gsap.from(".from-card", {
  y: 20,
  opacity: 0,
  duration: 0.4,
});

gsap.fromTo(
  ".from-to-card",
  { scale: 0.8, opacity: 0 },
  { scale: 1, opacity: 1, duration: 0.4 }
);
~~~

A from tween may render its starting values immediately when created. If the target is visible before the animation should begin, create it at the right time or configure immediate rendering deliberately.

## Set values without visible duration

gsap.set applies values immediately. It is a convenient form of a zero-duration tween and can prepare an element before a later animation.

~~~js
gsap.set(".panel", { x: 0, opacity: 1 });
gsap.to(".panel", { x: 120, duration: 0.5, ease: "power2.out" });
~~~

For a sequence of setup and animation steps, a timeline can place a set at a specific point. Timelines are covered in a later chapter.

## Use relative values

A relative value changes the current value instead of replacing it with a fixed absolute target.

~~~js
gsap.to(".box", {
  x: "+=40",
  rotation: "+=15",
  duration: 0.3,
});
~~~

Relative values are useful for repeated movement, but repeated clicks can keep moving the element farther away. Decide whether each action should start from the current position or return to a known position first.

## Animate JavaScript objects

GSAP can animate numeric properties on a plain object. This is useful for updating a canvas drawing value or another numeric model.

~~~js
const progress = { value: 0 };

gsap.to(progress, {
  value: 100,
  duration: 1,
  onUpdate: () => {
    console.log(Math.round(progress.value));
  },
});
~~~

onUpdate runs repeatedly while the tween changes. Keep the callback lightweight. If it updates a visible DOM element, avoid rebuilding a large section of the page on every frame.

## Practice questions

1. Which target types can GSAP animate?
2. What happens when a selector matches several elements?
3. How does gsap.to choose its starting values?
4. What does gsap.from animate toward?
5. When is gsap.fromTo useful?
6. What does gsap.set do?
7. How does a relative value such as x: "+=40" behave?
8. Why should an onUpdate callback stay lightweight?

## Main references

- [Tween targets](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [gsap.to()](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [gsap.from()](https://gsap.com/docs/v3/GSAP/gsap.from/)
- [gsap.fromTo()](https://gsap.com/docs/v3/GSAP/gsap.fromTo/)
- [gsap.set()](https://gsap.com/docs/v3/GSAP/gsap.set/)
# 03. Tween timing, repeats, and callbacks

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Targets, methods, and animation values](./02-targets-methods-and-animation-values.md) | [Notes index](../README.md) | [Next: Eases and motion feel](./04-eases-and-motion-feel.md) |

## Configure when a tween starts and ends

duration sets how long a tween takes in seconds. delay waits before its first run. These values belong in the tween vars object.

~~~js
gsap.to(".notification", {
  y: 0,
  opacity: 1,
  duration: 0.35,
  delay: 0.2,
});
~~~

A delay can help sequence a small entrance, but long delays can make controls feel unresponsive. Do not delay important content merely to make an animation more noticeable.

## Repeat and reverse a tween

repeat is the number of additional plays after the first one. Set repeat to -1 for an indefinite repeat. yoyo makes alternate repeats travel backward between the start and end values. repeatDelay adds a pause between repeats.

~~~js
gsap.to(".pulse", {
  scale: 1.08,
  duration: 0.6,
  repeat: 2,
  repeatDelay: 0.25,
  yoyo: true,
  ease: "power1.inOut",
});
~~~

With repeat: 2, the tween plays three times in total. The first play is followed by two repeats. An infinite repeat can continue to consume attention, so reserve it for a meaningful status or ambient effect and provide a way to stop it when needed.

## Run callbacks at useful points

Callbacks let application code react when an animation starts, updates, repeats, or completes. Keep callbacks focused on the event rather than doing expensive work on every frame.

~~~js
gsap.to(".progress-bar", {
  scaleX: 1,
  transformOrigin: "left center",
  duration: 1,
  onStart: () => console.log("Progress started"),
  onUpdate: () => console.log("Progress is changing"),
  onComplete: () => console.log("Progress finished"),
});
~~~

Do not use an arrow callback's this value to read tween state. GSAP passes callback parameters when configured, and a stored tween can be inspected directly. For example, keep the return value from gsap.to and read its progress when required.

~~~js
const tween = gsap.to(".meter", {
  x: 180,
  duration: 1,
  onUpdate: () => {
    console.log(tween.progress());
  },
});
~~~

For a real interface, an onUpdate callback should not print or perform heavy work on every frame. Update only the visual or application value that actually needs to change.

## Recalculate function values on repeat

repeatRefresh asks GSAP to invalidate and recalculate dynamically defined values on each repeat. This is useful when a function-based destination should be chosen again each time.

~~~js
gsap.to(".particle", {
  x: () => gsap.utils.random(-80, 80),
  y: () => gsap.utils.random(-40, 40),
  duration: 0.8,
  repeat: 3,
  repeatRefresh: true,
});
~~~

A fixed numeric value remains fixed. repeatRefresh is most useful when the vars object contains function-based values that should be evaluated again.

## Practice questions

1. Which unit does duration use?
2. What does delay change?
3. How many total plays does repeat: 2 produce?
4. What does yoyo do between repeats?
5. When can repeatDelay be useful?
6. Which lifecycle events can callbacks observe?
7. Why should an onUpdate callback avoid heavy work?
8. What does repeatRefresh recalculate?

## Main references

- [Tween vars](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [Tween callbacks](https://gsap.com/docs/v3/GSAP/Tween/)
- [repeat](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [repeatRefresh](https://gsap.com/docs/v3/GSAP/gsap.to/)
# 10. ScrollTrigger foundations

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Animating SVG and attributes](./09-animating-svg-and-attributes.md) | [Notes index](../README.md) | [Next: ScrollTrigger scrub, pin, and snap](./11-scrolltrigger-scrub-pin-and-snap.md) |

## Import and register ScrollTrigger

ScrollTrigger is an optional GSAP plugin. Import it and register it before creating animations that use its features.

~~~js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
~~~

Registration tells GSAP about the plugin and helps bundlers keep it in production builds. Register each plugin that the module uses.

## Start a tween when an element reaches the viewport

Add a scrollTrigger object to a tween. trigger identifies the element used for measurement, and start describes where that element meets the viewport.

~~~js
gsap.from(".feature-card", {
  y: 24,
  opacity: 0,
  duration: 0.35,
  ease: "power2.out",
  scrollTrigger: {
    trigger: ".feature-card",
    start: "top 82%",
    once: true,
  },
});
~~~

start: "top 82%" means the top of the trigger reaches a point 82 percent down from the top of the viewport. ScrollTrigger calculates positions from the document layout.

The content remains in the page whether the animation runs or not. Avoid hiding essential text until a scroll event occurs.

## Choose what happens when the trigger crosses a boundary

toggleActions configures behavior for entering, leaving, entering again from below, and leaving again in reverse. The four values appear in that order.

~~~js
gsap.from(".replay-card", {
  x: -20,
  opacity: 0,
  duration: 0.3,
  scrollTrigger: {
    trigger: ".replay-card",
    start: "top 85%",
    toggleActions: "play none none reverse",
  },
});
~~~

This example plays on entry and reverses when the user scrolls back past the starting boundary. Use once: true when the animation should run only on its first entry instead.

## Debug trigger positions

Set markers: true while tuning start and end positions. Markers show where ScrollTrigger measures its boundaries.

~~~js
gsap.to(".debug-box", {
  x: 120,
  scrollTrigger: {
    trigger: ".debug-box",
    start: "top center",
    end: "bottom center",
    markers: true,
  },
});
~~~

Remove markers before release. If positions are wrong after images or fonts load, refresh measurements after the layout is ready rather than guessing at new offsets.

## Create a trigger without an attached tween

ScrollTrigger can also observe a region and run callbacks without controlling a tween. Use this when an application needs to respond to entering or leaving a section.

~~~js
ScrollTrigger.create({
  trigger: ".chapter",
  start: "top center",
  onEnter: () => console.log("Chapter entered"),
  onLeaveBack: () => console.log("Chapter left in reverse"),
});
~~~

Keep callbacks small. A scroll callback can run during normal interaction and should not repeatedly build large DOM trees.

## Practice questions

1. Which package module exports ScrollTrigger?
2. What does gsap.registerPlugin do?
3. What does the trigger option identify?
4. How is start: "top 82%" interpreted?
5. In what order does toggleActions list its four behaviors?
6. What does once: true do?
7. Why use markers during development?
8. Why should essential content remain available before an entrance animation runs?

## Main references

- [ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
- [start](https://gsap.com/docs/v3/Plugins/ScrollTrigger/start/)
- [toggleActions](https://gsap.com/docs/v3/Plugins/ScrollTrigger/toggleActions/)
- [Plugin registration](https://gsap.com/docs/v3/GSAP/gsap.registerPlugin/)
# 11. ScrollTrigger scrub, pin, and snap

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: ScrollTrigger foundations](./10-scrolltrigger-foundations.md) | [Notes index](../README.md) | [Next: Responsive animation with matchMedia](./12-responsive-animation-with-matchmedia.md) |

## Link a timeline to scroll progress

scrub connects the animation playhead to scroll position. The user moves the animation forward and backward by scrolling through the configured range.

~~~js
const story = gsap.timeline({
  scrollTrigger: {
    trigger: ".story",
    start: "top top",
    end: "+=1400",
    scrub: true,
  },
});

story
  .to(".story-art", { x: 180, rotation: 12 })
  .to(".story-caption", { opacity: 1, y: 0 }, "<");
~~~

With scrub: true, the playhead follows the scrollbar directly. A numeric scrub value, such as scrub: 0.5, adds catch-up smoothing after the scroll position changes.

## Pin a section while the timeline plays

pin holds a trigger in place for part of the scroll range. Animate elements inside the pinned section rather than animating the pinned trigger itself.

~~~js
const panels = gsap.timeline({
  scrollTrigger: {
    trigger: ".feature-story",
    start: "top top",
    end: "+=1800",
    scrub: 0.4,
    pin: true,
    anticipatePin: 1,
  },
});

panels
  .to(".feature-one", { xPercent: -100 })
  .to(".feature-two", { xPercent: -100 });
~~~

Pinning changes page flow while the trigger is active. Check the surrounding layout and test the page at different viewport sizes. Avoid nesting many pinned sections because their measurements and spacing can become difficult to reason about.

## Snap to useful progress points

snap lets the scroll position settle at chosen progress values after the user stops scrolling. For a fixed number of panels, use evenly spaced progress points.

~~~js
gsap.to(".slide-track", {
  xPercent: -75,
  ease: "none",
  scrollTrigger: {
    trigger: ".slides",
    start: "top top",
    end: "+=1200",
    scrub: true,
    pin: true,
    snap: 1 / 3,
  },
});
~~~

For four panels, 1 / 3 divides the scroll progress into three equal intervals. Snapping can take control of scroll position, so use it only when those landing points are useful and test trackpad, wheel, touch, and keyboard scrolling.

## Keep scroll movement understandable

A scroll-linked effect is controlled by the user's scroll rather than a fixed-duration playback. Keep the relationship between scroll distance and visual progress predictable. Do not use a pinned section to hide content or make essential controls unreachable.

Reduced-motion preferences should change or remove large pinned and parallax effects. Always keep the information available in the normal document content.

## Practice questions

1. What does scrub connect?
2. How does scrub: 0.5 differ from scrub: true?
3. What does pin do during a trigger range?
4. Why should content inside a pinned section be animated instead of the pinned trigger itself?
5. How can nested pins complicate a page?
6. What does snap do after scrolling stops?
7. Why is 1 / 3 used for four evenly spaced panels?
8. Which input methods should be tested when snapping is enabled?

## Main references

- [ScrollTrigger scrub](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
- [pin](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
- [snap](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
- [ScrollTrigger start and end](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
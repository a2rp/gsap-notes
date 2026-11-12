# 12. Responsive animation with matchMedia

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: ScrollTrigger scrub, pin, and snap](./11-scrolltrigger-scrub-pin-and-snap.md) | [Notes index](../README.md) | [Next: GSAP in React with useGSAP](./13-gsap-in-react-with-usegsap.md) |

## Match animations to media conditions

gsap.matchMedia lets an animation setup run while media queries match. Animations and ScrollTriggers created inside the callback are reverted when its media setup changes. If a named condition changes while another condition still matches, GSAP reruns the callback with the updated condition values.

~~~js
const media = gsap.matchMedia();

media.add(
  {
    wide: "(min-width: 800px)",
    narrow: "(max-width: 799px)",
    reduceMotion: "(prefers-reduced-motion: reduce)",
  },
  (context) => {
    const { wide, narrow, reduceMotion } = context.conditions;

    if (reduceMotion) {
      return;
    }

    gsap.from(".hero-art", {
      x: wide ? 80 : narrow ? 20 : 0,
      opacity: 0,
      duration: wide ? 0.5 : narrow ? 0.25 : 0,
    });
  }
);
~~~

The callback receives a context with the matched named conditions. A conditions object runs its callback when at least one condition matches, so include both wide and narrow breakpoints to cover regular viewport widths. This example skips the entrance movement when reduced motion is preferred and uses a shorter, smaller entrance on narrow screens.

## Use an animation only where it fits

Not every animation needs a scaled-down version on a smaller screen. If the motion only fits a wide layout, set it up for that media query and let CSS handle the narrow layout. GSAP reverts the setup when its query stops matching.

~~~js
const responsive = gsap.matchMedia();

responsive.add("(min-width: 900px)", () => {
  gsap.to(".desktop-decoration", {
    x: 120,
    rotation: 8,
    duration: 0.4,
  });
});
~~~

When the viewport is narrower than 900 pixels, no animation setup runs and the stylesheet controls the decoration. Keep any extra DOM listeners or non-GSAP resources under their own cleanup logic.

## Revert media setup when finished

The returned matchMedia object can be reverted when the page or feature is removed.

~~~js
const mediaSetup = gsap.matchMedia();

mediaSetup.add("(min-width: 700px)", () => {
  gsap.to(".feature", { y: -12, duration: 0.3 });
});

function removeFeature() {
  mediaSetup.revert();
}
~~~

In a single-page application, connect revert to the route or component lifecycle so old media-query animations do not remain active after the view is removed.

## Avoid layout-only assumptions

A media query can change both animation values and the page layout. Test after fonts and images load, and verify that the trigger positions remain correct after a breakpoint change. ScrollTrigger measurements may need refreshing when application code changes layout outside the matchMedia setup.

## Practice questions

1. What does gsap.matchMedia observe?
2. What does the callback context provide?
3. When are GSAP animations created in a matchMedia callback reverted?
4. How can reduced motion affect the animation setup?
5. Why might a mobile layout need a separate animation choice?
6. What does matchMedia object's revert method do?
7. Which non-GSAP resources still need their own cleanup?
8. Why should ScrollTrigger positions be checked after a breakpoint change?

## Main references

- [gsap.matchMedia()](https://gsap.com/docs/v3/GSAP/gsap.matchMedia/)
- [gsap.matchMediaRefresh()](https://gsap.com/docs/v3/GSAP/gsap.matchMediaRefresh())
- [matchMedia and ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)

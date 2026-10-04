# 06. Stagger and function-based values

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Timelines, positions, and labels](./05-timelines-positions-and-labels.md) | [Notes index](../README.md) | [Next: Controlling tweens and timelines](./07-controlling-tweens-and-timelines.md) |

## Stagger a group of targets

A stagger starts the same tween on a group of targets at slightly different times. Add it to a tween vars object when each target should perform the same change.

~~~js
gsap.to(".result-card", {
  y: 0,
  opacity: 1,
  duration: 0.35,
  ease: "power2.out",
  stagger: 0.08,
});
~~~

The first card starts immediately, and each later card starts 0.08 seconds after the previous one. A stagger does not require a timeline when the targets share one animation.

## Choose the stagger order

An object gives more control over the spacing and order. The from setting chooses the starting target.

~~~js
gsap.from(".grid-card", {
  scale: 0.85,
  opacity: 0,
  duration: 0.3,
  stagger: {
    each: 0.06,
    from: "center",
    grid: "auto",
    axis: "x",
  },
});
~~~

grid: "auto" asks GSAP to infer the grid arrangement from target positions. axis limits the stagger calculation to one direction. Use these options only when the target layout has the arrangement the animation expects.

## Compute values for each target

Function-based values receive the target index, target element, and full target array. Use the index to give each item a distinct value.

~~~js
gsap.to(".list-item", {
  x: (index) => index * 14,
  duration: 0.4,
  ease: "power1.out",
  stagger: 0.07,
});
~~~

Here, later items travel farther and start later. Keep the function deterministic unless the effect needs variation. It is easier to review and repeat an animation when the same item maps to the same value.

## Combine stagger with a timeline

A timeline can coordinate a staggered group with other stages.

~~~js
const cardsTimeline = gsap.timeline();

cardsTimeline
  .from(".section-title", { y: 14, opacity: 0, duration: 0.3 })
  .from(
    ".result-card",
    { y: 18, opacity: 0, duration: 0.3, stagger: 0.08 },
    "-=0.1"
  )
  .from(".section-footer", { opacity: 0, duration: 0.2 });
~~~

The cards begin slightly before the heading tween finishes. A short, purposeful overlap can make a sequence feel connected without delaying access to every item.

## Practice questions

1. What does stagger change for a group of targets?
2. How does stagger: 0.08 place the start times?
3. What does the from option choose?
4. What does grid: "auto" ask GSAP to do?
5. Which arguments can a function-based value receive?
6. How can an index create a different value for each target?
7. When can a timeline be useful alongside stagger?
8. Why should function-based values usually be predictable?

## Main references

- [Stagger](https://gsap.com/docs/v3/GSAP/Staggers/)
- [Tween vars](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [gsap.utils](https://gsap.com/docs/v3/GSAP/UtilityMethods/)
- [Timeline](https://gsap.com/docs/v3/GSAP/Timeline/)
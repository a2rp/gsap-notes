# 04. Eases and motion feel

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Tween timing, repeats, and callbacks](./03-tween-timing-repeats-and-callbacks.md) | [Notes index](../README.md) | [Next: Timelines, positions, and labels](./05-timelines-positions-and-labels.md) |

## Shape speed over time

An ease controls how a tween changes speed between its start and end. It does not change the target values or total duration.

~~~js
gsap.to(".card", {
  x: 160,
  duration: 0.5,
  ease: "power2.out",
});
~~~

power2.out starts quickly and decelerates into the final position. This often feels responsive for a user-triggered change. power2.in starts more gradually and accelerates toward the end. power2.inOut eases both ends.

## Compare common ease families

GSAP includes ease families such as power, sine, expo, circ, back, elastic, and bounce. Power and sine eases are common choices for simple interface movement. Back, elastic, and bounce create more expressive overshoot or oscillation.

~~~js
gsap.to(".soft", {
  x: 100,
  duration: 0.7,
  ease: "sine.inOut",
});

gsap.to(".overshoot", {
  x: 100,
  duration: 0.7,
  ease: "back.out(1.4)",
});
~~~

An overshoot ease briefly moves past the destination before settling. It can add character to a playful element, but can make a small button or form control feel imprecise. Match the ease to the meaning of the interaction.

## Use different eases for different actions

An entrance often benefits from deceleration, while an exit can feel quicker as an element leaves. Choose each ease according to the direction and role of the motion.

~~~js
const entrance = gsap.from(".dialog", {
  y: 16,
  opacity: 0,
  duration: 0.3,
  ease: "power2.out",
});

function closeDialog() {
  gsap.to(".dialog", {
    y: 8,
    opacity: 0,
    duration: 0.18,
    ease: "power1.in",
  });
}
~~~

In an application, use a component ref or scoped selector rather than a page-wide selector. The example focuses on ease choices; component scoping is covered in the React and cleanup chapters.

## Keep duration and ease separate

Duration answers how long the tween runs. Ease answers how its speed changes during that time. If movement feels too slow, adjust duration first. If the start or finish feels wrong, adjust ease.

A timeline can use a default ease for its child tweens, and an individual tween can override that default. Prefer a small, consistent motion system over unrelated ease strings across every element.

## Practice questions

1. What does an ease control?
2. Does changing ease change the target value?
3. How does power2.out change speed?
4. How does power2.in differ from power2.out?
5. Which ease families can create overshoot or oscillation?
6. When can an overshoot ease be a poor choice?
7. Which ease is used for the sample entrance and why?
8. How is duration different from ease?

## Main references

- [GSAP easing](https://gsap.com/docs/v3/Eases/)
- [Ease visualizer](https://gsap.com/docs/v3/Eases/)
- [Tween vars and ease](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [Timeline defaults](https://gsap.com/docs/v3/GSAP/gsap.timeline/)
# 05. Timelines, positions, and labels

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Eases and motion feel](./04-eases-and-motion-feel.md) | [Notes index](../README.md) | [Next: Stagger and function-based values](./06-stagger-and-function-based-values.md) |

## Group related tweens in a timeline

A timeline sequences tweens on one shared playhead. It is easier to coordinate than giving each tween a separate delay.

~~~js
import { gsap } from "gsap";

const intro = gsap.timeline({
  defaults: {
    duration: 0.4,
    ease: "power2.out",
  },
});

intro
  .from(".page-title", { y: 20, opacity: 0 })
  .from(".page-copy", { y: 12, opacity: 0 })
  .from(".page-action", { y: 8, opacity: 0 });
~~~

The second tween starts after the first by default. The next chapter shows how a stagger can animate a collection of similar targets.

## Control placement with the position parameter

The position parameter places a tween at a time in the timeline. A number means an absolute time in seconds. A string can place a tween relative to the previous child.

~~~js
const sequence = gsap.timeline({ defaults: { duration: 0.5 } });

sequence
  .to(".first", { x: 100 })
  .to(".second", { x: 100 }, "+=0.2")
  .to(".third", { x: 100 }, "<")
  .to(".fourth", { x: 100 }, ">-0.15");
~~~

The second tween starts 0.2 seconds after the timeline's current end. The less-than position starts with the previous tween. The greater-than position starts 0.15 seconds before the previous tween ends. These relative positions help create overlap without calculating every start time.

## Name important moments with labels

Labels make a timeline easier to read and control. Add a label, place a tween at it, or seek the playhead to it later.

~~~js
const story = gsap.timeline({ paused: true });

story
  .addLabel("heading")
  .from(".heading", { opacity: 0, y: 16, duration: 0.35 })
  .addLabel("details")
  .from(".details", { opacity: 0, duration: 0.25 }, "details");

story.play();
~~~

A stored timeline can be paused, resumed, reversed, restarted, or moved to a label with methods such as pause(), play(), reverse(), restart(), and seek().

## Apply shared defaults

Timeline defaults reduce repetition for common tween settings such as duration and ease. A child tween can provide its own value to override a default.

~~~js
const panel = gsap.timeline({
  defaults: {
    duration: 0.3,
    ease: "power1.out",
  },
});

panel
  .from(".panel-title", { y: 10, opacity: 0 })
  .from(".panel-body", { opacity: 0, duration: 0.5 });
~~~

Use defaults for values that genuinely belong to the whole sequence. If every child needs a different duration or feel, explicit settings may be clearer.

## Practice questions

1. What does a GSAP timeline coordinate?
2. Where does the second child tween start by default?
3. What does a numeric position value mean?
4. What does "+=0.2" do?
5. What does the less-than position token mean?
6. How can a tween start shortly before the previous tween ends?
7. Why add labels to a timeline?
8. How can a child tween override timeline defaults?

## Main references

- [Timeline](https://gsap.com/docs/v3/GSAP/Timeline/)
- [gsap.timeline()](https://gsap.com/docs/v3/GSAP/gsap.timeline/)
- [Position parameter](https://gsap.com/resources/position-parameter/)
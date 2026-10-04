# 07. Controlling tweens and timelines

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Stagger and function-based values](./06-stagger-and-function-based-values.md) | [Notes index](../README.md) | [Next: Animating CSS and transforms](./08-animating-css-and-transforms.md) |

## Keep a reference when playback needs control

gsap.to and gsap.timeline return animation instances. Store the instance when a button or application event needs to control playback later.

~~~js
const panelTimeline = gsap.timeline({ paused: true });

panelTimeline
  .from(".panel-title", { y: 12, opacity: 0, duration: 0.25 })
  .from(".panel-body", { opacity: 0, duration: 0.2 });

document.querySelector("[data-play]").addEventListener("click", () => {
  panelTimeline.play();
});
~~~

paused: true creates the timeline without starting it. play resumes toward the end. The method can also take a time or label when playback should start from a specific position.

## Add pause, reverse, and restart controls

A real button can call the methods on the stored animation instance.

~~~html
<button type="button" data-play>Play</button>
<button type="button" data-reverse>Reverse</button>
<button type="button" data-restart>Restart</button>
~~~

~~~js
document.querySelector("[data-play]").addEventListener("click", () => {
  panelTimeline.play();
});

document.querySelector("[data-reverse]").addEventListener("click", () => {
  panelTimeline.reverse();
});

document.querySelector("[data-restart]").addEventListener("click", () => {
  panelTimeline.restart();
});
~~~

Remove event listeners when the owning component or page is discarded. In React, attach handlers through JSX and scope animation creation to the component lifecycle.

## Seek, inspect progress, and change speed

A tween or timeline can jump to an absolute time or a label, report progress, or play at a different speed.

~~~js
panelTimeline.seek(0.5);
console.log(panelTimeline.progress());
panelTimeline.timeScale(1.5);
~~~

progress returns a normalized value from zero to one. timeScale changes playback speed, where 1 is the original rate, 0.5 is half speed, and 2 is double speed.

## Stop or restore an animation

kill stops an animation and removes it from its parent timeline. It does not necessarily restore the target's original styles. revert kills the animation and restores the values that were present before it ran.

~~~js
const movement = gsap.to(".moving-card", {
  x: 120,
  duration: 1,
});

function stopAndRestore() {
  movement.revert();
}
~~~

Choose kill when the animation should stop and the current visual state should remain. Choose revert when temporary animation styles should be removed. Context-based cleanup for a component is covered in the React chapter.

## Practice questions

1. What does gsap.to return?
2. What does paused: true do on a timeline?
3. How do play and reverse differ?
4. What does restart do?
5. What values can seek accept?
6. What range does progress report?
7. How does timeScale change playback speed?
8. What is the difference between kill and revert?

## Main references

- [GSAP animation controls](https://gsap.com/docs/v3/GSAP/)
- [Timeline methods](https://gsap.com/docs/v3/GSAP/Timeline/)
- [kill()](https://gsap.com/docs/v3/GSAP/Tween/kill())
- [revert()](https://gsap.com/docs/v3/GSAP/Tween/revert())
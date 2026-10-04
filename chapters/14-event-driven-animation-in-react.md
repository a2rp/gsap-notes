# 14. Event-driven animation in React

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: GSAP in React with useGSAP](./13-gsap-in-react-with-usegsap.md) | [Notes index](../README.md) | [Next: Accessibility and reduced motion](./15-accessibility-and-reduced-motion.md) |

## Create a tween from a button event

Use React event props for user actions. Wrap a GSAP animation created after the hook callback with contextSafe so the integration can collect and clean it up.

~~~jsx
import { useRef } from "react";
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

export function NudgeCard() {
  const container = useRef(null);
  const { contextSafe } = useGSAP({ scope: container });

  const nudge = contextSafe(() => {
    gsap.to(".card", {
      x: 16,
      duration: 0.2,
      repeat: 1,
      yoyo: true,
      ease: "power1.inOut",
      overwrite: "auto",
    });
  });

  return (
    <section ref={container}>
      <button type="button" onClick={nudge}>
        Nudge card
      </button>
      <article className="card">This card responds to the button.</article>
    </section>
  );
}
~~~

The button remains the real interaction. The animation is scoped to the component and its tween is tracked by the hook context.

## Let React state choose the target

Use React state when the action changes application meaning, such as whether a disclosure is open. The animation should reflect that state.

~~~jsx
import { useRef, useState } from "react";
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

export function DetailsPanel() {
  const container = useRef(null);
  const [open, setOpen] = useState(false);

  useGSAP(
    () => {
      gsap.to(".details", {
        autoAlpha: open ? 1 : 0,
        y: open ? 0 : 8,
        duration: 0.25,
        overwrite: "auto",
      });
    },
    { scope: container, dependencies: [open] }
  );

  return (
    <section ref={container}>
      <button
        type="button"
        aria-expanded={open}
        onClick={() => setOpen((value) => !value)}
      >
        {open ? "Hide details" : "Show details"}
      </button>
      <p className="details" aria-hidden={!open}>
        Extra information controlled by React state
      </p>
    </section>
  );
}
~~~

~~~css
.details {
  visibility: hidden;
  opacity: 0;
}
~~~

This example contains plain text. If a disclosure contains links or other focusable controls, make sure closing it moves focus safely and prevents hidden controls from receiving focus. A native details and summary element may be simpler when custom animation is unnecessary.

## Avoid creating a new tween on every render

Do not call gsap.to directly in the component body. A React render can happen for many reasons, and creating an animation during each render can restart or duplicate work.

Create initial animations in useGSAP. Create event-driven animations in a contextSafe handler. When state determines a target, pass dependencies to the hook and revert the previous setup when it needs to be rebuilt.

## Handle repeated events

Users can activate a control before a previous tween completes. overwrite: "auto" lets the new tween take control of conflicting properties on the same target. Choose whether the interaction should restart, reverse, finish, or interrupt the current animation.

Do not use hover as the only input. If a visual response matters, provide an equivalent click, keyboard, or touch interaction.

## Practice questions

1. Why use React event props for button actions?
2. What does contextSafe do for a later event-created tween?
3. Why does the example scope selectors to a component ref?
4. When should React state choose the animation target?
5. Why should a disclosure's aria-expanded value match its visible state?
6. Why should gsap.to not run directly in the component body?
7. What does overwrite: "auto" help manage?
8. Why should hover not be the only way to trigger an important response?

## Main references

- [GSAP React guide](https://gsap.com/resources/React/)
- [useGSAP and contextSafe](https://github.com/greensock/react)
- [Tween overwrite](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [React accessibility](https://gsap.com/resources/accessibility/)
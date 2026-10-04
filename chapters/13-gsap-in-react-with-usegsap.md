# 13. GSAP in React with useGSAP

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Responsive animation with matchMedia](./12-responsive-animation-with-matchmedia.md) | [Notes index](../README.md) | [Next: Event-driven animation in React](./14-event-driven-animation-in-react.md) |

## Install the React integration

Add GSAP and the official React integration package:

~~~sh
npm install gsap @gsap/react
~~~

Import and register the hook in a JavaScript module:

~~~jsx
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);
~~~

Registering the hook helps bundlers preserve it and avoids loading multiple copies of the integration.

## Scope an animation to a component

Pass a container ref as the scope. Selector strings in the hook callback then match only elements inside that component.

~~~jsx
import { useRef } from "react";
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

export function IntroPanel() {
  const container = useRef(null);

  useGSAP(
    () => {
      gsap.from(".intro-title", {
        y: 18,
        opacity: 0,
        duration: 0.35,
        ease: "power2.out",
      });
    },
    { scope: container }
  );

  return (
    <section ref={container}>
      <h1 className="intro-title">GSAP in a React component</h1>
    </section>
  );
}
~~~

useGSAP uses a GSAP context to collect animations and clean them up when the component is removed. The scope ref avoids a global query that could select another instance of the same component.

## Re-run animation setup for changing dependencies

When an animation depends on React data, pass dependencies explicitly. Set revertOnUpdate when the previous animation should be reverted before the callback runs again.

~~~jsx
useGSAP(
  () => {
    gsap.to(".active-card", {
      x: isActive ? 0 : 24,
      opacity: isActive ? 1 : 0.7,
      duration: 0.25,
    });
  },
  {
    scope: container,
    dependencies: [isActive],
    revertOnUpdate: true,
  }
);
~~~

Put this hook call inside the component body and declare container and isActive there. Reverting prevents old inline styles and animations from accumulating across updates.

## Make event-created animations context-safe

Animations created later in an event handler are outside the original hook callback. Wrap the handler with contextSafe so those animations join the same context and are cleaned up.

~~~jsx
import { useRef } from "react";
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);

export function AnimationActions() {
  const container = useRef(null);
  const { contextSafe } = useGSAP({ scope: container });

  const rotateCard = contextSafe(() => {
    gsap.to(".active-card", {
      rotation: 8,
      duration: 0.2,
      yoyo: true,
      repeat: 1,
    });
  });

  return (
    <section ref={container}>
      <button type="button" onClick={rotateCard}>
        Rotate card
      </button>
      <div className="active-card">Card content</div>
    </section>
  );
}
~~~

This is a component fragment showing the hook and returned JSX. In a full component, keep hooks at the top level and return one component tree. The button remains a native keyboard-operable control.

## Keep React and GSAP responsibilities clear

React renders content and owns application state. GSAP changes visual properties and coordinates animation timing. Let React decide whether a component exists, then use GSAP to animate the transition or its contents.

Do not create a timeline during every render. Create it in useGSAP or a context-safe event handler, and let the hook clean up when the component lifecycle changes.

## Practice questions

1. Which package adds the GSAP React integration?
2. Why register useGSAP with GSAP?
3. What does the scope ref limit?
4. How does useGSAP clean up animations?
5. When should dependencies be passed to useGSAP?
6. What does revertOnUpdate do?
7. Why wrap a later event handler with contextSafe?
8. Which responsibilities should remain with React?

## Main references

- [GSAP React guide](https://gsap.com/resources/React/)
- [@gsap/react package](https://github.com/greensock/react)
- [gsap.context()](https://gsap.com/docs/v3/GSAP/gsap.context())
- [gsap.registerPlugin()](https://gsap.com/docs/v3/GSAP/gsap.registerPlugin/)
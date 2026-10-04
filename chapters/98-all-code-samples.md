# 98. All code samples

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Performance, testing, and release checks](./16-performance-testing-and-release-checks.md) | [Notes index](../README.md) | [Next: Complete questions and answers](./99-complete-q-and-a.md) |

## Source chapter: [01. GSAP setup and first tween](./01-gsap-setup-and-first-tween.md)

### Sample 1

~~~sh
npm install gsap
~~~

### Sample 2

~~~js
import { gsap } from "gsap";
~~~

### Sample 3

~~~html
<button type="button" data-play>Play animation</button>
<div class="box" aria-label="Orange animation box"></div>
~~~

### Sample 4

~~~css
.box {
  width: 80px;
  height: 80px;
  background: #e85b24;
  transform-origin: center;
}
~~~

### Sample 5

~~~js
import { gsap } from "gsap";

const boxAnimation = gsap.to(".box", {
  x: 220,
  rotation: 90,
  scale: 0.9,
  duration: 1,
  ease: "power2.out",
  paused: true,
});

document.querySelector("[data-play]").addEventListener("click", () => {
  boxAnimation.restart();
});
~~~

## Source chapter: [02. Targets, methods, and animation values](./02-targets-methods-and-animation-values.md)

### Sample 1

~~~js
import { gsap } from "gsap";

const cards = document.querySelectorAll(".card");

gsap.to(".notice", { opacity: 1, duration: 0.25 });
gsap.to(cards, { y: -8, duration: 0.3 });
~~~

### Sample 2

~~~js
import { gsap } from "gsap";

gsap.to(".to-card", {
  x: 80,
  opacity: 1,
  duration: 0.4,
});

gsap.from(".from-card", {
  y: 20,
  opacity: 0,
  duration: 0.4,
});

gsap.fromTo(
  ".from-to-card",
  { scale: 0.8, opacity: 0 },
  { scale: 1, opacity: 1, duration: 0.4 }
);
~~~

### Sample 3

~~~js
gsap.set(".panel", { x: 0, opacity: 1 });
gsap.to(".panel", { x: 120, duration: 0.5, ease: "power2.out" });
~~~

### Sample 4

~~~js
gsap.to(".box", {
  x: "+=40",
  rotation: "+=15",
  duration: 0.3,
});
~~~

### Sample 5

~~~js
const progress = { value: 0 };

gsap.to(progress, {
  value: 100,
  duration: 1,
  onUpdate: () => {
    console.log(Math.round(progress.value));
  },
});
~~~

## Source chapter: [03. Tween timing, repeats, and callbacks](./03-tween-timing-repeats-and-callbacks.md)

### Sample 1

~~~js
gsap.to(".notification", {
  y: 0,
  opacity: 1,
  duration: 0.35,
  delay: 0.2,
});
~~~

### Sample 2

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

### Sample 3

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

### Sample 4

~~~js
const tween = gsap.to(".meter", {
  x: 180,
  duration: 1,
  onUpdate: () => {
    console.log(tween.progress());
  },
});
~~~

### Sample 5

~~~js
gsap.to(".particle", {
  x: () => gsap.utils.random(-80, 80),
  y: () => gsap.utils.random(-40, 40),
  duration: 0.8,
  repeat: 3,
  repeatRefresh: true,
});
~~~

## Source chapter: [04. Eases and motion feel](./04-eases-and-motion-feel.md)

### Sample 1

~~~js
gsap.to(".card", {
  x: 160,
  duration: 0.5,
  ease: "power2.out",
});
~~~

### Sample 2

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

### Sample 3

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

## Source chapter: [05. Timelines, positions, and labels](./05-timelines-positions-and-labels.md)

### Sample 1

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

### Sample 2

~~~js
const sequence = gsap.timeline({ defaults: { duration: 0.5 } });

sequence
  .to(".first", { x: 100 })
  .to(".second", { x: 100 }, "+=0.2")
  .to(".third", { x: 100 }, "<")
  .to(".fourth", { x: 100 }, ">-0.15");
~~~

### Sample 3

~~~js
const story = gsap.timeline({ paused: true });

story
  .addLabel("heading")
  .from(".heading", { opacity: 0, y: 16, duration: 0.35 })
  .addLabel("details")
  .from(".details", { opacity: 0, duration: 0.25 }, "details");

story.play();
~~~

### Sample 4

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

## Source chapter: [06. Stagger and function-based values](./06-stagger-and-function-based-values.md)

### Sample 1

~~~js
gsap.to(".result-card", {
  y: 0,
  opacity: 1,
  duration: 0.35,
  ease: "power2.out",
  stagger: 0.08,
});
~~~

### Sample 2

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

### Sample 3

~~~js
gsap.to(".list-item", {
  x: (index) => index * 14,
  duration: 0.4,
  ease: "power1.out",
  stagger: 0.07,
});
~~~

### Sample 4

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

## Source chapter: [07. Controlling tweens and timelines](./07-controlling-tweens-and-timelines.md)

### Sample 1

~~~js
const panelTimeline = gsap.timeline({ paused: true });

panelTimeline
  .from(".panel-title", { y: 12, opacity: 0, duration: 0.25 })
  .from(".panel-body", { opacity: 0, duration: 0.2 });

document.querySelector("[data-play]").addEventListener("click", () => {
  panelTimeline.play();
});
~~~

### Sample 2

~~~html
<button type="button" data-play>Play</button>
<button type="button" data-reverse>Reverse</button>
<button type="button" data-restart>Restart</button>
~~~

### Sample 3

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

### Sample 4

~~~js
panelTimeline.seek(0.5);
console.log(panelTimeline.progress());
panelTimeline.timeScale(1.5);
~~~

### Sample 5

~~~js
const movement = gsap.to(".moving-card", {
  x: 120,
  duration: 1,
});

function stopAndRestore() {
  movement.revert();
}
~~~

## Source chapter: [08. Animating CSS and transforms](./08-animating-css-and-transforms.md)

### Sample 1

~~~js
gsap.to(".notice", {
  opacity: 1,
  backgroundColor: "#242424",
  borderColor: "#e85b24",
  duration: 0.3,
});
~~~

### Sample 2

~~~js
gsap.from(".dialog", {
  x: 24,
  y: 8,
  scale: 0.98,
  autoAlpha: 0,
  transformOrigin: "center",
  duration: 0.28,
  ease: "power2.out",
});
~~~

### Sample 3

~~~css
.progress {
  --progress: 0%;
  width: var(--progress);
  height: 6px;
  background: #e85b24;
}
~~~

### Sample 4

~~~js
gsap.to(".progress", {
  "--progress": "100%",
  duration: 0.8,
  ease: "power1.out",
});
~~~

### Sample 5

~~~js
gsap.to(".temporary-panel", {
  x: 120,
  opacity: 0,
  duration: 0.25,
  onComplete: () => {
    gsap.set(".temporary-panel", { clearProps: "transform,opacity" });
  },
});
~~~

## Source chapter: [09. Animating SVG and attributes](./09-animating-svg-and-attributes.md)

### Sample 1

~~~html
<svg viewBox="0 0 160 80" role="img" aria-labelledby="diagram-title">
  <title id="diagram-title">Circle moving along a path</title>
  <path d="M10 40 H150" stroke="#888" stroke-width="2" />
  <circle class="moving-dot" cx="10" cy="40" r="8" fill="#e85b24" />
</svg>
~~~

### Sample 2

~~~js
gsap.to(".moving-dot", {
  x: 140,
  duration: 0.7,
  ease: "power2.inOut",
});
~~~

### Sample 3

~~~js
gsap.to(".moving-dot", {
  attr: { cx: 150, r: 12 },
  duration: 0.5,
});
~~~

### Sample 4

~~~js
import { gsap } from "gsap";
import { DrawSVGPlugin } from "gsap/DrawSVGPlugin";

gsap.registerPlugin(DrawSVGPlugin);

gsap.set(".check-path", { drawSVG: "0%" });
gsap.to(".check-path", {
  drawSVG: "100%",
  duration: 0.65,
  ease: "power1.inOut",
});
~~~

### Sample 5

~~~html
<svg viewBox="0 0 48 48" aria-hidden="true">
  <path
    class="check-path"
    d="M8 25 L19 36 L40 11"
    fill="none"
    stroke="#e85b24"
    stroke-width="4"
    stroke-linecap="round"
    stroke-linejoin="round"
  />
</svg>
~~~

## Source chapter: [10. ScrollTrigger foundations](./10-scrolltrigger-foundations.md)

### Sample 1

~~~js
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
~~~

### Sample 2

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

### Sample 3

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

### Sample 4

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

### Sample 5

~~~js
ScrollTrigger.create({
  trigger: ".chapter",
  start: "top center",
  onEnter: () => console.log("Chapter entered"),
  onLeaveBack: () => console.log("Chapter left in reverse"),
});
~~~

## Source chapter: [11. ScrollTrigger scrub, pin, and snap](./11-scrolltrigger-scrub-pin-and-snap.md)

### Sample 1

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

### Sample 2

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

### Sample 3

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

## Source chapter: [12. Responsive animation with matchMedia](./12-responsive-animation-with-matchmedia.md)

### Sample 1

~~~js
const media = gsap.matchMedia();

media.add(
  {
    wide: "(min-width: 800px)",
    reduceMotion: "(prefers-reduced-motion: reduce)",
  },
  (context) => {
    const { wide, reduceMotion } = context.conditions;

    if (reduceMotion) {
      return;
    }

    gsap.from(".hero-art", {
      x: wide ? 80 : 20,
      opacity: 0,
      duration: wide ? 0.5 : 0.25,
    });
  }
);
~~~

### Sample 2

~~~js
const responsive = gsap.matchMedia();

responsive.add("(min-width: 900px)", () => {
  gsap.to(".desktop-decoration", {
    x: 120,
    rotation: 8,
    duration: 0.4,
  });
});

responsive.add("(max-width: 899px)", () => {
  gsap.set(".desktop-decoration", { clearProps: "all" });
});
~~~

### Sample 3

~~~js
const mediaSetup = gsap.matchMedia();

mediaSetup.add("(min-width: 700px)", () => {
  gsap.to(".feature", { y: -12, duration: 0.3 });
});

function removeFeature() {
  mediaSetup.revert();
}
~~~

## Source chapter: [13. GSAP in React with useGSAP](./13-gsap-in-react-with-usegsap.md)

### Sample 1

~~~sh
npm install gsap @gsap/react
~~~

### Sample 2

~~~jsx
import { gsap } from "gsap";
import { useGSAP } from "@gsap/react";

gsap.registerPlugin(useGSAP);
~~~

### Sample 3

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

### Sample 4

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

### Sample 5

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

## Source chapter: [14. Event-driven animation in React](./14-event-driven-animation-in-react.md)

### Sample 1

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

### Sample 2

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

### Sample 3

~~~css
.details {
  visibility: hidden;
  opacity: 0;
}
~~~

## Source chapter: [15. Accessibility and reduced motion](./15-accessibility-and-reduced-motion.md)

### Sample 1

~~~js
const motionPreference = gsap.matchMedia();

motionPreference.add(
  "(prefers-reduced-motion: no-preference)",
  () => {
    gsap.from(".intro-art", {
      y: 12,
      duration: 0.25,
      ease: "power1.out",
    });
  }
);
~~~

### Sample 2

~~~html
<button class="save-button" type="button">Save changes</button>
~~~

### Sample 3

~~~css
.save-button:focus-visible {
  outline: 3px solid #e85b24;
  outline-offset: 3px;
}
~~~

## Source chapter: [16. Performance, testing, and release checks](./16-performance-testing-and-release-checks.md)

### Sample 1

~~~js
const moveToX = gsap.quickTo(".cursor-marker", "x", {
  duration: 0.2,
  ease: "power2.out",
});

function handlePointerMove(event) {
  moveToX(event.clientX);
}

window.addEventListener("pointermove", handlePointerMove);

// Remove this listener when the feature is removed.
function cleanup() {
  window.removeEventListener("pointermove", handlePointerMove);
}
~~~

### Sample 2

~~~js
image.addEventListener("load", () => {
  ScrollTrigger.refresh();
});
~~~

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Performance, testing, and release checks](./16-performance-testing-and-release-checks.md) | [Notes index](../README.md) | [Next: Complete questions and answers](./99-complete-q-and-a.md) |

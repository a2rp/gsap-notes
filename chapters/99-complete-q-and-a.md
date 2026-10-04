# 99. Complete questions and answers

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: All code samples](./98-all-code-samples.md) | [Notes index](../README.md) | End of notes |

## 01. [01. GSAP setup and first tween](./01-gsap-setup-and-first-tween.md)

### Question 1: Which package does the installation example add?

**Answer:** It adds the gsap package from npm.

### Question 2: How is the gsap object imported in a JavaScript module?

**Answer:** Use the named import: import { gsap } from "gsap".

### Question 3: Which kinds of targets can GSAP animate?

**Answer:** GSAP can animate selector matches, DOM elements, arrays of elements, and numeric properties on plain JavaScript objects.

### Question 4: What does gsap.to use as its starting values?

**Answer:** gsap.to starts from the target values currently rendered in the page.

### Question 5: What units does duration use?

**Answer:** duration is measured in seconds.

### Question 6: What do x, rotation, and scale represent in the example?

**Answer:** They control horizontal movement, rotation, and size scaling through transform properties.

### Question 7: What does gsap.to return?

**Answer:** It returns a Tween instance that can be stored and controlled.

### Question 8: Why does the example keep the button semantic and the initial box visible?

**Answer:** A semantic button works with keyboard input, and a visible starting box keeps the content available before motion runs.

## 02. [02. Targets, methods, and animation values](./02-targets-methods-and-animation-values.md)

### Question 1: Which target types can GSAP animate?

**Answer:** Targets can be CSS selectors, individual DOM elements, arrays of elements, and plain JavaScript objects.

### Question 2: What happens when a selector matches several elements?

**Answer:** GSAP applies the tween to each matching element.

### Question 3: How does gsap.to choose its starting values?

**Answer:** gsap.to reads the target current rendered values and animates toward the values in the vars object.

### Question 4: What does gsap.from animate toward?

**Answer:** gsap.from starts at the values in its vars object and animates back to the targets current rendered values.

### Question 5: When is gsap.fromTo useful?

**Answer:** Use gsap.fromTo when the animation needs an explicit start and end value.

### Question 6: What does gsap.set do?

**Answer:** gsap.set applies values immediately as a zero-duration change.

### Question 7: How does a relative value such as x: "+=40" behave?

**Answer:** It adds 40 to the current x value instead of always moving to the same absolute x position.

### Question 8: Why should an onUpdate callback stay lightweight?

**Answer:** onUpdate can run many times per second, so heavy work can slow the interface.

## 03. [03. Tween timing, repeats, and callbacks](./03-tween-timing-repeats-and-callbacks.md)

### Question 1: Which unit does duration use?

**Answer:** duration uses seconds.

### Question 2: What does delay change?

**Answer:** delay sets how long GSAP waits before the first play begins.

### Question 3: How many total plays does repeat: 2 produce?

**Answer:** It produces three plays: the original play and two repeats.

### Question 4: What does yoyo do between repeats?

**Answer:** yoyo makes alternate repeat cycles travel back toward the starting values.

### Question 5: When can repeatDelay be useful?

**Answer:** repeatDelay adds a pause between cycles, which can make a repeated status effect easier to read.

### Question 6: Which lifecycle events can callbacks observe?

**Answer:** Callbacks can observe start, update, repeat, completion, and reverse completion events.

### Question 7: Why should an onUpdate callback avoid heavy work?

**Answer:** It can run every animation frame, so expensive computation or rendering can cause dropped frames.

### Question 8: What does repeatRefresh recalculate?

**Answer:** repeatRefresh invalidates and recalculates function-based values for each repeat.

## 04. [04. Eases and motion feel](./04-eases-and-motion-feel.md)

### Question 1: What does an ease control?

**Answer:** An ease controls the speed curve between the starting and ending values.

### Question 2: Does changing ease change the target value?

**Answer:** No. Ease changes timing feel, not the destination value.

### Question 3: How does power2.out change speed?

**Answer:** power2.out starts quickly and slows as it reaches the destination.

### Question 4: How does power2.in differ from power2.out?

**Answer:** power2.in starts gradually and accelerates, while power2.out starts quickly and decelerates.

### Question 5: Which ease families can create overshoot or oscillation?

**Answer:** Back, elastic, and bounce families can create overshoot or oscillation.

### Question 6: When can an overshoot ease be a poor choice?

**Answer:** Overshoot can make a small control feel imprecise or playful when the interface should feel calm and direct.

### Question 7: Which ease is used for the sample entrance and why?

**Answer:** The entrance example uses power2.out to arrive quickly and settle gently.

### Question 8: How is duration different from ease?

**Answer:** Duration is the total time in seconds; ease defines how speed changes during that time.

## 05. [05. Timelines, positions, and labels](./05-timelines-positions-and-labels.md)

### Question 1: What does a GSAP timeline coordinate?

**Answer:** A timeline coordinates the playback and timing of multiple tweens on one playhead.

### Question 2: Where does the second child tween start by default?

**Answer:** It starts after the first child tween finishes unless a position is supplied.

### Question 3: What does a numeric position value mean?

**Answer:** A numeric position is an absolute time in seconds on the timeline.

### Question 4: What does "+=0.2" do?

**Answer:** It places the tween 0.2 seconds after the current end of the timeline.

### Question 5: What does the less-than position token mean?

**Answer:** The less-than token starts the tween at the start time of the previous tween.

### Question 6: How can a tween start shortly before the previous tween ends?

**Answer:** Use a position such as >-0.15 to start it 0.15 seconds before the previous tween ends.

### Question 7: Why add labels to a timeline?

**Answer:** Labels name important timeline moments so tweens and controls can refer to them clearly.

### Question 8: How can a child tween override timeline defaults?

**Answer:** Set that property directly on the child tween; its explicit value overrides the shared default.

## 06. [06. Stagger and function-based values](./06-stagger-and-function-based-values.md)

### Question 1: What does stagger change for a group of targets?

**Answer:** Stagger offsets the start time for each target in a group.

### Question 2: How does stagger: 0.08 place the start times?

**Answer:** Each target starts 0.08 seconds after the previous target.

### Question 3: What does the from option choose?

**Answer:** from chooses which target or region begins the stagger, such as the center or last item.

### Question 4: What does grid: "auto" ask GSAP to do?

**Answer:** It asks GSAP to infer the grid arrangement from the positions of the targets.

### Question 5: Which arguments can a function-based value receive?

**Answer:** A function-based value can receive the target index, target element, and full target array.

### Question 6: How can an index create a different value for each target?

**Answer:** Use the index in a calculation, such as x: index => index * 14.

### Question 7: When can a timeline be useful alongside stagger?

**Answer:** A timeline can coordinate the staggered group with an entrance before it or another animation after it.

### Question 8: Why should function-based values usually be predictable?

**Answer:** Predictable values make an animation easier to understand and produce consistent results on repeated runs.

## 07. [07. Controlling tweens and timelines](./07-controlling-tweens-and-timelines.md)

### Question 1: What does gsap.to return?

**Answer:** gsap.to returns a Tween instance.

### Question 2: What does paused: true do on a timeline?

**Answer:** It creates the timeline without starting playback, so a later event can control it.

### Question 3: How do play and reverse differ?

**Answer:** play moves the playhead toward the end; reverse moves it toward the start.

### Question 4: What does restart do?

**Answer:** restart returns the playhead to the beginning and plays again.

### Question 5: What values can seek accept?

**Answer:** seek accepts an absolute time in seconds or a timeline label.

### Question 6: What range does progress report?

**Answer:** progress reports normalized progress from zero to one.

### Question 7: How does timeScale change playback speed?

**Answer:** A timeScale of 1 is normal speed, less than 1 is slower, and greater than 1 is faster.

### Question 8: What is the difference between kill and revert?

**Answer:** kill stops and removes the animation but may leave its current inline styles; revert also restores the pre-animation styles.

## 08. [08. Animating CSS and transforms](./08-animating-css-and-transforms.md)

### Question 1: Which types of CSS properties can GSAP animate?

**Answer:** GSAP can animate numeric CSS values, opacity, colors, transforms, and many other compatible style properties.

### Question 2: Why can an explicit unit such as px or percent help?

**Answer:** An explicit unit clarifies how the value should be interpreted, especially when a property has no useful unit to infer.

### Question 3: Name four GSAP transform properties.

**Answer:** Examples include x, y, scale, and rotation.

### Question 4: What does autoAlpha combine?

**Answer:** autoAlpha combines opacity and visibility.

### Question 5: Why can autoAlpha require care when content has keyboard focus?

**Answer:** An element made invisible can still contain keyboard focus, so focus should be moved safely before hiding it.

### Question 6: How can GSAP animate a CSS custom property?

**Answer:** Define the property in CSS and tween it with its custom property name, such as "--progress".

### Question 7: What does clearProps do?

**Answer:** clearProps removes selected inline properties so the stylesheet can control their final appearance.

### Question 8: How does animating height differ from animating a transform for document flow?

**Answer:** Changing height affects layout and can move surrounding content; a transform moves the element visually without changing document flow.

## 09. [09. Animating SVG and attributes](./09-animating-svg-and-attributes.md)

### Question 1: How can GSAP select an inline SVG element?

**Answer:** Use a CSS selector, an element reference, or a collection of inline SVG elements.

### Question 2: What does viewBox define?

**Answer:** viewBox defines the SVG coordinate system and how it scales into the rendered viewport.

### Question 3: Which transform shortcuts can move or rotate an SVG shape?

**Answer:** Properties such as x, y, rotation, and scale can move or turn an SVG shape.

### Question 4: When should an SVG attribute be placed under attr?

**Answer:** Use attr when animating an SVG geometry attribute such as cx, cy, or r.

### Question 5: Which plugin can reveal part of an SVG stroke?

**Answer:** DrawSVGPlugin can animate the visible portion of an SVG stroke.

### Question 6: What should an SVG path have for a line-drawing effect?

**Answer:** It needs a visible stroke, and fill="none" is common for a line drawing.

### Question 7: How should an informative SVG be named for assistive technology?

**Answer:** Give it a title or another accessible name, or use aria-hidden when it is decorative.

### Question 8: When should an optional SVG plugin be added?

**Answer:** Add one when the desired effect needs that feature; use core GSAP when it already handles the task.

## 10. [10. ScrollTrigger foundations](./10-scrolltrigger-foundations.md)

### Question 1: Which package module exports ScrollTrigger?

**Answer:** Import it from gsap/ScrollTrigger.

### Question 2: What does gsap.registerPlugin do?

**Answer:** It registers the imported plugin with GSAP so its features are available and bundlers retain the plugin.

### Question 3: What does the trigger option identify?

**Answer:** It identifies the element whose position controls the trigger measurements.

### Question 4: How is start: "top 82%" interpreted?

**Answer:** The trigger top edge meets a point 82 percent down from the top of the viewport.

### Question 5: In what order does toggleActions list its four behaviors?

**Answer:** The order is onEnter, onLeave, onEnterBack, then onLeaveBack.

### Question 6: What does once: true do?

**Answer:** It runs the trigger once on entry and then disables that one-time trigger.

### Question 7: Why use markers during development?

**Answer:** Markers show the measured start and end boundaries so they are easier to tune.

### Question 8: Why should essential content remain available before an entrance animation runs?

**Answer:** Users may not scroll or animation code may fail, so essential information must already be present in the page.

## 11. [11. ScrollTrigger scrub, pin, and snap](./11-scrolltrigger-scrub-pin-and-snap.md)

### Question 1: What does scrub connect?

**Answer:** scrub connects the animation playhead to the users scroll position.

### Question 2: How does scrub: 0.5 differ from scrub: true?

**Answer:** scrub: true follows scroll position directly; a number adds smoothing so the playhead catches up over that time.

### Question 3: What does pin do during a trigger range?

**Answer:** pin holds the trigger element in place for part of the configured scroll range.

### Question 4: Why should content inside a pinned section be animated instead of the pinned trigger itself?

**Answer:** Animating the pinned trigger can affect ScrollTrigger measurements; animate its children instead.

### Question 5: How can nested pins complicate a page?

**Answer:** Nested pins affect measurements and spacing, making the scroll range harder to predict.

### Question 6: What does snap do after scrolling stops?

**Answer:** snap moves scroll progress to a chosen landing point after scrolling settles.

### Question 7: Why is 1 / 3 used for four evenly spaced panels?

**Answer:** Four panels have three intervals between them, so 1 / 3 divides progress into three equal steps.

### Question 8: Which input methods should be tested when snapping is enabled?

**Answer:** Test touch, wheel, trackpad, and keyboard scrolling because snapping changes where scrolling settles.

## 12. [12. Responsive animation with matchMedia](./12-responsive-animation-with-matchmedia.md)

### Question 1: What does gsap.matchMedia observe?

**Answer:** It observes media queries such as viewport width and reduced-motion preference.

### Question 2: What does the callback context provide?

**Answer:** The callback context exposes the named conditions and whether each one currently matches.

### Question 3: When are GSAP animations created in a matchMedia callback reverted?

**Answer:** GSAP animations and ScrollTriggers created in that callback are reverted when its query stops matching.

### Question 4: How can reduced motion affect the animation setup?

**Answer:** Skip large movement, use a smaller effect, or provide no animation when reduced motion is requested.

### Question 5: Why might a mobile layout need a separate animation choice?

**Answer:** A narrow layout may have different spacing, content order, or available room, so desktop values may not fit.

### Question 6: What does matchMedia object's revert method do?

**Answer:** It reverts animations and media-query setups created by that matchMedia instance.

### Question 7: Which non-GSAP resources still need their own cleanup?

**Answer:** DOM event listeners and other resources not created as GSAP animations still need their own cleanup.

### Question 8: Why should ScrollTrigger positions be checked after a breakpoint change?

**Answer:** A breakpoint can change layout dimensions and element positions used for trigger measurements.

## 13. [13. GSAP in React with useGSAP](./13-gsap-in-react-with-usegsap.md)

### Question 1: Which package adds the GSAP React integration?

**Answer:** The @gsap/react package adds the useGSAP hook.

### Question 2: Why register useGSAP with GSAP?

**Answer:** Registration helps bundlers keep the hook and avoids loading conflicting copies of the integration.

### Question 3: What does the scope ref limit?

**Answer:** It limits selector strings in the hook callback to elements inside the referenced component.

### Question 4: How does useGSAP clean up animations?

**Answer:** The hook uses a GSAP context to collect animations and revert them when the component is removed.

### Question 5: When should dependencies be passed to useGSAP?

**Answer:** Pass dependencies when animation setup must run again after relevant React data changes.

### Question 6: What does revertOnUpdate do?

**Answer:** It reverts the previous animation setup before the hook callback runs again for changed dependencies.

### Question 7: Why wrap a later event handler with contextSafe?

**Answer:** It makes animations created later by the handler part of the hook context so they are cleaned up with the component.

### Question 8: Which responsibilities should remain with React?

**Answer:** React should render content, own application state, and decide whether components exist; GSAP handles visual timing.

## 14. [14. Event-driven animation in React](./14-event-driven-animation-in-react.md)

### Question 1: Why use React event props for button actions?

**Answer:** React event props connect actions to click, keyboard activation, and other browser input consistently.

### Question 2: What does contextSafe do for a later event-created tween?

**Answer:** It adds later-created animations to the current GSAP context for cleanup and selector scoping.

### Question 3: Why does the example scope selectors to a component ref?

**Answer:** The ref confines selectors to the component instance and prevents matching unrelated elements elsewhere.

### Question 4: When should React state choose the animation target?

**Answer:** Use React state when an action changes what the interface means or which content should be visible.

### Question 5: Why should a disclosure's aria-expanded value match its visible state?

**Answer:** The accessibility state must describe what users can actually see and operate.

### Question 6: Why should gsap.to not run directly in the component body?

**Answer:** Rendering may happen repeatedly; creating a tween in the component body can duplicate or restart animations.

### Question 7: What does overwrite: "auto" help manage?

**Answer:** It replaces conflicting active tweens on the same target properties.

### Question 8: Why should hover not be the only way to trigger an important response?

**Answer:** Keyboard and touch users may not hover, so important behavior needs another reachable input.

## 15. [15. Accessibility and reduced motion](./15-accessibility-and-reduced-motion.md)

### Question 1: Which media feature represents the reduced-motion preference?

**Answer:** The prefers-reduced-motion media feature represents that preference.

### Question 2: How does the example decide whether to add movement?

**Answer:** It creates the entrance movement only when the no-preference query matches.

### Question 3: Why should content start visible before the animation?

**Answer:** Visible content remains understandable even if animation does not run or the user avoids motion.

### Question 4: Which HTML element is appropriate for a save action?

**Answer:** A native button is appropriate for a save action.

### Question 5: What does :focus-visible style?

**Answer:** :focus-visible styles an element when it has keyboard-style focus that should be shown.

### Question 6: Why should motion not be the only signal for a result?

**Answer:** Users may not see, tolerate, or have motion enabled, so text or semantic state must also explain the result.

### Question 7: What should happen to focus when a panel closes?

**Answer:** Move focus to a visible control outside the panel before hiding the focused content.

### Question 8: Which user settings and input methods should be tested?

**Answer:** Test reduced-motion settings, keyboard navigation, zoom, touch input, and narrow layouts.

## 16. [16. Performance, testing, and release checks](./16-performance-testing-and-release-checks.md)

### Question 1: Why are transforms and opacity often preferred for frequent animation?

**Answer:** Transforms and opacity can often update without recalculating page layout, reducing repeated rendering work.

### Question 2: When can animating width or height still be the right choice?

**Answer:** It is right when surrounding content should reflow and performance remains acceptable with realistic content.

### Question 3: What does gsap.quickTo help avoid?

**Answer:** It reuses a tween for frequent value changes instead of creating a new tween for every event.

### Question 4: Why should high-frequency event listeners be cleaned up?

**Answer:** Listeners retain references and can keep running after a feature is removed, causing stale behavior or extra work.

### Question 5: When should ScrollTrigger.refresh be called?

**Answer:** Call it after meaningful layout changes, such as content insertion or image loading, once positions are ready.

### Question 6: Which performance signs should be checked in browser tools?

**Answer:** Check dropped frames, long tasks, layout shifts, and repeated layout or rendering work.

### Question 7: What should be checked after images and fonts load?

**Answer:** Confirm trigger positions, page spacing, content wrapping, and animation behavior after the layout settles.

### Question 8: Which items belong in a final release check?

**Answer:** Check reduced motion, keyboard focus, control behavior, layout stability, listener cleanup, plugin registration, and the production build.

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: All code samples](./98-all-code-samples.md) | [Notes index](../README.md) | End of notes |

# 01. GSAP setup and first tween

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: Targets, methods, and animation values](./02-targets-methods-and-animation-values.md) |

## Install GSAP

GSAP is a JavaScript animation library. In a project that uses npm, add the core package:

~~~sh
npm install gsap
~~~

In a JavaScript module, import the gsap object:

~~~js
import { gsap } from "gsap";
~~~

The same package can be used with a build tool or loaded in a browser in other ways. Use the project package manager and follow its module format. These notes use JavaScript modules.

## Prepare an element to animate

GSAP can target a selector, an element, or a collection of elements. Start with one element and give it a clear initial layout.

~~~html
<button type="button" data-play>Play animation</button>
<div class="box" aria-label="Orange animation box"></div>
~~~

~~~css
.box {
  width: 80px;
  height: 80px;
  background: #e85b24;
  transform-origin: center;
}
~~~

Keep the button in normal document flow and animate the box. GSAP writes the animation styles to the target element.

## Create the first tween

A tween changes one or more properties over time. gsap.to starts from the element's current rendered values and moves it toward the values in the vars object.

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

x, rotation, and scale are GSAP transform properties. They are easier to compose than manually replacing the full CSS transform string. duration is measured in seconds. ease controls how the movement changes speed over that time.

The tween is paused when it is created. Clicking the button restarts it from the beginning. This keeps the effect tied to an actual user action rather than starting before the interface is ready.

## Understand what gsap.to returns

gsap.to returns a Tween object. Keep it in a variable when the interface needs to restart, pause, reverse, or inspect the animation later. If no later control is needed, the call can be written without storing the return value.

Use a selector that identifies only the intended elements. A broad selector can animate unrelated parts of a page that happen to use the same class.

## Check the result

The button remains a real button and can be activated with a keyboard. The box is still visible before interaction, and its movement provides feedback after the user asks for it.

When an animation does not appear, check that the target exists, the module ran after the markup was created, and no later CSS rule overwrote the animated property.

## Practice questions

1. Which package does the installation example add?
2. How is the gsap object imported in a JavaScript module?
3. Which kinds of targets can GSAP animate?
4. What does gsap.to use as its starting values?
5. What units does duration use?
6. What do x, rotation, and scale represent in the example?
7. What does gsap.to return?
8. Why does the example keep the button semantic and the initial box visible?

## Main references

- [GSAP installation](https://gsap.com/docs/v3/Installation/)
- [GSAP core](https://gsap.com/docs/v3/GSAP/)
- [gsap.to()](https://gsap.com/docs/v3/GSAP/gsap.to/)
- [Tween](https://gsap.com/docs/v3/GSAP/Tween/)
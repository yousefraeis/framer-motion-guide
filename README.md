<div style="text-align: center;">
  <img src="./framer-motion.webp" />
</div>

# Mastering Animations with **Framer Motion**: A Step-by-Step Guide for Beginners

## **Introduction to Framer Motion** ✨

Welcome to the world of **Framer Motion**, a powerful animation library for React that helps you create smooth, interactive animations with ease. Whether you’re a beginner or an experienced developer, this guide will walk you through the basics and advanced techniques to help you animate your UI components and make your web applications more engaging.

In this guide, we will explore different animation techniques using Framer Motion, starting from simple animations like hover effects, all the way to complex animations using **variants**, **keyframes**, and more. Let’s get started!

<br/>

---

<br/>

### Tutorial 1: First Steps in Framer Motion 👣

#### Basic Structure:

```html
<div></div>
<motion.div></motion.div>
```

#### Animating with Motion 🎬:

-   **`initial={{}}`**: Sets the starting position (like `0%` in CSS animations).
-   **`animate={{}}`**: Sets the final position (like `100%` in CSS animations).

#### Common Properties:

-   **`translateX`**: Moves the element horizontally (e.g., `x: 20` moves 20 pixels).
-   **`opacity`**: Changes how see-through the element is.
-   **`rotate`**: Rotates the element.

You can use any CSS property in `motion.div`.

#### Changing Starting Position 🔄:

-   Use `initial={{}}` to set where the animation starts.

#### Animation Properties:

-   **`initial`**: The starting state of the element.
-   **`animate`**: The ending state of the element.
-   **`transition`**: Controls how long the animation lasts. Example: `transition={{ duration: 1 }} ` (for 1 second).

#### Example Code:

```jsx
import { motion } from 'framer-motion';

function Example() {
    return (
        <motion.div
            initial={{ opacity: 0, x: -100 }} // Start invisible and to the left
            animate={{ opacity: 1, x: 0 }} // End fully visible and at the original position
            transition={{ duration: 2 }} // Animation lasts 2 seconds
        >
            Hello, I will animate! ✨
        </motion.div>
    );
}

export default Example;
```

<br/>

---

<br/>

### Tutorial 2: **Making Elements Disappear with Style `exit={{}}`** 🚪

In **Framer Motion**, when an element is removed from the screen, you can make it animate out using the `exit={{}}` property. This is useful for animating an element when it disappears. 👋

#### Example:

Let's say you want to hide a button after 5 seconds, but before it disappears, you want it to animate out.

```jsx
import { motion, AnimatePresence } from 'framer-motion';
import { useState, useEffect } from 'react';

const App = () => {
    const [show, setShow] = useState(true);

    useEffect(() => {
        setTimeout(() => {
            setShow(false); // After 5 seconds, hide the button
        }, 5000);
    }, []);

    return (
        <div>
            <AnimatePresence>
                {' '}
                {/* Wrap the element with AnimatePresence */}
                {show && (
                    <motion.button
                        exit={{ opacity: 0, x: 200 }} // Animate out when the button disappears
                    >
                        Click Me! 👆
                    </motion.button>
                )}
            </AnimatePresence>
        </div>
    );
};

export default App;
```

### Why it doesn't work without `AnimatePresence`:

-   **`AnimatePresence`** is needed to handle the exit animations properly when elements are conditionally removed (like when `show` is set to `false`).
-   Without it, the exit animation won't be triggered, and the element will simply disappear without any animation. ❌

#### Key Points:

-   **`exit={{}}`**: Specifies how an element should animate when it is removed.
-   **`AnimatePresence`**: Must wrap the elements that will use exit animations to ensure they animate properly when removed from the DOM.

---

### Using the `transition` Property ⏳:

```jsx
<motion.div
    initial={{ x: 100 }} // Start position (off the right)
    animate={{ x: 0 }} // End position (original place)
    transition={{
        delay: 2, // Wait 2 seconds before starting the animation
        duration: 2, // The animation will take 2 seconds to complete
        type: 'spring', // Use spring physics for the animation
        stiffness: 100, // Controls how fast the spring moves
        damping: 20, // Controls how the spring slows down
        mass: 1, // Controls the weight of the spring (higher = slower, lower = faster)
    }}
>
    Hello, I animate with spring! 🌱
</motion.div>
```

<br/>

---

<br/>

### Tutorial 3: Explanation of the `transition` Settings 🔧

1. **`delay`**:

    - The animation will start **after a certain delay**. For example, `delay: 2` means the animation will not start until **2 seconds** have passed. ⏰

2. **`duration`**:

    - This defines how long the animation will take. For example, `duration: 2` means the animation will take **2 seconds** to finish.

3. **`type`**:

    - Controls the style of the animation.
        - **`tween`** (default): The animation moves at a **constant speed** (linear).
        - **`spring`**: The animation behaves like a **spring**, going past the target and then returning to it, like bouncing. 🏀

4. **Spring properties**:

    - **`mass`**: Controls how "heavy" the spring is.
        - A higher mass (e.g., `mass: 2`) means the animation moves **slower**.
        - A lower mass (e.g., `mass: 0.1`) makes the animation **faster**, similar to `tween`.

    - **`damping`**: Controls how much the animation **slows down** towards the end. A higher damping value means the animation stops more quickly, while a lower damping value means the animation **vibrates** or takes longer to stop.

    - **`stiffness`**: Determines how **tight** the spring is.
        - Higher stiffness makes the animation move **quicker** and **sharper**.
        - Lower stiffness makes the animation more **sluggish** or less responsive.

---

### Example with `spring` type 🏃‍♂️:

If you set the type to `"spring"`, the animation will look like a bouncing effect, where it overshoots its target and then returns to the final position.

---

### Explaining **stiffness** and **damping** 💡:

### 1. **Stiffness**:

-   **Stiffness** is how strong or tight the spring is.
    -   **High stiffness**: The spring moves **quickly** to its final position. It feels **strong**.
    -   **Low stiffness**: The spring moves **slowly** to its final position. It feels **weak**.

**Example**:

-   Think of a **tight rubber band** (high stiffness). It will snap back quickly.
-   Now, think of a **loose rubber band** (low stiffness). It moves more slowly and doesn't snap back as fast.

### 2. **Damping**:

-   **Damping** is how quickly the spring stops moving after it is stretched or moved.
    -   **High damping**: The spring **stops quickly** and doesn't bounce much.
    -   **Low damping**: The spring **bounces more** before it stops.

**Example**:

-   Imagine a **shock absorber** on a car (high damping). It stops the car from bouncing quickly.
-   Now, imagine a **trampoline** (low damping). It bounces up and down a few times before stopping.

### Simple Summary:

-   **High Stiffness** = Fast movement (like a tight rubber band).
-   **Low Stiffness** = Slow movement (like a loose rubber band).
-   **High Damping** = Stops quickly (like a car shock absorber).
-   **Low Damping** = Bounces more before stopping (like a trampoline).

This is how the spring moves based on stiffness and damping! 🌱

<br/>

---

<br/>

### Tutorial 4: Interactive Animations with Framer Motion: Hover, Tap, Drag, and Scroll Effects 🎮

### 1. **whileHover={{}}** 🖱️

-   This property is used to apply animations when you **hover** over an element.
-   Example: Change the size of a button when you hover over it.

```jsx
<motion.div whileHover={{ scale: 1.2 }}>Hover over me!</motion.div>
```

### 2. **whileTap={{}}** 👆

-   This property triggers animations when the element is **clicked** or **tapped**.
-   Example: The element scales down when you click on it.

```jsx
<motion.div whileTap={{ scale: 0.8 }}>Tap me!</motion.div>
```

### 3. **whileFocus={{}}** 🔲

-   This property is mainly used with **input fields**. It triggers when the input field **gains focus** (e.g., when clicked on or selected).
-   Example: Change the border color when the input is focused.

```jsx
<motion.input whileFocus={{ borderColor: 'blue' }} />
```

### 4. **whileDrag={{}}** 🖱️

-   This property is used when you **drag** an element (move it around).
-   Example: Scale the element up slightly when you drag it.

```jsx
<motion.div whileDrag={{ scale: 1.2 }} drag="x">
    Drag me horizontally!
</motion.div>
```

-   `drag="x"` makes the element move **horizontally** (along the x-axis). You can also use `drag="y"` for vertical drag or `drag` for free dragging in both directions.

### 5. **dragConstraints={{}}** ⛔

-   This defines the **boundary** where the element can be dragged. For example, you can set the limits for how far the element can move.

```jsx
<motion.div drag="x" dragConstraints={{ left: 0, right: 100 }}>
    Drag me between 0 and 100!
</motion.div>
```

-   The element can only be dragged from **0 to 100** along the x-axis (horizontally).

### 6. **whileInView={{}}** 👀

-   This property triggers an animation when the element **comes into view** on the screen (for example, when you scroll down the page).
-   Example: Animate a button when it scrolls into view.

```jsx
<motion.button whileInView={{ opacity: 1 }} initial={{ opacity: 0 }}>
    Scroll down to see me!
</motion.button>
```

-   The button will appear when it **comes into the browser view** (like when you scroll down), and you can define animations for it.

---

### Quick Summary: ✨

-   **whileHover**: Animates when you hover over the element.
-   **whileTap**: Animates when you click on the element.
-   **whileFocus**: Animates when an input field gains focus.
-   **whileDrag**: Animates while you drag the element.
-   **dragConstraints**: Limits the dragging movement to a specific range.
-   **whileInView**: Triggers an animation when the element comes into view (like when scrolling).

<br/>

---

<br/>


### Tutorial 5: Using **Variants** in **Framer Motion** to Help Clean Up Your Code and Make Animations Easier to Manage ✨

### What are **Variants**? 🔄

Variants in **Framer Motion** help you define multiple animation states and then use them across your elements in a more organized way. This makes your code cleaner and easier to manage.

### 1. **Defining Variants** 🖋️

You can define the animation states for an element using **variants**. For example:

```javascript
const btnVariant = {
    hidden: { x: 100 }, // Start position (hidden state)
    visible: { x: 0, transition: { duration: 0.5 } }, // End position (visible state with 0.5 second transition)
};
```

### 2. **Using Variants in Components** 🎨

Once you’ve defined a variant, you can apply it to your components using the `variants` prop.

Example:

```jsx
<motion.button
    variants={btnVariant} // Apply the defined variants
    initial="hidden" // Start in the "hidden" state
    animate="visible" // Animate to the "visible" state
>
    Click Me!
</motion.button>
```

-   `initial="hidden"`: The element starts in the **hidden** state.
-   `animate="visible"`: The element animates to the **visible** state.

### 3. **Parent and Child Variants** 👨‍👩‍👧‍👦

If you have parent and child elements, you can use **parent variants** to control the timing and order of animations for the children.

#### Parent Variants 🌱:

You can define animation for both the parent and the children and control their order.

```javascript
const parentVariant = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { duration: 1 } },
};
```

#### Child Variants 🧸:

You can define animations for child elements as well, with delays or staggered timings.

```javascript
const childVariant = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { duration: 0.5 } },
};
```

### 4. **Parent Variants Control Timing** ⏰

The parent variant controls how child animations play. You can use the following properties:

-   **`beforeChildren`**: The parent animation will finish before the children's animations start.
-   **`afterChildren`**: The parent animation will start after the children's animations finish.
-   **`delayChildren`**: You can set a delay before the children start animating.
-   **`staggerChildren`**: Adds a delay between each child’s animation (like staggered text).

Example with `staggerChildren`:

```javascript
const parentVariant = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { duration: 1, staggerChildren: 0.5 } },
};
```

In this example, each child will animate 0.5 seconds apart.

### 5. **Example with Parent and Child Variants** 🏠👶

```jsx
const parentVariant = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { duration: 1, staggerChildren: 0.5 } },
};

const childVariant = {
    hidden: { opacity: 0 },
    visible: { opacity: 1, transition: { duration: 0.5 } },
};

function Example() {
    return (
        <motion.div variants={parentVariant} initial="hidden" animate="visible">
            <motion.h1 variants={childVariant}>Child 1</motion.h1>
            <motion.h1 variants={childVariant}>Child 2</motion.h1>
            <motion.h1 variants={childVariant}>Child 3</motion.h1>
        </motion.div>
    );
}
```

### Key Points: 📌

-   **Variants** help organize animations and make your code cleaner.
-   **Parent variants** control when children start and how their animations behave.
-   You can use **`staggerChildren`** to add a delay between child animations.

With variants, you can manage complex animations in a much more structured and readable way! 🧹

<br/>

---

<br/>


### Tutorial 6: Explaining **Keyframes** and How to Use Them in **Framer Motion** 🔄, Along with Repeat Options and Repeat Types 🔁

### 1. **Keyframes** in Framer Motion:

Keyframes let you define multiple values for an animation at different points in time. For example, you can make an element move and change its size in a sequence.

#### Example:

```jsx
<motion.div
    initial={{ x: [0, 100, 0], scale: [1, 2, 1] }} // Define the keyframe values for initial state
    animate={{ x: [0, 100, 0], scale: [1, 2, 1] }} // Define the keyframe values for animate state
    transition={{ duration: 2 }} // Define how long the animation takes
>
    Animated with keyframes!
</motion.div>
```

-   **`x: [0, 100, 0]`**: This means the element starts at position 0, moves to 100, and then returns back to 0.
-   **`scale: [1, 2, 1]`**: The element starts with a scale of 1, grows to 2, and then returns back to 1.

### 2. **Repeat Animation** 🔄:

You can make the animation repeat a certain number of times or indefinitely.

#### Example for Repeat:

```jsx
<motion.div
    initial={{ x: [0, 100, 0], scale: [1, 2, 1] }}
    animate={{ x: [0, 100, 0], scale: [1, 2, 1] }}
    transition={{
        duration: 2,
        repeat: Infinity, // Animation repeats indefinitely
        repeatType: 'loop', // The animation loops back to the start
    }}
>
    Repeating Animation
</motion.div>
```

-   **`repeat: Infinity`**: The animation will repeat forever.
-   **`repeat: 3`**: The animation will repeat 3 times.

### 3. **Repeat Types** 🔁:

You can control how the animation repeats using the `repeatType` property. The available options are:

-   **`reverse`**: The animation will reverse after each repeat.
    -   Example: **1 → 2 → 1 → 2 → 1 → 2** (it repeats back and forth).
-   **`mirror`**: The animation plays forwards and then **mirrors** itself in reverse, starting from the end.
    -   Example: **1 → 2 → 1 → 0 → 1 → 2** (starts and ends in reverse).
-   **`loop`**: The animation simply **loops**, playing the same sequence again and again.
    -   Example: **1 → 2 → 1 → 2 → 1 → 2** (loops from the start).

#### Example with `repeatType`:

```jsx
<motion.div
    initial={{ x: [0, 100, 0], scale: [1, 2, 1] }}
    animate={{ x: [0, 100, 0], scale: [1, 2, 1] }}
    transition={{
        duration: 2,
        repeat: 3, // Repeat 3 times
        repeatType: 'reverse', // Reverse the animation each time
    }}
>
    Animation with Reverse Repeat
</motion.div>
```

### 4. **Is `repeat` Used Only in Transitions?** 🧐

-   Yes, the `repeat` property is used in the **`transition`** of the animation to define how many times it should repeat and what type of repetition should happen. You can’t use `repeat` outside of a `transition` property.

---

### Summary 📌:

-   **Keyframes** allow you to define multiple points for properties like `x` and `scale`.
-   **Repeat animation** allows you to repeat the animation indefinitely or a specific number of times.
-   **Repeat Types**:
    -   **`reverse`**: Animations reverse after each repeat.
    -   **`mirror`**: The animation mirrors itself after each repeat.
    -   **`loop`**: The animation loops continuously.
-   **`repeat` is part of the transition settings** and controls how the animation repeats.

This allows you to create dynamic and smooth animations that repeat with various effects.


---

Here’s a table summarizing the **Framer Motion** properties you can use, along with their possible values and explanations:

| **Property**              | **Value**                                                            | **Description**                                                                                                       |
| ------------------------- | -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **initial**               | Object (e.g., `{ opacity: 0, x: -100 }`)                             | Defines the starting position or state of the element.                                                                |
| **animate**               | Object (e.g., `{ opacity: 1, x: 0 }`)                                | Specifies the final position or state of the element.                                                                 |
| **exit**                  | Object (e.g., `{ opacity: 0, x: 200 }`)                              | Defines the animation for an element when it exits or is removed from the DOM.                                        |
| **transition**            | Object (e.g., `{ duration: 2, delay: 1, type: "spring" }`)           | Defines the duration, delay, type, and other transition properties such as `mass`, `stiffness`, and `damping`.        |
| **whileHover**            | Object (e.g., `{ scale: 1.2 }`)                                      | Specifies the animation to trigger when the element is hovered.                                                       |
| **whileTap**              | Object (e.g., `{ scale: 0.8 }`)                                      | Specifies the animation to trigger when the element is clicked or tapped.                                             |
| **whileFocus**            | Object (e.g., `{ borderColor: 'blue' }`)                             | Specifies the animation when an input field gains focus.                                                              |
| **whileDrag**             | Object (e.g., `{ scale: 1.2 }`)                                      | Specifies the animation when the element is being dragged.                                                            |
| **drag**                  | "x", "y", or "both"                                                  | Enables dragging along the x-axis, y-axis, or both axes.                                                              |
| **dragConstraints**       | Object (e.g., `{ left: 0, right: 100 }`)                             | Defines the boundaries within which the element can be dragged.                                                       |
| **whileInView**           | Object (e.g., `{ opacity: 1 }`)                                      | Specifies the animation when the element enters the view (e.g., when the user scrolls to it).                         |
| **variants**              | Object (e.g., `{ hidden: { opacity: 0 }, visible: { opacity: 1 } }`) | Defines multiple states (e.g., hidden, visible) for the element to animate between.                                   |
| **initial (in variants)** | String (e.g., "hidden")                                              | Specifies which variant state to start with (e.g., "hidden", "visible").                                              |
| **animate (in variants)** | String (e.g., "visible")                                             | Specifies which variant state to animate to (e.g., "visible", "hidden").                                              |
| **beforeChildren**        | Boolean (e.g., `true`)                                               | Ensures the parent animation completes before the children start.                                                     |
| **afterChildren**         | Boolean (e.g., `true`)                                               | Ensures the parent animation starts after the children finish.                                                        |
| **delayChildren**         | Number (e.g., `0.5`)                                                 | Adds a delay before starting the children's animations.                                                               |
| **staggerChildren**       | Number (e.g., `0.5`)                                                 | Adds a stagger (delay) between each child animation.                                                                  |
| **repeat**                | "Infinity" or Number (e.g., `3`)                                     | Defines how many times the animation repeats, or if it repeats infinitely.                                            |
| **repeatType**            | "reverse", "mirror", or "loop"                                       | Specifies how the animation repeats: `reverse` (back and forth), `mirror` (mirrors itself), `loop` (continuous loop). |
| **x**                     | Number or Array (e.g., `100`, `[0, 100, 0]`)                         | Defines the horizontal movement (can also use `y` for vertical movement).                                             |
| **scale**                 | Number or Array (e.g., `1`, `[1, 2, 1]`)                             | Defines the scaling of the element.                                                                                   |
| **opacity**               | Number (e.g., `0`, `1`)                                              | Defines the opacity of the element (from fully transparent to fully opaque).                                          |
| **rotate**                | Number (e.g., `90`)                                                  | Defines the rotation of the element in degrees.                                                                       |
| **delay**                 | Number (e.g., `2`)                                                   | Sets the delay before the animation starts (in seconds).                                                              |
| **duration**              | Number (e.g., `2`)                                                   | Defines how long the animation takes to complete (in seconds).                                                        |
| **type**                  | String (e.g., `"spring"`, `"tween"`)                                 | Defines the type of animation: `"spring"` for bouncy animations, `"tween"` for smooth, linear transitions.            |
| **mass**                  | Number (e.g., `1`, `2`)                                              | Defines the "weight" of the spring. A higher value makes the spring move slower.                                      |
| **damping**               | Number (e.g., `20`)                                                  | Controls how quickly the spring slows down. A higher value results in a quicker stop.                                 |
| **stiffness**             | Number (e.g., `100`)                                                 | Defines the stiffness of the spring. A higher value makes the animation quicker and tighter.                          |

This table covers many of the key properties used in **Framer Motion** for animations.

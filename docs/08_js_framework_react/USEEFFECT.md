# Understanding `useEffect` in React

`useEffect` is one of the most important hooks in React. It allows you to perform **side effects** in function components, such as:

- Fetching data from APIs
- Starting timers or intervals
- Subscribing to external events
- Manually updating the DOM (rare in React)

---

## 1️⃣ Basic Idea

- `useEffect` runs **after the render** is committed to the screen.
- It can optionally return a **cleanup function** that runs:
  - Before the next effect runs (when dependencies change)
  - Or when the component unmounts

```js
useEffect(() => {
  // Effect body
  return () => {
    // Cleanup body
  };
}, [dependencies]);
```

---

## 2️⃣ Rules of Thumb

1. **Effects synchronize with external systems**

   - Only update internal state if it’s the result of that synchronization.
   - Example: fetching data or starting a timer.

2. **Do not use effects for things that can be computed during render**

   - Derived state from props? Compute directly.
   - User interactions? Handle in event handlers.
   - Initialization? Use the state initializer.

3. **Dependencies array matters**
   - Include everything the effect reads from outside the effect body.
   - **State setters (`setState`) do NOT need to be dependencies.**
   - If a value is read in the effect and changes, add it as a dependency.

---

## 3️⃣ Capturing Values in a Constant – “Snapshot” Pattern

React’s effects can be confusing because of **closures**.  
If you access a prop or state directly in the effect or cleanup, it may **change by the time cleanup runs**.

**Solution:** capture the value at the moment of this effect:

```js
useEffect(() => {
  const completedValue = wish.completed; // snapshot

  // effect body
  if (!completedValue) {
    // start interval, fetch, etc.
  }

  return () => {
    // cleanup body
    // completedValue remains the same as when this effect started
  };
}, [wish.completed]);
```

**Why this is important:**

- Without capturing, the cleanup may see **the latest prop/state**, not the one that was active when the effect started.
- Capturing ensures predictable behavior.
- Helps avoid bugs with intervals, timers, or async actions.

---

## 4️⃣ Example: Age Counter for a Wish

```js
useEffect(() => {
  const completedValue = wish.completed;
  let ageInterval;

  if (!completedValue) {
    ageInterval = setInterval(() => {
      setAge((currentAge) => currentAge + 1);
    }, 1000);
  }

  return () => {
    if (!completedValue) {
      clearInterval(ageInterval);
      setAge(0); // reset age when we stop counting
    }
  };
}, [wish.completed]);
```

**Explanation:**

- **Effect runs after render**, capturing `wish.completed` in `completedValue`.
- **Interval starts only if wish is not completed.**
- **Cleanup stops the interval and resets age** only if we were counting.
- Using a **functional state update** (`setAge(c => c + 1)`) avoids stale state issues and warnings from the linter.

---

## 5️⃣ When to use `useEffect`

✅ Fetching or syncing external data  
✅ Subscribing to events outside React  
✅ Timers, intervals, animations  
✅ Cleanup on unmount or dependency change

❌ Computing derived values from props/state  
❌ Updating state purely from other state (use render, reducers, or state initializers)  
❌ React events handled inside the DOM directly (`addEventListener`)

---

## 6️⃣ Mental Model

> **“Effects react to things outside React. State setters inside effects are the result of reacting, not the goal.”**

- `useEffect` runs **after render**
- Cleanup runs **before next effect or unmount**
- **Capture values** for predictable closure behavior
- **Use functional updates** when updating state depending on previous state

---

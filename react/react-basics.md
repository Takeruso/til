# React Core Concepts (v2 – Deep Dive, Interview-Ready)

## 1. JSX is Data, not DOM
- **Concept:**
  JSX is compiled to `React.createElement()` → a plain JavaScript object.
- **Why it matters:**
  React treats UI as **data**, not DOM nodes. This lets React:
  - Diff objects instead of touching the DOM.
  - Recreate UI descriptions cheaply.
  - Re-render components while delaying actual DOM changes.
  *DOM operations are expensive. Object creation is cheap.*
  **This is the core of React’s rendering model.**

## 2. Declarative = UI = f(state)
- **Concept:**
  The UI is a pure function of state.
- **Why it matters:**
  React doesn’t let you manipulate the DOM directly because imperative DOM logic causes:
  - Inconsistent UI
  - Hidden side effects
  - Complex cleanup
  - Race conditions
  
  By treating UI as the result of `f(state)`, React can:
  - Re-run the function.
  - Compute the diff.
  - Apply minimal DOM updates.
  **Declarative = React owns the DOM, you own the state.**

## 3. One Root Fiber
- **Concept:**
  Each component must return **exactly one root element**.
- **Why it matters:**
  React builds a **Fiber tree**, where each component produces one Fiber node which may have children.
  
  Multiple roots = multiple Fiber nodes with no parent = **no valid tree**.
  React needs:
  - One entry point.
  - One return path.
  - One reconciler per subtree.
  *Fragment (`<>`) only exists to satisfy this structural constraint.*

## 4. Virtual DOM = Diffing Layer, not a performance hack
- **Concept:**
  A lightweight, in-memory representation of the UI.
- **Why it matters:**
  The Virtual DOM is not “faster than DOM.” Its real purpose is to:
  - Provide a pure, deterministic structure for diffing.
  - Enable **interruptible rendering (Fiber)**.
  - Batch DOM writes into the Commit phase.
  - Avoid inconsistent intermediate UI states.
  **Virtual DOM is the “calculation layer”. DOM is the “effect layer.”**

## 5. Composition > Inheritance
- **Concept:**
  Components are functions. UI is built by **function composition**.
- **Why it matters:**
  React avoids inheritance because:
  - Inheritance couples behavior.
  - Composition isolates concerns.
  - Functions compose naturally (props → output).
  
  This matches React’s core model:
  **“UI = functions + state transitions”**
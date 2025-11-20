# React Rendering Model: Fiber, Reconciliation & Concurrent

**Deep dive into how React actually works under the hood.**
(Understanding React 18, Fiber Architecture, and the Render Phases)

## 1. DOM (Document Object Model)
- **Concept:** The DOM is an object model representing HTML as a tree structure inside the browser.
- **Key Point:** JavaScript interacts with the DOM tree, not HTML strings. React uses the **Virtual DOM** to perform minimal updates because touching the real DOM is slow.

## 2. React vs. ReactDOM
- **React:** Responsible for "UI Logic" (Components, State, Virtual DOM). It describes the *ideal* state of the UI.
- **ReactDOM:** The "Renderer". It calculates the difference (diff) and updates the actual DOM.
- **Summary:** React decides **"WHAT"** to render, ReactDOM handles **"HOW"** to render it.

## 3. Legacy vs. Concurrent Rendering (React 18)
- **React 17 (Legacy):** Blocking rendering. Once updates start, they cannot be interrupted. (Can cause UI freezing).
- **React 18 (Concurrent):** Introduced `createRoot()`. Rendering is **interruptible**.
    - High priority tasks (user input) can pause low priority tasks (heavy rendering).
    - Keeps the app responsive even during heavy updates.

## 4. Priority Lanes
React categorizes updates into priorities:
1.  **Immediate:** Key press, Click, Scroll (Must react instantly).
2.  **Normal:** `useState` updates, re-renders.
3.  **Low/Idle:** Background tasks, Suspense preparation.

The **Scheduler** decides what to process now and what to delay.

## 5. Reconciliation
The algorithm for diffing the "Old Virtual DOM" vs. the "New Virtual DOM".
- **Rule:** If a component type changes, destroy and rebuild the tree.
- **Rule:** List items are optimized using `keys`.

## 6. React Fiber
**Fiber is the core engine of React 18.**
- **Definition:** Fiber is a **"Unit of Work"**.
- **Why it changed:** The old engine updated the whole tree synchronously (slow). Fiber breaks work into small units that can be **paused, resumed, or prioritized**.
- **Structure:** A Linked List structure (Child -> Sibling -> Return).

## 7. The Two Phases: Render vs. Commit
React updates happen in two distinct phases:

1.  **Render Phase (Async / Interruptible):**
    - Constructs the new Fiber tree.
    - Calculates changes (diff).
    - *Can be paused or aborted.*
2.  **Commit Phase (Sync / Uninterruptible):**
    - Applies changes to the real DOM.
    - Runs layout effects.
    - *Cannot be stopped (to ensure UI consistency).*

## 8. Why does this matter? (Developer Perspective)
Understanding Fiber and Concurrency helps to:
- Understand how `useTransition` and `Suspense` actually work.
- Debug performance issues (why is my input lagging?).
- Explain **"Why React?"** in technical interviews (The ability to interrupt rendering for better UX).

---
### 🇯🇵 日本語メモ (Deep Dive)

**Fiber Tree とトラバースの仕組み**
Reactは以下の順序でFiberノード（作業単位）を処理する。
1.  **Start:** 親から開始
2.  **Child:** 最初の子へ (Deep dive)
3.  **Sibling:** 子が終わったら兄弟へ
4.  **Return:** 兄弟がいなければ親に戻る
*この過程のどこでも「中断・再開」が可能。*

**Concurrent Rendering の挙動例**
重い処理（C）を実行中に、ユーザーがキー入力（高優先度）を行った場合：
1.  `currentFiber = C` を保存して一時停止。
2.  キー入力処理（高優先度）を先に実行して画面に反映。
3.  終わったら `C` から作業を再開する。
→ これが「アプリが固まらない」理由。
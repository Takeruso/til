# React Basics & Fundamentals

Learned from : [Scrimba React Course](https://scrimba.com/learn-react-c0e)

## 1. Rendering Location

Basic structure where elements that created in React insert.
- **Concept:**
 All react elements are rendered inside the specific container in the HTML file.

  ### Virtual DOM vs Real DOM
  **Q. Do React elements go directly to the browser's DOM?**

    - **Answer:** No. They go to the **Virtual DOM** first.
    - **Process:**
        1. React creates a copy of the DOM in memory (Virtual DOM).
        2. It compares the new version with the old version (Diffing).
        3. It updates only the parts that changed in the actual Browser DOM.
    - **Why?:** Updating the real DOM is slow/expensive. This method makes React fast.

## 2. JSX acts as JavaScript Object

JSX looks like HTML. However, how are they treated in JavaScript?
 
- **Concept:**
 JSX is not a string or HTML. It compiles down to plain **JavaScript Object**
- **Memo:**
If I run `console.log(<h1>Hello</h1>)`, it returns a js object not a DOM element. Because JSX is treated as data (instructions for creating UI), it can be stored in variables or returned from functions.

## 3. One Parent Rule

An important regulation to return JSX.

- **Concept:**
 React components (or `root.render`) must return a **single parent element**.
- **Memo:**
 There is based on JS rule that `return` statement only can return one value(object). If I want to return several elements, I need to make one element to use `<div>` and `<>` (Fragment).

## 4. Declaretive vs Imperative (宣言的　vs　命令的)

The defining style feature of React.

- **Declarative (React):**
 Describing **"WHAT"** should happen. (Tell React what the UI should look like, and let it handle the DOM updates)
- **Imperative (jQuery/Vanilla JS):**
 Descriping **"HOW"** to do it. (Step-by-step instructions: create element -> add text -> append to body.)
- **Memo:**
 The difference is only to tell the destination to a taxi driver (Delarative) and to tell all the process how to go to the destination. React is former.

## 5. Composability (構成可能性)
Modern UI development concept.

- **Concept:**
 Building complex application by assembling small, reuseable pieces called **Components**
- **Memo:**
 It does't create huge one file, it approaches to create small lego such as `Header`, `Footer` and `Button`.


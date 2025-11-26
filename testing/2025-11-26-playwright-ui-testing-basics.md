# TIL: Playwright – Key Practical Learnings

## 1. What Playwright Actually Tests
Playwright verifies **UI behavior through real browser interactions**, not internal logic.
It checks whether the *final visible state* of the UI behaves correctly when a user clicks, types, navigates, etc.

Trying to use Playwright to validate internal logic or function-level behavior is a misuse of the tool.

---

## 2. E2E Performance Reality
End-to-end tests are inherently slow because they involve:

- Browser startup
- Page rendering
- DOM updates
- Network requests
- Simulated human interactions

This makes E2E **structurally heavy**, so the strategy must be:
**Quality > Quantity.**

A few essential flows are far more valuable than many brittle tests.

---

## 3. Why Playwright Tests Break Easily
UI changes directly affect E2E tests:

- Text changes
- DOM structure changes
- Selector updates
- Component nesting differences

Because E2E relies on the rendered UI, these changes frequently break tests.

**Conclusion:**  
Only write E2E tests for areas of the UI that are already stable.

---

## 4. Browser API Limitations
Some browser-dependent APIs have restricted automation due to security constraints:

- Permission dialogs
- Screen/media capture
- Camera/microphone access
- OS-level interactions

These are **browser limitations, not Playwright limitations**.  
No E2E framework can bypass browser security policies.

---

## 5. Clear Separation of Responsibilities
Unit tests and E2E tests serve different purposes:

| Type of Test | Purpose |
|--------------|---------|
| **Unit Tests** | Validate internal logic, branching, and data handling |
| **Playwright E2E Tests** | Validate full UI flows and final visible behavior |

Mixing both in E2E results in brittle, slow, and unmaintainable test suites.

---

## Summary
- Playwright is for UI flow validation, not logic validation.  
- E2E is inherently slow → keep it minimal and strategic.  
- UI changes easily break E2E tests → only test stable flows.  
- Some browser features cannot be fully automated by design.  
- Unit tests and E2E tests must remain separate and complementary.


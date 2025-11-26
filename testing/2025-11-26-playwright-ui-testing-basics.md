# Understanding Playwright: Key Learnings

Playwright is a tool to verify the final state of UI through **user interactions × real browsers**
→ It's not for testing internal logic.

## Performance Implications

E2E testing with real browsers is structurally "heavy" due to browser startup
→ **Quality over quantity matters more than the number of tests.**

## Fragility Concerns

UI changes (text, structure, selectors) make tests break easily
→ **Start writing tests on stable parts of the UI.**

## Browser Limitations

Browser-dependent APIs (permissions, capture features, etc.) have limited automation capabilities
→ This is a **browser security specification issue**, not a tool limitation.

## Clear Separation of Concerns

Unit tests and E2E tests should have completely separate roles:
- **Unit Tests**: Verify the correctness of internal logic
- **Playwright E2E Tests**: Ensure the overall UI flow doesn't break

---

## Summary

| Aspect | Purpose |
|--------|---------|
| Unit Tests | Internal logic validation |
| Playwright E2E | UI integrity and user flow verification |

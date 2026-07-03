---
name: code-simplification
description: Simplifies code for clarity. Use when refactoring code for clarity without changing behavior. Use when code works but is harder to read, maintain, or extend than it should be. Use when reviewing code that has accumulated unnecessary complexity.
---

## Analysis Strategy
1. **Locate Code Smells:** Spot nested conditional branches, large switch statements, repetitive functions, and dead code variables.
2. **Apply DRY Principle:** Find lines matching syntax signatures across separate layouts. Extract into functions or reusable structures.
3. **Complexity Reduction:** Replace manual collections logic with streamlined arrays functions (`map`, `filter`, `reduce`).
4. **Semantic refactoring:** Replace long if-else layouts with ternary operations, early guards, or map lookups.

## Code Standards
- **Guard Clauses:** Prefer returning error matches early.
  ```typescript
  // Bad
  if (user) { if (user.isActive) { return process(user); } }
  
  // Good
  if (!user || !user.isActive) return;
  return process(user);
  ```
- **Lookup Maps:** Avoid long else-if blocks.
  ```typescript
  const STYLING_MAP = { active: 'bg-green', idle: 'bg-gray' };
  const getStyle = (state) => STYLING_MAP[state] || STYLING_MAP.idle;
  ```

## Rules
- Verify tests still pass after refactoring.
- Do not modify architectural API structures or data formats.
- Refactor progressively — one module block per session.

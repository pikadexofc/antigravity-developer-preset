---
name: browser-testing-with-devtools
description: Tests in real browsers via Chrome DevTools MCP. Use when building or debugging anything that runs in a browser. Use when you need to inspect the DOM, capture console errors, analyze network requests, profile performance, or verify visual output with real runtime data. Requires the chrome-devtools MCP server to be configured.
---

## Tools
- `new_page` → start session | `close_page` → end session | `list_pages` → check active pages
- `navigate_page` → load url | `select_page` → focus context
- `evaluate_script` → DOM queries/window variables
- `click` / `type_text` / `fill` / `fill_form` / `press_key` / `hover` / `drag` → interactions
- `take_screenshot` / `take_snapshot` → visual verification
- `list_console_messages` / `get_console_message` → errors & output
- `list_network_requests` / `get_network_request` → API inspections
- `resize_page` / `emulate` → layout & device testing

## Workflow
1. **Init:** `new_page` or `list_pages` → find viewport targets.
2. **Load & Test:** `navigate_page` to localhost/Vercel -> wait for selectors using browser-testing.
3. **Verify:** Check for errors with `list_console_messages` (warnings/failures).
4. **Assert DOM:** Run `evaluate_script` to check document structures:
   ```js
   document.querySelector('.target').textContent
   ```
5. **Interactive Flow:** Use `click`, `type_text`, and `fill_form` to test interactive loops.
6. **Capture:** `take_screenshot` (saved under absolute local paths) to verify visual design.
7. **Cleanup:** Explicitly `close_page` when done.

## Rules
- Always check console logs before declaring success.
- Use explicit viewport sizes with `resize_page` to test mobile breakpoints.
- Do not let pages remain open post-session.

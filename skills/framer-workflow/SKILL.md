---
name: framer-workflow
description: Framer + Unframer workflow skill. Use when working with Framer projects, CMS collections, React component export, code overrides, or publishing. Covers MCP tool usage, component patterns, and CMS integration patterns.
---

## MCP Tools
- `getProjectXml` — project tree | `getNodeXml` — single node | `getSelectedNodesXml` — selection
- `updateXmlForNode` — mutate node | `zoomIntoView` — verify visually
- `readCodeFile` / `createCodeFile` / `updateCodeFile` — overrides
- `getCMSCollections` / `getCMSItems` / `upsertCMSItem` — CMS CRUD
- `exportReactComponents` | `getProjectWebsiteUrl` | `getComponentInsertUrlAndTypes`
- `manageColorStyle` / `manageTextStyle` — tokens | `createPage` / `duplicateNode` / `deleteNode`

## Workflow
1. **Orient:** `getProjectXml` → `getSelectedNodesXml`
2. **Inspect before mutate:** `getNodeXml` on target → then `updateXmlForNode`. Never mutate blind.
3. **Overrides:** In `.framer/`. Read with `readCodeFile` before creating. Keep stateless; use `addPropertyControls` for config.
4. **CMS:** `getCMSCollections` → get ID+schema → `getCMSItems` → `upsertCMSItem` (all required fields).
5. **Publish:** `getProjectWebsiteUrl` → verify live render with Chrome DevTools MCP.

## Rules
- Never delete without `getNodeXml` first. Always `zoomIntoView` after mutating.
- Prefer updating existing components over creating new. Match tokens via `manageColorStyle` before adding new ones.

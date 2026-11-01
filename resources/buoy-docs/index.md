---
title: "Login items"
summary: "Inspect and explicitly manage the containing macOS app login service."
category: "Overview"
order: 0
keywords: ["loginitems", "login", "items"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Login items

MainAppLoginItem uses SMAppService.mainAppService for the containing application. Creating it and asking for status never enable login. It supports the main application only, not privileged helpers, launch daemons, or arbitrary executables.

## Platform support

Runtime support requires macOS 13 or newer. Registration additionally requires a correctly signed containing .app. A console process reports NotFound and refuses mutation. Other targets and older systems report Unsupported.

## Start reading

- [Getting started](getting-started.md) walks through installation and a complete example.
- [API reference](api.md) describes public symbols, state, errors, and ownership.

## Scope

Read Status to display current state. Call Register or Unregister only from a deliberate user preference action on the main thread. RequiresApproval must remain visible in the UI; it does not mean enabled. OpenLoginItemSettings opens the system pane without changing registration.

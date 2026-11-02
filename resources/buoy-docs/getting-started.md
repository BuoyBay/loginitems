---
title: "Login items getting started"
summary: "Install loginitems and use its core API with explicit application ownership."
category: "Guides"
order: 10
keywords: ["loginitems", "login", "items", "installation", "example"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Login items getting started

## Install and import

Copy the sealed `loginitems-0.1.0.buipkg` archive into your project `packages/` directory, or install a source/registry dependency named `loginitems` using BPM and sync it. Then use `Import loginitems`. The archive includes this documentation as package resources.

Use a consuming source filename such as `main.bui`; a local module named exactly like the package shadows its import.

## Complete usage example

The example is compiler-checked as a complete Buoy module. Functions and Subs are intended to be called from the consuming app at the appropriate user action or lifecycle event.

```basic
Import loginitems

Sub Main()
    Dim item As New MainAppLoginItem()
    Dim state As LoginItemState = item.Status()
    Print CType(state, Integer)
End Sub
```

## Integrate with the application

Read Status to display current state. Call Register or Unregister only from a deliberate user preference action on the main thread. RequiresApproval must remain visible in the UI; it does not mean enabled. OpenLoginItemSettings opens the system pane without changing registration.

## Handle failures and unsupported targets

Registration failures throw LoginItemException with NativeCode and the localized OS error description. Register returns RequiresApproval if macOS reports pending approval even when registration also returns an error. Availability does not prove signing, location, eligibility, or approval.

Runtime support requires macOS 13 or newer. Registration additionally requires a correctly signed containing .app. A console process reports NotFound and refuses mutation. Other targets and older systems report Unsupported.

Return to the [overview](index.md) or consult the [API reference](api.md).

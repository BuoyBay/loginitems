---
title: "Login items API"
summary: "Inspect and explicitly manage the containing macOS app login service."
category: "Reference"
order: 20
keywords: ["loginitems", "login", "items", "API", "lifecycle"]
symbols: ["LoginItemsSupported", "LoginItemState", "MainAppLoginItem", "MainAppLoginItem.Status", "MainAppLoginItem.Register", "MainAppLoginItem.Unregister", "OpenLoginItemSettings", "LoginItemException.NativeCode"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# Login items API

Import the `loginitems` package. Constructors below use the class name; invoke them with `New`. Listed members are public client APIs; native declarations and trampoline helpers are implementation details.

## Public surface

| Symbol | Contract |
| --- | --- |
| `LoginItemsSupported() As Boolean` | Checks runtime SMAppService availability without registering. |
| `LoginItemState` | Integer enum: Unsupported=-1, NotRegistered=0, Enabled=1, RequiresApproval=2, NotFound=3. |
| `MainAppLoginItem` | Inert wrapper for the containing main-app login service. |
| `MainAppLoginItem.Status() As LoginItemState` | Read-only query; unsupported or console contexts have explicit states. |
| `MainAppLoginItem.Register() As LoginItemState` | Explicit registration request; returns the subsequent state. |
| `MainAppLoginItem.Unregister() As LoginItemState` | Explicit removal request; returns the subsequent state. |
| `OpenLoginItemSettings()` | Opens the native Login Items settings pane without registering. |
| `LoginItemException.NativeCode As Integer` | Native error code attached to a registration exception. |

## Ownership and timing

Read Status to display current state. Call Register or Unregister only from a deliberate user preference action on the main thread. RequiresApproval must remain visible in the UI; it does not mean enabled. OpenLoginItemSettings opens the system pane without changing registration.

## Errors and result interpretation

`Register()` and `Unregister()` throw `LoginItemException` on failure. Unsupported runtime APIs, a missing containing `.app`, or a missing main-app service produce `NativeCode = -1` with a package-generated message. Native failures preserve the OS error code and localized description when an error object is available; otherwise the code is `-1` with a generic message. `OpenLoginItemSettings()` instead throws `UnsupportedOperationException` when the runtime API is unavailable. Catching only `LoginItemException` does not handle that settings failure. Register returns RequiresApproval if macOS reports pending approval even when registration also returns an error. Availability does not prove signing, location, eligibility, or approval.

## Platform behavior

Runtime support requires macOS 13 or newer. Registration additionally requires a correctly signed containing .app. A console process reports NotFound and refuses mutation. Other targets and older systems report Unsupported.

See the [complete usage example](getting-started.md) and the [package overview](index.md).

[Full typed API: properties, parameters, defaults, and returns](typed-api.md)

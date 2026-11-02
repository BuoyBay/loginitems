# LoginItems · 0.1.0

`Import loginitems` provides modern main-application login support using
`SMAppService.mainAppService` (macOS 13+). The ServiceManagement framework is loaded
at runtime; older macOS versions and other platforms are explicitly unsupported.

- `LoginItemsSupported()` checks runtime API availability, without registering.
- `New MainAppLoginItem()` has no side effects.
- `Status()` returns `LoginItemState`: Unsupported (-1), NotRegistered (0),
  Enabled (1), RequiresApproval (2), or NotFound (3).
- `Register()` and `Unregister()` explicitly change registration and return the
  subsequent state. Failures throw `LoginItemException` with `NativeCode` and
  Apple's localized error description.

A containing, correctly code-signed `.app` bundle is required. Console consumers
report NotFound and refuse mutation. API availability alone does not prove a
particular app is eligible, installed in the right location, approved by the user,
or correctly signed. Registered does not necessarily mean enabled: expose
RequiresApproval in the app and let the user manage consent in System Settings.
Only the containing main app is supported, not privileged helpers or launch daemons.

Call registration only from a deliberate user preference action, on the main
thread. Importing, constructing and querying this package never enable login.
The loaded system framework remains loaded for process lifetime. No shell command,
LaunchAgent plist installation, permission bypass or automatic fallback is used.

[Apple's registration API](https://developer.apple.com/documentation/servicemanagement/smappservice/register())
describes user approval and the required code-signing/application context.

`Register()` returns `RequiresApproval` when macOS reports a pending approval even if registration also returns an error. `OpenLoginItemSettings()` explicitly opens the system settings pane without registering an item.

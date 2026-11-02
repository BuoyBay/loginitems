# Register macOS applications to launch at login

`Import loginitems` provides modern main-application login support using
`SMAppService.mainAppService` (macOS 13+). The ServiceManagement framework is loaded
at runtime; older macOS versions and other platforms are explicitly unsupported.

A containing, correctly code-signed `.app` bundle is required. Console consumers
report NotFound and refuse mutation. API availability alone does not prove a
particular app is eligible, installed in the right location, approved by the user,
or correctly signed. Registered does not necessarily mean enabled: expose
RequiresApproval in the app and let the user manage consent in System Settings.
Only the containing main app is supported, not privileged helpers or launch daemons.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add loginitems --git https://github.com/BuoyBay/loginitems.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
Import loginitems

Sub Main()
    Dim item As New MainAppLoginItem()
    Dim state As LoginItemState = item.Status()
    Print CType(state, Integer)
End Sub
```

## Platform and scope

Registration uses macOS main-application login APIs. User approval and registration state remain explicit.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer loginitems
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```


## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)

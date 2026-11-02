---
title: "loginitems typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["LoginItemException", "LoginItemState", "MainAppLoginItem"]
dependencies: []
symbols: ["LoginItemException", "LoginItemState", "MainAppLoginItem"]
related: ["api.md", "getting-started.md", "index.md"]
---

# loginitems typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## LoginItemState

`Public Enum LoginItemState As Integer`

### Values

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Unsupported` | `LoginItemState` | `-1` | — |
| `NotRegistered` | `LoginItemState` | `0` | — |
| `Enabled` | `LoginItemState` | `1` | — |
| `RequiresApproval` | `LoginItemState` | `2` | — |
| `NotFound` | `LoginItemState` | `3` | — |

## LoginItemException

`Public Class LoginItemException Inherits Exception`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `NativeCode` | `Integer` | No | No | — | — |

### Constructor

`Public Sub Constructor(message As String, code As Integer)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `message` | `String` | `ByVal` | Required |
| `code` | `Integer` | `ByVal` | Required |

Returns: no value.

### LoginItemsSupported

`Public Function LoginItemsSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### OpenLoginItemSettings

`Public Sub OpenLoginItemSettings()`

Explicitly opens the system Login Items settings; does not register anything.

No parameters.

Returns: no value.

## MainAppLoginItem

`Public Class MainAppLoginItem`

Controls the containing app's main login service (macOS 13+). No mutations occur on construction.

### Status

`Public Function Status() As LoginItemState`

No parameters.

#### Returns

| Type |
| --- |
| `LoginItemState` |

### Register

`Public Function Register() As LoginItemState`

No parameters.

#### Returns

| Type |
| --- |
| `LoginItemState` |

### Unregister

`Public Function Unregister() As LoginItemState`

No parameters.

#### Returns

| Type |
| --- |
| `LoginItemState` |

# ubx-sdk-azure

Typed bindings for the `hashicorp/azurerm` Terraform provider, generated
by [ubx](https://github.com/ubiquex/ubiquex) (`ubx sdk gen`), for all
three SDK languages in one combined repo:

- [`sdk/go/`](sdk/go/) — Go bindings, module `github.com/ubiquex/ubx-sdk-azure/sdk/go`
  (a subdirectory Go module, tagged `sdk/go/vX.Y.Z`)
- [`sdk/typescript/`](sdk/typescript/) — TypeScript bindings, published to JSR as
  [`@ubx/sdk-azure`](https://jsr.io/@ubx/sdk-azure)
- [`sdk/python/`](sdk/python/) — Python bindings, published to PyPI as
  [`ubx-sdk-azure`](https://pypi.org/project/ubx-sdk-azure/) (imported as
  `ubx.azurerm.*`, a real PEP 420 namespace package)

One package per Azure resource-provider boundary (`compute/`, `storage/`,
...), one file per resource type, in every language.

**Naming note**: the repo/package name is `azure` (this project's own
real convention — matches the provider's short, common name), but the
provider source itself is `hashicorp/azurerm`, and every generated
directory/import path underneath (`azurerm/compute/...`,
`ubx.azurerm.compute`) reflects that real source name mechanically.
This is a deliberate, known divergence — not a typo in either
direction.

This repo-shaped-per-provider layout (UBI-138) supersedes the earlier
one-repo-per-(provider,language) convention (UBI-98/UBI-103) — matches
the real Pulumi precedent this project cites (`pulumi/pulumi-azure`'s
own `sdk/go/`, `sdk/python/`, `sdk/nodejs/` structure). Package names on
every registry are unchanged from the earlier per-language repos; only
Go's module path changed, because a subdirectory Go module requires it.

The version this repo was last generated from is tracked in `VERSION`.
Every file except each language's own `doc.{go,ts}` / `__init__.py` is
generated — do not hand-edit; re-run `ubx sdk gen` after a provider
version bump.

Depends on the shared runtime: [ubx-sdk-go](https://github.com/ubiquex/ubx-sdk-go) (Go),
[`jsr:@ubx/sdk`](https://jsr.io/@ubx/sdk) (TypeScript),
[`ubx-sdk`](https://pypi.org/project/ubx-sdk/) (Python, imported as `ubx_sdk`).

# artifacts/azure

UBI-240 slice 6: the canonical home for this provider's own docs/codegen
artifacts, moved here from `ubiquex-docs`. See `ubx-sdk-kubernetes`'s
own `artifacts/kubernetes/README.md` for the full account of why this
moved (UBI-102's own comment thread) and how the four files divide.

- **`descriptions.json`** / **`intros.json`** / **`categories.json`** /
  **`exclusions.json`** — real source of truth, read by
  `ubx-docs-providers` at build time. `descriptions.json` is keyed
  against the raw (doubled) wire, same as always —
  `export_raw_descriptions.py` applies `azure_corrected_wire` at export
  time, not something to redo by hand.
- **`azure.json`** — codegen-ready export (`{resource: {relPath:
  text}}`, already `azure_corrected_wire`-keyed). What `ubx sdk gen
  --descriptions-dir artifacts/azure` actually reads. Never edited
  directly.

To update: edit `descriptions.json` here, then regenerate `azure.json`
from a sibling `ubiquex-docs` checkout:

```bash
ubx sdk gen --only azure --dump-ir /tmp/dump --out /tmp/unused
cd ~/Ubiquex/ubiquex-docs/scripts/resource-reference-gen
python3 export_raw_descriptions.py azure "Microsoft Azure" \
    --dump-root /tmp/dump/azure \
    --descriptions-path ~/Ubiquex/ubx-sdk-azure/artifacts/azure/descriptions.json \
    --nested-out ~/Ubiquex/ubx-sdk-azure/artifacts/azure/azure.json
```

Commit both files together.

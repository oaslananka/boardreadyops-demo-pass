# BoardReadyOps demo — a board that gets fixed

A two-file KiCad project that starts out unfabricable, and one pull request that repairs it.

`main` carries the broken board. [Pull request #1](../../pull/1) repairs it, and the
**Fabrication readiness** check on that pull request goes green.

Read the check's comment on the pull request — that is the whole product in one screen:
every finding, where it is on the board, and what to do about it.

## What is wrong on `main`

| Rule | What it caught |
| --- | --- |
| `design.board-outline` | No closed outline on Edge.Cuts, so the fabricator has no board shape. |
| `design.unique-references` | Two components share a reference designator. |
| `bom.missing-mpn` | A BOM line has no manufacturer part number, so it cannot be sourced. |
| `bom.compliance` | A part carries no RoHS/REACH status. |
| `bom.risk-score` | Single-source parts push the assembly's supply risk over the threshold. |

## Running it yourself

```bash
npx @boardreadyops/cli run .
```

No KiCad installation required: `boardreadyops.yml` disables the DRC and ERC rules that
shell out to `kicad-cli`, so the checks above run on the files alone.

The companion repository [boardreadyops-demo-fail](https://github.com/oaslananka/boardreadyops-demo-fail)
runs the same corpus the other way round — a clean board, and a pull request that breaks it.

Licensed MIT, like BoardReadyOps itself. Copy the board, the config, or the workflow into your own repository.

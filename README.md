# rotation-size-planner

Estimate storage consumed by rotated logs and an active file.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "active_mib": 100,
  "rotations": 7,
  "compression_ratio": 0.2,
  "budget_mib": 300
}
```

Result:

```json
{
  "estimated_mib": 240.0,
  "within_budget": true
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Assumes equally sized rotations; compression ratios and log growth vary. No files are rotated or removed.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [systemd-unit-linter](https://github.com/sal-s-root/systemd-unit-linter), [maintenance-window-planner](https://github.com/sal-s-root/maintenance-window-planner).

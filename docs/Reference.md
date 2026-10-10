# Sampler and contributor reference

The [README](../README.md) covers installation, controls, hardware support, and updates.
This page describes the sampler output and developer checks.

## Plugin entry point

The plugin id is `im0001gt.hw-tooltip`. Its bar entry is `HardwareTooltip.qml`.
The reviewed manifest version is `1.7.0`. See [manifest.json](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/manifest.json#L1-L23).

## Sampler output

`scripts/system-usage` emits text records, one per line. Labels that contain spaces occupy the rest of their line.

| Prefix | Fields |
| --- | --- |
| `cpu` | Overall load percentage |
| `core` | Logical core index and load percentage |
| `cpu_name` | CPU name |
| `ram` | Used GiB, total GiB, and percentage |
| `ram_info` | Memory type and speed |
| `gpu` | Percentage or `n/a` |
| `gpu_name` | GPU name |
| `gpu_kind` | `render` or `infer` |
| `gpu_hint` | Missing tool hint, such as `nvidia-utils` |
| `cpu_temp`, `gpu_temp`, `ram_temp` | Celsius or `n/a` |
| `disk_temp` | Mount and Celsius |
| `disk` | Mount, used GiB, total GiB, percentage, and optional model |

This contract is in [scripts/system-usage](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/scripts/system-usage#L1-L28).
The sampler measures CPU counters across a 0.2-second interval.
Memory usage derives from `MemTotal` and `MemAvailable`.
See [scripts/system-usage](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/scripts/system-usage#L39-L102).

## Missing readings

The sampler tries the Python sidecar before its final GPU fallback.
An absent GPU reading becomes `gpu n/a`. See [scripts/system-usage](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/scripts/system-usage#L130-L142).
The Python `tick` command can return status 1 while it still emits temperature records.
That status means it could not report GPU load. It does not discard other measurements.
See [scripts/hw_tooltip.py](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/scripts/hw_tooltip.py#L903-L918).
Missing kernel sensors do not prove a device has no load or heat.
For hardware-specific sources, use the [README requirements](../README.md#requirements).

## Developer checks

From a working checkout with Python 3 and Omarchy, run:

```sh
python3 -m unittest discover -s tests -v
omarchy plugin validate .
```

The first command selects the repository's unittest suite. See [tests/test_hw_tooltip.py](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/tests/test_hw_tooltip.py#L1-L24).
The second checks the root plugin manifest. See [README.md](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/README.md#L106-L119).
This source review did not execute these checks or test real GPU telemetry.

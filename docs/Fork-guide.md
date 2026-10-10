# Fork source guide

This repository is a fork of [the upstream project](https://github.com/IM0001GT/omarchy-hw-tooltip).
The source snapshot for this guide is `d6fd7e05589bacc40940a71b08eba97b976fcc89` in `wszaq/omarchy-hw-tooltip`.
The [GitHub repository](https://github.com/wszaq/omarchy-hw-tooltip) identifies the upstream relationship.

## Attribution and scope

The fork keeps the plugin id `im0001gt.hw-tooltip` and names IM0001GT as its author.
The original [README](../README.md#install) installs from the upstream URL.
That command follows upstream, rather than this fork's reviewed snapshot.
See [manifest.json](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/manifest.json#L1-L9) and [README.md](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/README.md#L51-L59).

## Install this fork

If you want this fork, replace the upstream URL in the existing installation command:

```sh
omarchy plugin add https://github.com/wszaq/omarchy-hw-tooltip --enable
```

This command follows the fork's current default branch. It does not pin the reviewed commit.
The command form comes from the [README installation section](https://github.com/wszaq/omarchy-hw-tooltip/blob/d6fd7e05589bacc40940a71b08eba97b976fcc89/README.md#L51-L59).
The fork uses the same plugin id as upstream. Do not treat them as two independent plugins.
This review did not execute installation. Read the existing trust and requirements notes before you install.

## Compare before you merge

This guide does not claim which files differ from upstream. The review inspected this fork's source snapshot only.
Before you merge an upstream update, compare the relevant commit and files.
Keep existing attribution and asset notices with their sources.

Read [Sampler reference](Reference.md) for the additional protocol and developer checks.

# AD5M Buildroot repository instructions

This repository maintains the Buildroot base used by the Flashforge AD5M
Klipper Mod project.

## Repository relationships

Writable repository:

- origin:
  git@github.com:iRomanyshyn/buildroot-flashforge-ad5m.git

Primary upstream:

- upstream:
  https://gitlab.com/buildroot.org/buildroot.git

Historical AD5M Buildroot reference:

- xblax:
  https://github.com/xblax/flashforge_adm5_buildroot_chroot.git

Sibling Klipper Mod repository:

- ../flashforge_ad5m_klipper_mod

Project coordination repository:

- ../ad5m-project

Before substantial project work, read:

- ../ad5m-project/PROJECT.md
- the active task under ../ad5m-project/tasks/, when one exists
- ../flashforge_ad5m_klipper_mod/AGENTS.md when the task affects integration

## Current base

The maintained branch is:

- ad5m-2025.02

It is based on the official Buildroot 2025.02 LTS series.

Do not develop AD5M changes on upstream/master.

## Repository role

This repository should contain changes that properly belong in the
Buildroot base itself, including:

- generic Buildroot package fixes
- missing package dependencies
- base userspace changes
- toolchain-related changes
- reusable Buildroot package definitions
- changes that are not inherently specific to the Klipper Mod integration

Printer-specific integration should normally remain in the sibling
flashforge_ad5m_klipper_mod repository, especially:

- printer configuration
- Klipper macros
- Moonraker configuration
- service integration specific to AD5M
- Klipper Mod installer/update logic
- variant configuration
- project-specific Buildroot external-tree packages where appropriate

Before adding something here, consider whether it belongs in the
Klipper Mod Buildroot external tree instead.

## Upstream policy

Prefer official Buildroot functionality and fixes.

When functionality is missing:

1. Check whether the official Buildroot 2025.02 LTS branch already contains
   an appropriate solution.
2. Check newer official Buildroot versions for an upstream fix that can be
   backported cleanly.
3. Only then consider carrying a project-specific patch.

The xblax repository is a historical/reference source. Do not merge its
master branch wholesale.

Inspect and port individual AD5M-relevant changes only after determining
that they are still necessary.

Do not treat third-party Buildroot forks as authoritative upstreams.

## Cross-repository changes

If a task requires changes to both this repository and
flashforge_ad5m_klipper_mod:

- inspect both repositories before modifying either
- keep generic Buildroot changes here
- keep AD5M integration changes in Klipper Mod
- document any required commit pairing in the task file

Do not solve a Buildroot problem by adding a workaround to Klipper Mod
without first determining where the underlying fix belongs.

## Safety and reliability

This project runs on a resource-constrained embedded device.

Avoid unnecessary:

- packages
- daemons
- memory use
- persistent writes
- background CPU load

Changes affecting boot, filesystem layout, updates, networking, or runtime
dependencies must be reviewed for failure and recovery behavior.

## Git rules

Before modifying files:

- inspect `git status`
- confirm the current branch
- inspect relevant history when changing inherited code

Do not:

- push to upstream
- push to xblax
- force-push
- rebase published branches
- commit
- push
- merge
- open pull requests

unless explicitly requested by the user.

Do not silently modify unrelated files.

## Verification

Never claim a successful build unless the build was actually run.

Never claim hardware verification unless the result was actually tested
on an AD5M or AD5M Pro.

At the end of a task report:

- files changed
- why the change belongs in this repository
- build/test commands actually run
- corresponding Klipper Mod changes required
- hardware testing still required
- unresolved risks or questions

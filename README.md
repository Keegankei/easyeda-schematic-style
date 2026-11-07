<h1 align="center">EasyEDA Schematic Style</h1>

<p align="center">
  <strong>Clear schematics, consistent style.</strong><br>
  An agent skill for EasyEDA Professional layout, annotations, and verification.
</p>

<p align="center">
  <strong>English</strong> · <a href="README.zh-CN.md">简体中文</a>
</p>

<p align="center">
  <a href="https://github.com/Keegankei/easyeda-schematic-style/releases/tag/v1.0.0"><img src="assets/badges/version.svg" alt="Version 1.0.0"></a>
  <a href="SKILL.md"><img src="assets/badges/format.svg" alt="Format: Codex skill"></a>
  <a href="LICENSE"><img src="assets/badges/license.svg" alt="License: MIT"></a>
</p>

**Version 1.0.0** · [Release notes](https://github.com/Keegankei/easyeda-schematic-style/releases/tag/v1.0.0) · [Download ZIP](https://github.com/Keegankei/easyeda-schematic-style/releases/download/v1.0.0/easyeda-schematic-style-v1.0.0.zip)

[Get started](#get-started) · [Features](#features) · [Examples](#examples) · [Verification](#verification) · [Guides](#guides) · [License](#license)

---

A reusable agent skill for drawing, organizing, and reviewing **EasyEDA Professional schematics**. Follow a reference sheet's visual style or use project defaults while preserving the electrical design and staying within the authorized editing scope.

> **A reference sheet is optional.** Start with an existing circuit and a sheet name; the included guide supplies layout and typography principles.

<a id="get-started"></a>

## Get started

### 1. Check the requirements

- An agent that supports `SKILL.md` skills or can read these instructions explicitly.
- Access to the relevant EasyEDA Professional project. Reference sheets are optional.
- For automated edits, a working official EasyEDA MCP, CLI, or extension API connection, plus documentation for the installed version.

This package contains instructions and reference guides, with no bundled MCP server, EasyEDA extension, or component library. Installing it does not configure an EasyEDA connection. The package itself requires no Python packages or bundled runtime.

### 2. Download and install

**[Download easyeda-schematic-style-v1.0.0.zip](https://github.com/Keegankei/easyeda-schematic-style/releases/download/v1.0.0/easyeda-schematic-style-v1.0.0.zip)**

Extract the ZIP and copy the **complete** `easyeda-schematic-style` folder to **one** location below. Choose a user-level location to reuse the skill across projects.

| Installation scope | Skill folder |
|---|---|
| Windows, current user | `%USERPROFILE%\.agents\skills\easyeda-schematic-style\` |
| macOS / Linux, current user | `~/.agents/skills/easyeda-schematic-style/` |
| Current project | `<project-root>/.agents/skills/easyeda-schematic-style/` |

These paths follow the [official Codex local-skills documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills). `%USERPROFILE%` and `~` mean your user home directory; `<project-root>` is the folder you open as your Codex project. With WSL or a remote environment, use the home directory of the environment where Codex runs.

On Windows, open `%USERPROFILE%` in File Explorer and create `.agents`, then `skills`, if they do not exist. Paste the skill folder inside `skills`. For project-only use, create `.agents/skills` inside your project instead.

The entry point should be `<skills-directory>/easyeda-schematic-style/SKILL.md`. For example, a Windows user-level installation puts it at `%USERPROFILE%\.agents\skills\easyeda-schematic-style\SKILL.md`. Keep `references/` beside `SKILL.md`; copying the entry point alone is insufficient. After extracting the ZIP, avoid an extra nested `easyeda-schematic-style` folder.

### 3. Run your first request

Codex normally detects skill changes automatically. If the skill does not appear, restart Codex. In Codex CLI or the IDE extension, use `/skills` or type `$` to find `easyeda-schematic-style`, then include `$easyeda-schematic-style` in your request. See the [official invocation instructions](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills).

For another compatible agent, use its skill directory and invocation method. You can also point it directly to [SKILL.md](SKILL.md) and identify the project and editable sheets. Automated EasyEDA editing still requires the connection listed above.

**No reference sheet?** Use the general style guide and project defaults. You do not need to choose fonts or sizes. The agent can group existing circuitry, clarify local wiring, and tidy labels while preserving the components, electrical connections, and ground topology.

Copy this request and replace `Controller` with your sheet name:

```text
Use $easyeda-schematic-style to organize the Controller sheet.
I have no reference sheet; use the general style guide and project defaults.
Improve functional grouping, local wiring presentation, and label readability.
Preserve current designators, values, footprints, assembly properties,
nets, and NC markers. Modify only this sheet.
Save, check connectivity, and report the changes and completed checks.
```

**Want to review first?** Ask for a review and proposed layout without edits.

**Starting with an empty sheet?** Supply the intended components and connections, or define a separate circuit-design task first. Missing visual references can be handled with defaults; missing circuit requirements should be identified rather than invented.

<a id="features"></a>

## Features

| Area | Guidance |
|---|---|
| **Layout** | Functional regions, readable signal flow, clear headings, and consistent spacing. |
| **Connections** | Compact local wiring for existing supporting circuits and cross-sheet summaries based on actual connectivity. |
| **Annotations** | Consistent reference designators, values, net labels, and interface destinations. |
| **Verification** | Netlist comparison, fresh visual checks, protection of read-only sheets, and API state checks for the installed version. |

<a id="examples"></a>

## More example requests

<details>
<summary><strong>Match an existing sheet</strong> — reuse a read-only style reference</summary>

```text
Use $easyeda-schematic-style to format the Controller sheet.
Use the Interface sheet as a read-only style reference.
Preserve all components, values, footprints, nets, and NC markers.
Do not modify any PCB or other board.
```

</details>

<details>
<summary><strong>Add an interface summary</strong> — describe current cross-sheet connections</summary>

```text
Add a non-electrical interface summary to the Power sheet.
Derive net names and destinations from the current project.
Keep the existing circuit and layout unchanged.
```

</details>

<details>
<summary><strong>Review without editing</strong> — collect layout findings</summary>

```text
Review the selected schematic sheets using $easyeda-schematic-style.
Report overlapping labels, unclear local connections, and inconsistent
formatting. Do not modify the project.
```

</details>

The sheet names in these examples are illustrative. Use your own project's names and editing scope.

<a id="verification"></a>

## Editing scope and verification

1. Identify authorized editable sheets, read-only references, and protected objects.
2. Capture the latest native data, rendered views, and electrical baseline.
3. Use a reference or the general guide to organize authorized content.
4. Save, read back, compare connectivity, and inspect fresh exports.
5. Report changes, completed checks, and unresolved findings.

Formatting-only work preserves current designators, component values, footprints, NC states, and assembly properties. Project-specific decisions about DNP parts, test points, ground topology, and numbering remain in place. Reference sheets and protected objects stay unchanged; the skill does not create review signatures or treat a successful API call as proof of a correct schematic.

The skill focuses on schematic presentation. PCB routing, component selection, and electrical redesign require their own explicit task scope.

<a id="guides"></a>

## Guides and package files

| File | Purpose |
|---|---|
| [SKILL.md](SKILL.md) | Agent entry point, scope, workflow, and verification |
| [Schematic style guide](references/schematic-style-guide.md) | Layout, wiring presentation, annotations, and interface summaries |
| [EasyEDA API notes](references/easyeda-api-notes.md) | Object identity, coordinates, state handling, and API verification |
| [Contributing](CONTRIBUTING.md) | Improvements and reproducible issue reports |
| [简体中文 README](README.zh-CN.md) | Simplified Chinese version of this guide |

The skill entry point, reference guides, and contribution guide are currently in English.

<details>
<summary><strong>View the complete folder structure</strong></summary>

```text
<skills-directory>/
└── easyeda-schematic-style/
    ├── SKILL.md
    ├── README.md
    ├── README.zh-CN.md
    ├── CONTRIBUTING.md
    ├── LICENSE
    ├── .gitignore
    ├── .gitattributes
    ├── assets/
    │   └── badges/
    │       ├── version.svg
    │       ├── format.svg
    │       └── license.svg
    └── references/
        ├── schematic-style-guide.md
        └── easyeda-api-notes.md
```

</details>

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Use synthetic examples and keep project files, credentials, personal paths, and private design information out of contributions.

---

<a id="license"></a>

## Author and license

Copyright © 2026 **KeeganKei**. This skill package is licensed under the [MIT License](LICENSE).

# EasyEDA Schematic Style

**English** | [简体中文](README.zh-CN.md)

A reusable agent skill for drawing and organizing **EasyEDA Professional schematics**. It helps an agent use a reference sheet's visual style or project defaults while preserving the electrical design and staying within the requested editing scope. A reference sheet is optional.

The package contains instructions and reference guides. It is not an MCP server, an EasyEDA extension, or a component library.

## What it covers

- Functional grouping and readable signal flow.
- Compact local wiring for existing supporting circuits.
- Consistent headings, reference designators, values, and net labels.
- Cross-sheet interface summaries based on actual connectivity.
- Netlist comparison, visual checks, and protection of read-only sheets.
- API state checks and version-aware editing practices.

It focuses on schematic presentation. PCB routing, component selection, and electrical redesign require their own explicit task scope.

## Requirements

- An agent that supports `SKILL.md` skills or can read these instructions explicitly.
- Access to the relevant EasyEDA Professional project. Reference sheets are optional.
- For automated edits, a working official EasyEDA MCP, CLI, or extension API connection, plus documentation for the installed version.

Installing the skill does not install or configure an EasyEDA connection. No Python packages or bundled runtime are required by this documentation-only package.

## Installation

### Codex: choose a location

Choose one scope and copy the **complete** `easyeda-schematic-style` folder to the corresponding location. The user-level option is convenient if you want to reuse it across projects. These paths follow the [official Codex local-skills documentation](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills).

| Scope | Skill folder |
|---|---|
| Windows, current user | `%USERPROFILE%\.agents\skills\easyeda-schematic-style\` |
| macOS / Linux, current user | `~/.agents/skills/easyeda-schematic-style/` |
| Current project | `<project-root>/.agents/skills/easyeda-schematic-style/` |

`%USERPROFILE%` and `~` mean your user home directory. `<project-root>` means the folder you open as your Codex project. These are generic locations, not a particular person's paths. With WSL or a remote environment, use the home directory of the environment where Codex runs.

On Windows, open `%USERPROFILE%` in File Explorer and create `.agents`, then `skills`, if they do not exist. Paste the skill folder inside `skills`. For project-only use, create `.agents/skills` inside your project instead.

### File placement example

After copying, the entry point should be `<skills-directory>/easyeda-schematic-style/SKILL.md`:

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
    └── references/
        ├── schematic-style-guide.md
        └── easyeda-api-notes.md
```

For example, Windows user-level installation puts the entry point at `%USERPROFILE%\.agents\skills\easyeda-schematic-style\SKILL.md`. Avoid an extra nested `easyeda-schematic-style` folder after extracting a ZIP. Keep `references/` beside `SKILL.md`; copying the entry point alone is insufficient.

### Check discovery and start

Codex normally detects skill changes automatically. If the skill does not appear, restart Codex. In Codex CLI or the IDE extension, use `/skills` or type `$` to find `easyeda-schematic-style`; then include `$easyeda-schematic-style` in your request. See the [official invocation instructions](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills).

For another compatible agent, use that agent's skill directory and invocation method. You can also point it directly to [SKILL.md](SKILL.md) and identify the project and editable sheets. Installing this package supplies drawing guidance; automated EasyEDA editing still needs the connection described under Requirements.

## Starting without a reference sheet

You do not need to prepare a reference page or choose fonts and sizes. Name the sheet the agent may edit and request the built-in general style guide with project defaults. It will:

- Group existing circuitry into functional regions with clear headings.
- Arrange signal flow and local wiring so connections are easy to follow.
- Use available fonts and consistent designators, values, and net labels.
- Preserve the existing electrical connections, components, and ground topology.

Copy this request and replace `Controller` with your sheet name:

```text
Use $easyeda-schematic-style to organize the Controller sheet.
I have no reference sheet; use the general style guide and project defaults.
Improve functional grouping, local wiring presentation, and label readability.
Preserve current designators, values, footprints, assembly properties,
nets, and NC markers. Modify only this sheet.
Save, check connectivity, and report the changes and completed checks.
```

If you prefer a first pass without edits, ask for a review and proposed layout only. If your sheet is empty, supply the intended components and connections, or define a separate circuit-design task first. Missing visual references can be handled with defaults; missing circuit requirements should be identified rather than invented.

## Example requests

### Match an existing sheet

```text
Use $easyeda-schematic-style to format the Controller sheet.
Use the Interface sheet as a read-only style reference.
Preserve all components, values, footprints, nets, and NC markers.
Do not modify any PCB or other board.
```

### Add an interface summary

```text
Add a non-electrical interface summary to the Power sheet.
Derive net names and destinations from the current project.
Keep the existing circuit and layout unchanged.
```

### Review without editing

```text
Review the selected schematic sheets using $easyeda-schematic-style.
Report overlapping labels, unclear local connections, and inconsistent
formatting. Do not modify the project.
```

These sheet names are illustrative. Use the names and scope of your own project.

## Working approach

1. Identify editable sheets, any read-only references, and protected objects.
2. Capture the latest native data, rendered views, and electrical baseline.
3. Extract a suitable visual hierarchy and organize authorized content.
4. Save, read back, compare connectivity, and inspect fresh exports.
5. Report changes, completed checks, and unresolved findings.

The skill preserves project-specific decisions such as DNP parts, test points, ground topology, and numbering. It does not create review signatures or treat a successful API call as proof of a correct schematic.

## Package structure

```text
easyeda-schematic-style/
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── CONTRIBUTING.md
├── LICENSE
├── .gitignore
├── .gitattributes
└── references/
    ├── schematic-style-guide.md
    └── easyeda-api-notes.md
```

| File | Purpose |
|---|---|
| [简体中文 README](README.zh-CN.md) | Simplified Chinese version of this guide |
| [SKILL.md](SKILL.md) | Agent entry point, scope, workflow, and verification |
| [Schematic style guide](references/schematic-style-guide.md) | Layout, wiring presentation, annotations, and interface summaries |
| [EasyEDA API notes](references/easyeda-api-notes.md) | Object identity, coordinates, state handling, and API verification |
| [Contributing](CONTRIBUTING.md) | Guidelines for improvements and reproducible reports |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Use synthetic examples and keep project files, credentials, personal paths, and private design information out of contributions.

## Author

KeeganKei

## License

This skill package is licensed under the [MIT License](LICENSE).

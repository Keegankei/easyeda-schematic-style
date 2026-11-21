---
name: easyeda-schematic-style
description: Draw and review EasyEDA Professional schematics, follow reference-sheet layout and wiring, and compare manual revisions for style, connectivity and assembly cleanup. Use for schematic work rather than PCB routing or standalone component selection.
metadata:
  version: "1.1.0"
---

# EasyEDA Schematic Style

Make schematics easy to follow along signal paths and check pin by pin. The user's chosen style, latest reference sheets, and authorized scope take precedence.

## Establish scope and a baseline

1. Read the project's boards, schematics, and sheet list. Identify editable sheets, any reference sheets, and protected objects. Treat reference sheets as read-only and restrict writes to authorized sheet IDs. Proceed when existing authorization is clear.
2. Obtain current native data and rendered views of the target sheets and any available reference sheets. Users may have moved, renumbered, or replaced components; do not reuse stale designator or coordinate assumptions.
3. Record stable component identities, actual pins and nets, no-connect (NC) states, values, footprints, and assembly properties. Preserve them during formatting-only work. Make electrical changes only within an explicitly authorized scope.

When reviewing a manual redraw, compare the issued drawing with a fresh read of the user’s saved revision. Inspect both ends of each changed branch in the manufacturing netlist. If the user fixes an issue during review, retain the initial finding and use a fresh export for the final result. Learn layout choices from repeated, electrically verified examples.

## Draw and organize

Read the [schematic style guide](references/schematic-style-guide.md). When a reference sheet is available, extract its layout and typography. Otherwise, use the guide's general principles with available fonts and project defaults; do not require the user to supply a reference or choose typography before proceeding. For an empty sheet, use the supplied circuit plan and authorized connections, and identify missing electrical requirements rather than inventing them from formatting conventions.

For MCP or scripted editing, also read the [EasyEDA API notes](references/easyeda-api-notes.md) and verify interfaces against the documentation available in the current environment. This skill requires no fixed server name, session, operating-system path, or bundled helper script.

- Group core devices, supporting circuitry, and interfaces by function. Leave room for headings, labels, and wire bends.
- Keep a feedback divider, crystal load network, or local decoupling bank legible as one circuit. Where a long supply rail only repeats a connection across independent branches, use short branches with verified electrical supply flags.
- Read actual pin positions before moving, rotating, or replacing a component, then read them back afterward. Similar symbols can have different pin orientations.
- Preserve reference designators and dynamic name expressions. Adjust annotation placement, orientation, and visibility to remove overlap and duplicate labels.
- Use ordinary text or non-electrical graphics for interface summaries. List nets, directions, and destinations without adding isolated electrical wires or ports for decoration.

## Execute and verify

Work by sheet or functional block and retain a pre-edit snapshot. Check the active sheet and affected objects before each change. If the user has changed relevant content, refresh the data and revise the plan.

- **Electrical verification:** Compare actual component-pin-net relationships, NC states, values, footprints, and assembly properties. Distinguish existing ERC/DRC findings from newly introduced ones.
- **Assembly cleanup:** When requested, check placed schematic units, per-board manufacturing netlists and exported BOM line items as described in the [API notes](references/easyeda-api-notes.md#6-reviewing-a-manual-edit-and-assembly-cleanup). Account for multi-unit devices, functional board contacts and any existing PCB placements.
- **Visual verification:** Save and export again. Inspect the complete sheet and detailed views for grouping, labels, junctions, borders, and interface destinations.
- **Scope verification:** Confirm protected objects remain unchanged. Do not automatically copy, update, or create review signatures and completion marks.

Report the scope, checks actually performed, and unresolved issues. Follow the current project's rules for do-not-populate (DNP) parts, test points, ground topology, sheet size, and numbering. Do not turn one project's choices into universal hardware requirements. This skill grants no additional permission to purchase, publish, or modify other projects.

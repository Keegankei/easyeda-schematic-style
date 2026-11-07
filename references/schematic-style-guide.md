# Schematic Style Guide

This guide defines reading order and presentation principles for schematics of different sizes. Circuit topology, components, net names, and drawing templates belong to the current project.

## 1. Page layout and functional regions

Use a clear hierarchy: **functional region → core device → pins and supporting circuitry → cross-sheet destinations**.

- A simple sheet can read from input through local processing to output. Divide complex sheets into functional regions separated by whitespace.
- Place headings above their regions. Allow enough room around core devices for complete supporting circuits and annotations before reducing unused space.
- Align repeated circuits and related components horizontally or vertically. Do not shrink a drawing by overlapping text or hiding required labels.
- Retain the current border and title block. Check actual dimensions and usable drawing area rather than relying on a paper-size label.
- Schematic placement communicates connections; it does not prescribe PCB placement.

## 2. Local wiring

These conventions express existing or explicitly designed connections. They do not justify adding components, changing bias networks, or inferring circuit topology.

| Circuit relationship | Recommended presentation |
|---|---|
| Decoupling on one supply | Arrange capacitors side by side, with a short supply rail and the correct ground return. Make each branch identifiable. |
| Resistive feedback divider | When this topology is already used, show the complete divider and its midpoint connection to the feedback pin. |
| Configuration resistor | Show the local connection from the configuration pin through its resistor to the specified rail or ground. Avoid fragmenting it into disconnected labels. |
| Pull-up or pull-down | Show the signal node, resistor, and bias source together so the default state is readable. |
| Reset, enable, or open-drain interface | Show existing local bias components and the cross-sheet control net, rather than only an isolated signal name. |
| Series component | Place it along the relevant signal path while preserving actual pin assignments. |
| Long-distance or cross-sheet connection | Use consistent net names or the project's port convention. Add direction and destination notes when useful. |

Prefer orthogonal wiring and avoid unnecessary detours. Make T-junctions identifiable and minimize crossings between different nets. Verify connectivity from the actual netlist rather than color or visual contact alone.

Keep supply and ground symbols near their branches to avoid long loops around entire regions. Orient symbols to fit the drawing while preserving their names and electrical meaning. Formatting does not determine whether grounds should be split or connected at a single point.

## 3. Component and net annotations

- Place IC and connector reference designators above or near the upper-left corner. Put part names below or in clear space away from pins and wires.
- For vertical resistors and capacitors, place designators and values on separate lines to the right. For horizontal parts, usually place the designator above and the value below. Adapt to unusual symbols.
- Show values for passive components and part names for ICs and connectors. Preserve expressions such as `={Value}` and `={Manufacturer Part}` instead of replacing them with detached text.
- Keep net labels close to the relevant segment, preferably horizontal. A continuous local net usually needs one readable label; separated segments should remain individually identifiable.
- When a supply symbol already displays a net name, hide redundant wire text if needed. Do not remove electrical associations to eliminate visual duplication.
- Preserve inheritance when font, color, or size is `null`; do not interpret it as zero size or a fixed color.

## 4. Extract and apply a style

When reference sheets are available, inspect both native properties and rendered output. Do not guess fonts, sizes, or wire widths from a screenshot alone.

| Element | Properties to capture | Default principle without a reference |
|---|---|---|
| Page or interface-summary heading | Font, size, color, alignment, and spacing | Highest text level, clearly distinct from regional headings |
| Functional-region heading | Font, size, color, and position | More prominent than component annotations; consistent within its level |
| Interface destination or local note | Size, line spacing, and alignment | Short statements, broken into readable lines |
| Reference designator, value, or part name | Size, orientation, and relative position | Near the editor's normal annotation size, readable at detail scale |
| Net or supply name | Visible property, color, and orientation | Follow the theme and use consistent treatment |
| Wire | Width, line style, color, or inheritance | Follow project defaults and keep junctions clear |

Use the editor's size definitions. Do not directly convert them to print points or PCB millimeters. Recheck text bounds after changing sizes, especially for multiline notes, long part names, and text near the title block.

Use fonts available in the target environment. If a reference font is unavailable, choose an available substitute and report it. Keep reusable guidance independent of personal fonts, custom title blocks, and one machine's theme.

## 5. Interface summaries

Derive cross-sheet interfaces from current connections. A useful summary includes:

| Field | Content |
|---|---|
| Net name | Exact electrical net name |
| Direction | Input, output, bidirectional, or common connection relative to this sheet |
| Destination | Other sheet, module, or connector |
| Purpose | Brief function, including pass-through relationships when needed |

Use annotations or non-electrical graphics rather than dangling wires as table rows. There is no need to list every internal net. Do not connect NC pins to make a summary appear complete. Distinguish connector pass-through signals from connections to local device pins.

## 6. Completion checks

1. Electrical relationships and assembly properties match the authorized task; formatting-only work preserves the baseline.
2. Whole-sheet and detailed exports are readable, with no overlap among headings, labels, wiring, and borders.
3. The saved state has been read back, new ERC/DRC findings checked, and unresolved pre-existing findings identified.
4. Protected content and review marks are unchanged. Automated verification is not presented as a user-signed review.

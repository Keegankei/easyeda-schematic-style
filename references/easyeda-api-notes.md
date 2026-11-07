# EasyEDA API Notes

Use the official MCP, CLI, or extension API available in the current environment. Read the installed version's documentation before writing calls: method signatures, enumerations, return values, and native formats can change.

## 1. Identify objects and check state

- Locate the current project, board, and sheet by their actual IDs. Verify the active sheet and authorized scope before mutations.
- Record stable component identities, pin numbers and coordinates, wires, net flags, and text properties. Display names and reference designators can change and are not sufficient as unique identities.
- Distinguish physical components, sheet frames, net flags, and symbol units. Multiple symbol units may represent one physical component; do not treat all returned objects alike.
- After switching sheets, wait for readiness and read target objects to confirm access. Check each call's success status and returned objects, not only the process exit code.
- If a call returns an empty value, fails, or produces unexpected state, read back what happened before adapting the operation. Avoid duplicate creation or deletion after partial success.

## 2. Coordinates, rotation, and pins

API coordinates and native data may use different directions or units. Confirm the transformation, calculate in one coordinate system, and convert at the boundary. Do not mask direction errors with absolute values.

Use actual pin positions relative to the component origin when moving or rotating a symbol. Check mirrored symbols, multi-unit parts, and different libraries separately. Similar part names or footprints do not guarantee identical pin orientation. Read pin positions and nets again afterward.

Do not move pins during text-only cleanup. Attach NC markers to actual pins rather than imitating them with ordinary text.

## 3. Wires and nets

The following names are useful documentation search terms. Confirm current signatures before use.

| Capability | API search terms |
|---|---|
| Read components and pins | `sch_PrimitiveComponent.getAll`, `getAllPinsByPrimitiveId` |
| Adjust component placement | `sch_PrimitiveComponent.modify` |
| Create named wires | `sch_PrimitiveWire.create` |
| Create supply and ground symbols | `sch_PrimitiveComponent.createNetFlag` |
| Read and modify attributes | `sch_PrimitiveAttribute.getAll`, `modify` |
| Work with ordinary annotations | `sch_PrimitiveText` |

- Determine replacement wires from actual connectivity, not proximity alone. Check shared branches and user annotations separately.
- Connect wires to the intended pins and avoid NC pins, unintended overlaps, and crossings between different nets. A wire at a pin must actually meet that pin; a nearby matching label does not prove contact.
- After creating a named wire, read back its name attribute before adjusting placement or visibility. Do not repeatedly add independent labels to compensate for an unchecked creation failure.
- Keep supply or ground flags consistent with their wire nets. After replacing or moving a component, inspect its old location for residual wires and flags.
- Preserve the project's ground topology. Non-electrical interface summaries do not add electrical branches.

## 4. Text and attributes

Handle `Designator` and `Name` separately. `Name` may contain a dynamic property expression; preserve its value, expression, and parent association when adjusting display properties.

A net object may have several name attributes. Identify which one is visible before removing duplication. Do not apply one generic offset to designators, values, pin labels, and title-block fields.

For multiline text, specify the anchor and alignment explicitly. Compare API readback, native alignment, and rendered output; a successful response alone does not prove correct placement. If the current modification interface cannot reliably apply alignment, recreate an authorized ordinary annotation using a verified creation interface. Confirm the new object exists before deleting the old one. Preserve content, font, color, and hierarchy; do not extend this workaround to electrical objects or review marks.

## 5. Verification and delivery

Compare actual nets before and after editing using stable component identities and pin numbers, including multi-unit symbols and NC states. Formatting-only work also preserves values, footprints, assembly properties, and reference designators.

Save and export whole-sheet and detailed views. Check for overlap, duplicates, out-of-frame content, and dangling endpoints. Report the checks actually performed and unresolved findings, keeping presentation verification distinct from circuit-design review.

Reusable automation obtains IDs and paths from the current session. Do not embed real project exports, credentials, personal directories, or fixed session identifiers. Use minimal synthetic examples when publishing demonstrations.

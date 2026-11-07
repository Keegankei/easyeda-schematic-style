# Contributing

Contributions should help an agent produce clearer schematics while preserving user intent, electrical relationships, and editing scope.

## Propose a focused change

- Describe the concrete problem and the behavior the change improves.
- Keep the agent entry point short. Put detailed layout guidance in the style guide and automation details in the API notes.
- Treat project-specific choices as inputs, not universal requirements. Do not mandate particular components, ground arrangements, fonts, page sizes, or assembly options.
- Distinguish observed version behavior from API guarantees. For a compatibility issue, include the EasyEDA version and a minimal reproduction.
- Preserve relative links and keep the package self-contained.

## Examples and issue reports

Use a small synthetic schematic or a text description that demonstrates the issue. Include the expected result, the observed result, and relevant tool responses with private data removed.

Do not include real customer designs, project exports, access tokens, session IDs, personal directories, author signatures, or unreviewed screenshots. Supply only the artifacts necessary to understand the problem.

## Check the result

For documentation changes:

1. Check Markdown rendering and internal links.
2. Confirm `SKILL.md` has valid YAML frontmatter with `name` and `description`, and that its name matches the folder.
3. Read the instructions against a realistic request involving a protected reference sheet and recently renumbered components. Confirm the instructions preserve the current data and editing scope.
4. Check the changed files for real identifiers, private paths, credentials, and project-specific assumptions.

For changes to editing guidance, also use a disposable synthetic project when practical. Compare the actual netlist and assembly properties before and after a formatting-only operation, inspect the saved exports, and distinguish old ERC/DRC findings from new ones.

Report what was tested. Do not describe a text review as a live EasyEDA integration test.

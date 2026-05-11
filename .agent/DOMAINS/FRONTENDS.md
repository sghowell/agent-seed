# Frontend And Product Interface Overlay

Use this overlay for user-facing interfaces, dashboards, tools, visualizations, product workflows, browser apps, mobile apps, design systems, or documentation experiences.

## Product Intent And Workflow

Before changing UI, understand:

- target users,
- primary workflow,
- user goal,
- data contract,
- failure states,
- success criteria.

Build the actual usable workflow, not a decorative shell.

## Accessibility

Consider:

- semantic structure,
- labels,
- focus order,
- keyboard use,
- contrast,
- screen-reader behavior,
- reduced motion,
- error announcements.

## Visual Verification

For visual changes, provide evidence:

- screenshots,
- browser checks,
- visual regression output,
- viewport checks,
- interaction checks,
- loading and error states.

## Responsive Behavior

Check:

- mobile,
- tablet,
- desktop,
- narrow and wide layouts,
- text fitting,
- no incoherent overlap,
- stable control dimensions.

## Browser And Device Coverage

Record:

- browsers tested,
- devices or viewports,
- rendering mode,
- accessibility tooling,
- known limitations.

## State And Data Contracts

Review:

- API assumptions,
- loading states,
- empty states,
- error states,
- optimistic updates,
- stale data behavior,
- privacy-sensitive UI,
- analytics or telemetry impact.

Use `.agent/TEMPLATES/INTERFACE_CONTRACT.md` when UI depends on a stable data or API contract.

## Performance

Consider:

- interaction latency,
- bundle size,
- rendering cost,
- Core Web Vitals when relevant,
- image and media loading,
- expensive animations,
- network behavior.

## Specialist Review

Request frontend/product/accessibility review for major workflows, accessibility-sensitive changes, visual redesigns, public user interfaces, privacy-sensitive UI, or changes where screenshots/browser evidence are needed.

# Pantry iOS - Claude Code Instructions

This repository is for a native SwiftUI iPhone app called Pantry.

## Core rules
- Use SwiftUI only
- Use Swift only
- iPhone-first only
- Do not use web technologies
- Do not introduce React, HTML, CSS, or JavaScript
- Keep architecture simple, modular, and production-leaning
- Prefer reusable design-system components over repeated ad hoc styling
- Every new screen should be previewable in SwiftUI previews

## Design source of truth
- `references/pantry-ui-spec.md`

## Build order
1. Design system tokens and theme
2. Reusable UI components
3. Static screen shells
4. Navigation structure
5. View models / app state
6. Backend integration
7. Polish and QA

## Design constraints
- Warm cream background
- White cards on cream
- Orange accent
- Serif headings only where specified
- SF Pro for interface/body
- 20pt standard horizontal margins
- Rounded, warm, premium, cookbook-like feeling
- Avoid generic AI-app aesthetics
- Avoid dashboard/SaaS visual language
- Keep animations subtle

## Implementation behavior
Before making large changes:
1. Summarize the plan
2. List files to create or modify
3. Implement in small, verifiable steps

Do not try to build the full app in one pass.
Start with the design system and components first.

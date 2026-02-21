---
name: write-spec
description: >
  Write a feature spec or PRD from a problem statement or feature idea.
  Generates a structured document with problem statement, user stories,
  requirements, success metrics, and open questions. Invoke as $write-spec.
---

# Write Spec

Write a feature specification or product requirements document (PRD).

## Workflow

### 1. Understand the Feature

Ask the user what they want to spec. Accept any of:
- A feature name ("SSO support")
- A problem statement ("Enterprise customers keep asking for centralized auth")
- A user request ("Users want to export their data as CSV")
- A vague idea ("We should do something about onboarding drop-off")

### 2. Gather Context

Ask the user for the following. Be conversational — do not dump all questions at once. Ask the most important ones first and fill in gaps as you go:

- **User problem**: What problem does this solve? Who experiences it?
- **Target users**: Which user segment(s) does this serve?
- **Success metrics**: How will we know this worked?
- **Constraints**: Technical constraints, timeline, regulatory requirements, dependencies
- **Prior art**: Has this been attempted before? Are there existing solutions?

### 3. Pull Context from Connected Tools

**With a connected project tracker** (Linear/Asana/Jira/ClickUp): Search for related tickets, epics, or features. Pull in any existing requirements or acceptance criteria. Identify dependencies on other work items.

**Without connected tools**: Work entirely from what the user provides. Ask: "Are there any related tickets, prior specs, or design docs you can share?"

**With a connected knowledge base** (Notion/Confluence): Search for related research documents, prior specs, or design docs. Pull in relevant user research findings.

**Without connected tools**: Ask the user to paste any relevant prior work, research findings, or reference documents.

**With a connected design tool** (Figma/Sketch): Pull related mockups, wireframes, or design explorations.

**Without connected tools**: Ask if there are any designs to share (screenshots or descriptions work fine).

### 4. Generate the PRD

Produce a structured PRD with these sections. See the **feature-spec-knowledge** skill for detailed guidance on user stories, requirements categorization, acceptance criteria, and success metrics.

Use the template at `templates/prd-template.md` as a starting point.

- **Problem Statement**: The user problem, who is affected, and impact of not solving it (2-3 sentences)
- **Goals**: 3-5 specific, measurable outcomes tied to user or business metrics
- **Non-Goals**: 3-5 things explicitly out of scope, with brief rationale for each
- **User Stories**: Standard format ("As a [user type], I want [capability] so that [benefit]"), grouped by persona
- **Requirements**: Categorized as Must-Have (P0), Nice-to-Have (P1), and Future Considerations (P2), each with acceptance criteria
- **Success Metrics**: Leading indicators (change quickly) and lagging indicators (change over time), with specific targets
- **Open Questions**: Unresolved questions tagged with who needs to answer (engineering, design, legal, data)
- **Timeline Considerations**: Hard deadlines, dependencies, and phasing

### 5. Review and Iterate

After generating the PRD:
- Ask the user if any sections need adjustment
- Offer to expand on specific sections
- Offer to create follow-up artifacts (design brief, engineering ticket breakdown, stakeholder pitch)

## Output Format

Use markdown with clear headers. Keep the document scannable — busy stakeholders should be able to read just the headers and bold text to get the gist.

## Tips

- Be opinionated about scope. A tight, well-defined spec is better than an expansive vague one.
- If the user's idea is too big for one spec, suggest breaking it into phases and spec the first phase.
- Success metrics should be specific and measurable, not vague ("improve user experience").
- Non-goals are as important as goals. They prevent scope creep during implementation.
- Open questions should be genuinely open — do not include questions you can answer from context.

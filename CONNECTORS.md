# Connected Apps Configuration

## How tool references work

Skills reference external tools by category rather than by specific product name.
When a Connected App is available in Codex, it will be used automatically.
When it is not available, skills fall back to requesting manual input from the user.

## Connector categories

| Category | Connected App (if available) | Fallback behavior |
|---|---|---|
| **Chat** | Slack, Microsoft Teams | Ask user: what was accomplished, blockers, decisions made, next steps |
| **Project Tracker** | Linear, Asana, Jira, ClickUp, Monday.com | Ask user to describe roadmap items, ticket statuses, or priorities |
| **Knowledge Base** | Notion, Confluence, Guru, Coda | Ask user to paste or upload relevant documents |
| **Design** | Figma, Sketch, Adobe XD | Ask user to share screenshots or describe designs in text |
| **Product Analytics** | Amplitude, Pendo, Mixpanel, Heap | Ask user to paste metrics data (table, CSV, or prose description) |
| **User Feedback** | Intercom, Productboard, Canny, UserVoice | Ask user to paste feedback excerpts or describe themes |
| **Meeting Transcription** | Fireflies, Gong, Dovetail, Otter.ai | Ask user to paste meeting notes or key takeaways |

## Fallback pattern used in all skills

Every skill uses this two-branch pattern when referencing external tools:

```
**With connected [category]**: [what the skill does automatically]
**Without connected tools**: Ask the user to [what to request manually].
  Accept any format: prose description, table, screenshot, or pasted text.
```

## Notes on specific skills

- **`$competitive-brief`**: Uses web search as the primary research source. Connected apps supplement but are not required.
- **`$synthesize-research`**: User-pasted text or uploaded files are the primary input. Connected tools (user feedback, meeting transcription) supplement.
- **`$metrics-review`**: Analytics platforms (Amplitude, Pendo) may not be available as Connected Apps. The primary path is user-provided data.
- **`$stakeholder-update`**: Uses the most connectors. Each has a fallback, so the skill works fully without any connected apps.

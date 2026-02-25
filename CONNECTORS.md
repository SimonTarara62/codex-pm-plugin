# Connected Apps Configuration

## How tool references work

Skills reference external tools by category rather than by specific product name.
When a Connected App is available in Codex, it will be used automatically.
When it is not available, skills fall back to requesting manual input from the user.

## Connector categories

| Category | Connected App (if available) | Fallback behavior |
|---|---|---|
| **Chat** | Slack, Microsoft Teams | Ask user: what was accomplished, blockers, decisions made, next steps |
| **Project Tracker** | Jira, Linear, Asana, ClickUp, Monday.com | Ask user to describe roadmap items, ticket statuses, or priorities |
| **Knowledge Base** | Confluence, Notion, Guru, Coda | Ask user to paste or upload relevant documents |
| **Calendar** | Google Calendar | Ask user for key dates, upcoming milestones, team availability, and upcoming meeting context |
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

## Notes on specific connectors

- **Atlassian Rovo**: Connecting Rovo covers two categories at once — Jira maps to **Project Tracker** and Confluence maps to **Knowledge Base**. Skills will use both automatically.
- **Google Calendar**: Calendar events may contain links to Google Drive documents (agendas, meeting notes, pre-read materials). When a calendar is connected, follow these links to retrieve additional context from Drive.

## Notes on specific skills

- **`$competitive-brief`**: Uses web search as the primary research source. Connected apps supplement but are not required.
- **`$synthesize-research`**: User-pasted text or uploaded files are the primary input. Connected tools (user feedback, meeting transcription) supplement.
- **`$metrics-review`**: Analytics platforms (Amplitude, Pendo) may not be available as Connected Apps. The primary path is user-provided data.
- **`$stakeholder-update`**: Uses the most connectors. Each has a fallback, so the skill works fully without any connected apps.

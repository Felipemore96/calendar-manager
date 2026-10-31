# Config example

The agent reads these values from the routine prompt (see `prompts/routine.md`). This file only shows the shape. **Don't put real values here**, since this repo is public.

```
CALENDAR_NAME: <name of the shared calendar, exactly as shown in Google Calendar>
CALENDAR_ID: <optional, e.g. abc123@group.calendar.google.com>
OWNER_NAMES: <name 1>, <name 2>
TIMEZONE: Europe/Amsterdam
GO_LIVE_DATE: <YYYY/MM/DD, emails before this date are ignored>
MODE: dry-run
```

| Key | Required | Meaning |
|---|---|---|
| `CALENDAR_NAME` | one of the two | Target calendar, looked up by exact name |
| `CALENDAR_ID` | one of the two | Target calendar ID; wins over the name when both are set |
| `OWNER_NAMES` | no | Helps the agent recognise whose booking an email is about |
| `TIMEZONE` | yes | Default timezone when an email gives none |
| `GO_LIVE_DATE` | yes | Lower bound for the Gmail search |
| `MODE` | yes | `dry-run` reports only; `live` writes events and labels |

# Routine prompt template

Copy everything below the line into the routine's prompt on claude.ai and fill in the placeholders. Don't commit the filled-in version.

---

Run the Calendar Manager agent as described in `CLAUDE.md` in this repository. Follow it exactly, including the guardrails, and use `docs/event-formats.md` for event formats. Don't modify, commit or push anything in the repository.

Private config:

```
CALENDAR_NAME: <shared calendar name>
CALENDAR_ID: <optional calendar ID>
OWNER_NAMES: <name 1>, <name 2>
TIMEZONE: Europe/Amsterdam
GO_LIVE_DATE: <YYYY/MM/DD>
MODE: dry-run
```

End with the run summary from `CLAUDE.md` section 10.

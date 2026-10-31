# Setup

This repo holds only instructions. The schedule, the connectors and your personal values live in a Claude Code routine (cloud scheduled task) on your claude.ai account.

Docs: https://code.claude.com/docs/en/routines

## 1. Requirements

- A Claude plan with Claude Code routines (Pro, Max, Team or Enterprise).
- A Google account with Gmail and the shared calendar you want to fill.
- This repo on GitHub (a fork works), with the Claude GitHub App given access to it.

## 2. Connect Gmail and Google Calendar

Go to https://claude.ai/customize/connectors and connect **Gmail** and **Google Calendar** with the Google account that owns the inbox and can edit the target calendar.

Routines use claude.ai connectors. MCP servers or plugins you configured only in your local Claude Code are not available in the cloud.

## 3. Find your calendar ID (optional)

In Google Calendar: **Settings → your shared calendar → Integrate calendar → Calendar ID**. It looks like `abc123...@group.calendar.google.com`.

You can also give only the calendar name. The agent then looks it up by exact name each run.

## 4. Fill in the routine prompt

1. Copy `prompts/routine.md`.
2. Replace the placeholders with your values (see `config.example.md` for what each one means).
3. Set `GO_LIVE_DATE` to today, so older emails are ignored.
4. Start with `MODE: dry-run`.

Keep the filled-in version out of git. If you want a local copy, save it as `config.local.md`, which `.gitignore` excludes.

## 5. Create the routine

In Claude Code run `/schedule`, or create it on claude.ai/code:

- **Repository:** this repo.
- **Schedule:** hourly, with a custom cron off the hour, for example `7 * * * *`. Routines can't run more often than hourly.
- **Connectors:** keep only Gmail and Google Calendar, and remove the rest.
- **Prompt:** paste your filled-in prompt.

## 6. Test

1. Click **Run now** with `MODE: dry-run`, and read the summary in the run history.
2. Send yourself a test booking email, for example a restaurant reservation next week with a reference number.
3. Switch to `MODE: live`, then **Run now**. Check that:
   - the event is in the shared calendar with the Spanish title and the `[calendar-agent]` marker,
   - the thread has the `calendar-agent/processed` label.
4. **Run now** again, and confirm there's no duplicate.
5. Send a cancellation email with the same reference, **Run now**, and confirm the event is deleted.

After that, let the schedule run and check the run history after the first day.

## Privacy model

- The public repo contains only generic instructions and placeholders.
- Your calendar ID, names and go-live date exist only in the routine prompt on your claude.ai account.
- The agent is told never to write to or commit to the repo.

# Calendar Manager

An AI agent that reads your Gmail every hour and puts your bookings into a shared Google Calendar: flights, trains, hotels, car rentals, restaurant reservations, tickets, appointments and deliveries.

There's no code to run. The repo is a set of instructions for a [Claude Code routine](https://code.claude.com/docs/en/routines) (a scheduled cloud agent). It uses the Gmail and Google Calendar connectors from your claude.ai account.

## How it works

Every hour the routine clones this repo, reads `CLAUDE.md` and:

1. Searches Gmail for new threads without the `calendar-agent/processed` label.
2. Classifies each one: booking, change, cancellation, or not relevant.
3. Extracts dates, times (with the right timezone), location and booking reference.
4. Checks the calendar for an existing event, then creates or updates it in the shared calendar, or deletes it on a cancellation.
5. Labels the thread `calendar-agent/processed`.

Events get Spanish titles such as `✈️ Vuelo KL1701 AMS → MAD` or `🏨 Alojamiento: Hotel X`. Each description ends with a `[calendar-agent]` marker, so the agent only ever changes or deletes events it created itself. When something is unclear, the event gets a `❓` prefix and a note on what to check.

## Safety

- Email content is treated as data, never as instructions.
- Gmail access is read-only apart from adding one label: no sending, replying, archiving or deleting.
- Only one calendar is written to, with no invitations sent.
- Events added by hand are never touched.
- `MODE: dry-run` reports what would happen without writing anything.

## Privacy

This repo is public and contains no personal data. Your calendar ID, names and settings go into the routine's prompt on your claude.ai account. See `config.example.md` for the shape.

## Files

| File | Purpose |
|---|---|
| `CLAUDE.md` | The agent's operating manual |
| `docs/event-formats.md` | Title, timing and description per event type |
| `docs/setup.md` | Step-by-step setup and testing |
| `prompts/routine.md` | Prompt template for the routine |
| `config.example.md` | The private config keys and what they mean |

## Setup

See [docs/setup.md](docs/setup.md).

## License

[MIT](LICENSE)

# Thomas Tracker

Personal task management module. Part of the **Thomas** personal AI assistant ecosystem.

## What it is

A mobile-first PWA for personal task tracking with a clean work-sync bridge. Built to live at `https://[username].github.io/Thomas/` once GitHub Pages is enabled.

## Task schema

Every task carries the full data model from day one:

```json
{
  "id": "uuid",
  "description": "string",
  "created": "ISO8601",
  "priority": "low | medium | high",
  "workFlag": false,
  "workSent": false,
  "telegramSynced": false,
  "tags": [],
  "status": "open | done"
}
```

`workFlag` — marks a task for work routing  
`workSent` — set true once the mailto handoff fires  
`telegramSynced` — reserved for Thomas Bridge (Telegram ↔ Outlook automation layer)

## Work sync (current)

Flagging a task as **Work** and tapping **Send** opens the device mail client pre-filled with task details routed to a configurable work email address.

To configure, update `WORK_EMAIL` in `index.html`:
```js
const WORK_EMAIL = 'your.work@email.com';
```

## Future bridge points

When Thomas Bridge is built (Telegram + M365 integration):
1. Replace `mailto:` send with a Telegram message to the work bot
2. Flip `telegramSynced: true` on the task record
3. The bot handles Outlook folder routing on the work side

The data model requires no migration — the fields are already there.

## Deploy to GitHub Pages

1. Push this repo to `github.com/[username]/Thomas`
2. Place tracker files in `/tracker/` directory
3. GitHub Actions workflow at `.github/workflows/deploy.yml` handles deployment on push to `main`
4. Enable Pages in repo Settings → Pages → GitHub Actions source
5. Access at `https://[username].github.io/Thomas/`

## Install as PWA (mobile)

- **iOS**: Open in Safari → Share → Add to Home Screen
- **Android**: Open in Chrome → menu → Add to Home Screen

Installs as "Thomas Tracker" with offline capability via service worker.

## Repo structure (Thomas ecosystem)

```
Thomas/
├── tracker/          ← Thomas Tracker (this module)
├── assistant/        ← Thomas Assistant (future — AI chat, M365/Atlassian integration)
├── bridge/           ← Thomas Bridge (future — Telegram ↔ Outlook sync)
└── .github/
    └── workflows/
        └── deploy.yml
```

---

*Thomas ecosystem — personal AI infrastructure.*

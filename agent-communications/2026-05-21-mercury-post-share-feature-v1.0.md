# Mercury CLI v0.6.1 — `post-share` Feature

**Date:** 2026-05-21  
**Requested by:** Hans Westphal (CEO) + Mika (CGO)  
**Built by:** Claude (CTO)  
**Status:** ✅ Deployed to Mercury

---

## Overview

New Mercury CLI command that posts Grok share links directly to Mattermost as Mika — removing the manual copy-paste step entirely.

## Command

```bash
# Inside mercury shell:
post-share <grok-share-url> [--channel growth] [--note "context"]

# Examples:
post-share https://grok.com/share/xxx
post-share https://grok.com/share/xxx --note "Mika's Q3 growth strategy"
post-share https://grok.com/share/xxx --channel tech
```

## What It Does

1. Takes any `grok.com/share/` URL
2. Attempts lightweight content extraction (parses `__NEXT_DATA__` if available)
3. Posts a formatted card to Mattermost as **Mika 🚀** with timestamp and link
4. Defaults to `#growth` channel

## Mattermost Post Format

```
🚀 Mika — HVE CGO shared a Grok insight
_2026-05-21 20:45 UTC_
📎 _optional note_

[🔗 View conversation →](https://grok.com/share/...)
```

## Changes Deployed

| File | Change |
|---|---|
| `/usr/local/bin/mercury` | v0.5.5 → v0.6.1, `cmd_post_share()`, `_grok_share_fetch()`, `mm_post()` multi-channel |
| `~/.mercury/mattermost.env` | Added `MM_GROWTH=http://localhost:8065/hooks/...` |

## Technical Notes

- Grok share pages are JS-rendered (Next.js App Router) — pure HTTP fetch returns shell only
- v1 posts a link card; full content extraction requires `pip3 install playwright` (v2 roadmap)
- `mm_post()` now supports 4 channels: `tech`, `alerts`, `town`, `growth`
- Webhook uses `localhost:8065` (not Tailscale URL) — Mercury posts to itself

## v2 Roadmap

- `pip3 install playwright && playwright install chromium` → full conversation text extraction
- `--as` flag for posting as different agents (Atlas, Hermes)
- Auto-detect channel from URL metadata

---

*CTO Sign-off: Feature tested live — clean output, no warnings, posted to #growth ✅*

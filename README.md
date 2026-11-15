# TG bot: overview

> **Source code is private.** This repository describes the system's logic and architecture.

**A Telegram bot that runs a music community on its own: it keeps a Ukrainian electronic-music group in
Madrid free of spam, and finds and drafts event announcements so the owner only has to tap "publish".**

![Python](https://img.shields.io/badge/Python-3-3776AB)
![Telegram](https://img.shields.io/badge/Telegram-Bot%20API-26A5E4)
![SQLite](https://img.shields.io/badge/SQLite-state-003B57)
![systemd](https://img.shields.io/badge/systemd-user%20unit-informational)

## Self-running group admin

- **New-member quarantine:** for the first 24 hours no links, forwards, @-mentions or buttons
- Spam patterns apply to everyone; every violation is a strike, **two strikes → ban** with messages revoked
- A sweeper removes join/leave noise about deleted accounts every 30 minutes; the bot stays silent in the
  group itself (no welcome or "user banned" notices)
- Owner commands in DM: stats, unban; an optional join-request captcha

## Finding announcements

- **Daily:** scans Resident Advisor listings for every Spanish area over the next 90 days and keeps events whose
  lineup includes a Ukrainian artist (by the artist's country on RA or a watchlist)
- **Weekly:** picks special, non-routine Madrid club nights
- RA has no public API; the bot uses the GraphQL endpoint RA's own site uses, a few dozen requests per scan,
  and fails loudly rather than posting nonsense if it changes

## Publishing flow

Each find arrives in the owner's DM as a ready draft: **publish now, schedule** (presets or a custom time) or
**skip**. Published posts land in the right forum topic (festivals vs. Madrid clubs).

## My role

Designed and built it, and run it on my home server. Main themes: low-friction moderation and turning
an unofficial data source into a curated feed.

# HardBlock
# HardBlock

Competitive Call of Duty, broken down.

HardBlock is a self-hosted website focused on the Competitive Call of Duty esports scene. The goal is to combine match coverage, player and team statistics, matchup analysis, editorial content, and eventually scrim tracking into one platform.

## Vision

HardBlock is meant to be a hybrid of:
- stats hub
- matchup analysis site
- CDL editorial platform

The site will track:
- recent match results
- upcoming matches
- player stats
- team stats
- head-to-head comparisons
- predictions and analysis
- future scrim data with clear source labeling

## Core principles

- Keep official data separate from third-party and scrim data
- Make source attribution visible
- Build admin tools early
- Launch a focused MVP before expanding into advanced features
- Prioritize clean UX and trustworthy data presentation

## Planned stack

### Infrastructure
- Proxmox VE on self-hosted hardware
- Ubuntu Server VM
- Docker Compose
- Reverse proxy with HTTPS
- PostgreSQL backups and VM snapshots

### Application
- Next.js
- TypeScript
- PostgreSQL
- Prisma
- Tailwind CSS

## MVP pages

- Home
- Matches
- Match Detail
- Teams
- Team Detail
- Players
- Player Detail
- Articles
- Article Detail
- About
- Admin Dashboard

## Initial data sources

- COD Esports Fandom Wiki
- Breaking Point

## Roadmap

### Phase 1
- Infrastructure setup
- App scaffold
- Database schema
- Public MVP pages

### Phase 2
- Admin tools
- Raw ingest pipeline
- Fandom data ingestion
- Stats pages

### Phase 3
- Breaking Point ingestion
- Predictions and editorial integration
- Head-to-head tools

### Phase 4
- Reliability improvements
- Monitoring and backups
- Scrim support

## Status

This project is currently in early planning/buildout.

## Notes

HardBlock is being built as a self-hosted project with an emphasis on performance, clean design, and useful competitive insight for CDL fans.

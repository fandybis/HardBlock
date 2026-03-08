# HardBlock Technical Blueprint

## Overview

HardBlock is a self-hosted website built around the Competitive Call of Duty esports scene.

The platform is intended to combine:
- recent and upcoming match coverage
- player and team statistics
- matchup and head-to-head analysis
- editorial content and predictions
- future scrim tracking with clear source labeling

The goal is to build something that feels like a hybrid of a stats site, matchup hub, and CDL editorial platform.

---

## Product goals

HardBlock should:

- make Competitive Call of Duty data easier to browse and understand
- provide useful context around upcoming and completed matches
- combine stats with real analysis rather than just dumping numbers
- keep official, third-party, and scrim data clearly separated
- be self-hosted and fully under owner control

---

## Core principles

### 1. Trust the data hierarchy
Not all data is equal. HardBlock should visibly separate:
- official data
- public third-party data
- manual/admin-entered data
- scrim data
- unverified/community-sourced data

### 2. Editorial is part of the product
Analysis, predictions, and written context are not filler. They are a core part of what makes HardBlock valuable.

### 3. Build for manual control first
Admin tools should allow data to be created, corrected, reviewed, and published without direct database edits.

### 4. Launch narrow, expand deep
The first version should be focused and reliable. Advanced tools like scrim systems, deeper comparisons, and more complex stat models can come later.

---

## Infrastructure blueprint

### Physical host
- spare desktop PC
- Proxmox VE installed on bare metal

### Virtualization layout

#### VM 1: Production VM
Ubuntu Server VM used for:
- Docker host
- web application
- PostgreSQL
- worker/ingest jobs
- reverse proxy

#### VM 2: Staging VM
Optional later for:
- testing
- parser changes
- schema experiments

#### VM 3: Backup/Utility VM
Optional later for:
- backup jobs
- monitoring
- internal tooling

For the initial version, only the production VM is required.

---

## Container layout

The production VM should run Docker Compose with the following services:

### web
Handles:
- Next.js frontend
- server-rendered app routes
- public pages
- admin interface

### db
Handles:
- PostgreSQL database
- persistent application data

### worker
Handles:
- ingest jobs
- parsing
- normalization
- scheduled tasks

### proxy
Handles:
- HTTPS
- reverse proxy
- public traffic routing

### redis
Optional later for:
- caching
- rate limiting
- job queues
- session storage

---

## Application stack

### Recommended stack
- Next.js
- TypeScript
- PostgreSQL
- Prisma
- Tailwind CSS
- Recharts later for visualizations
- NextAuth or simple admin auth for protected routes

### Architecture style
Start as a monolith, not microservices.

Primary app modules:
- public site
- stats and comparisons
- editorial/content
- admin dashboard
- ingest pipeline
- source attribution layer

---

## Data architecture

HardBlock should use a three-layer data model.

### Layer 1: Raw source layer
Used to store fetched source material before parsing.

Tables:
- raw_documents
- raw_fetch_runs
- raw_parse_logs

Purpose:
- preserve source snapshots
- debug parser failures
- track source changes over time

### Layer 2: Canonical normalized layer
Used for clean internal data models.

Tables:
- teams
- players
- team_rosters
- events
- matches
- match_maps
- player_match_stats
- team_match_stats
- articles
- predictions
- sources
- ingest_runs

### Layer 3: Published/app-facing layer
Used for:
- homepage queries
- leaderboards
- matchup summaries
- player pages
- cached public views

This can be implemented through canonical tables, query helpers, and later materialized views if needed.

---

## Core database entities

### teams
Fields should include:
- id
- name
- short_name
- slug
- logo_url
- region
- active
- created_at
- updated_at

### players
Fields should include:
- id
- gamer_tag
- full_name optional
- slug
- country optional
- active
- current_team_id optional
- role optional
- headshot_url optional
- created_at
- updated_at

### team_rosters
Fields should include:
- id
- team_id
- player_id
- start_date
- end_date optional
- is_active

### events
Fields should include:
- id
- name
- slug
- season
- stage
- event_type
- start_date
- end_date

### matches
Fields should include:
- id
- event_id
- home_team_id
- away_team_id
- scheduled_at
- completed_at optional
- status
- winner_team_id optional
- score_home
- score_away
- best_of
- match_type
- source_id
- verification_status
- external_ref
- created_at
- updated_at

### match_maps
Fields should include:
- id
- match_id
- map_name
- mode
- team1_score
- team2_score
- winner_team_id
- map_order

### player_match_stats
Fields should include:
- id
- match_id
- player_id
- team_id
- kills
- deaths
- kd_ratio
- assists optional
- damage optional
- objective_time optional
- mode
- source_id
- verification_status

### team_match_stats
Fields should include:
- id
- match_id
- team_id
- overall_kd optional
- hp_win_pct optional
- snd_win_pct optional
- control_win_pct optional
- source_id
- verification_status

### articles
Fields should include:
- id
- title
- slug
- excerpt
- body
- cover_image_url optional
- published_at optional
- status
- category
- related_match_id optional
- related_team_id optional
- created_at
- updated_at

### predictions
Fields should include:
- id
- related_match_id
- predicted_winner_team_id
- predicted_score
- confidence
- analysis_summary
- published_at optional

### sources
Fields should include:
- id
- name
- source_type
- url
- attribution_text
- license_notes optional
- trust_level

### ingest_runs
Fields should include:
- id
- source_id
- started_at
- completed_at optional
- status
- items_fetched
- items_parsed
- items_failed
- notes optional

---

## Future scrim entities

These should stay separate from official/public match data.

Future tables:
- scrim_blocks
- scrim_maps
- scrim_team_stats
- scrim_player_stats
- scrim_sources

Scrim data should always carry:
- source details
- confidence level
- visibility setting
- verification status

---

## Source trust model

HardBlock should use visible source labels on public pages where appropriate.

### Source categories
- official
- public-third-party
- manual/admin-entered
- scrim
- unverified/community-sourced

### Public rules
- official match data should not be silently mixed with scrim data
- third-party data should be attributed
- manually entered values should be distinguishable internally
- unverified information should never look authoritative by accident

---

## Public site routes

### Core routes
- `/`
- `/matches`
- `/matches/[id]`
- `/teams`
- `/teams/[slug]`
- `/players`
- `/players/[slug]`
- `/articles`
- `/articles/[slug]`
- `/about`

### Phase 2 routes
- `/stats`
- `/stats/players`
- `/stats/teams`
- `/predictions`
- `/head-to-head`
- `/head-to-head/[teamA]-vs-[teamB]`

---

## Admin routes

- `/admin`
- `/admin/teams`
- `/admin/players`
- `/admin/matches`
- `/admin/articles`
- `/admin/predictions`
- `/admin/sources`
- `/admin/ingest`

Future:
- `/admin/scrims`

---

## Public page blueprint

### Homepage
Purpose:
- show what is happening now
- surface upcoming and recent matches
- highlight featured writing
- quickly communicate site value

Primary sections:
- hero
- upcoming matches
- recent results
- featured editorial
- trending teams or players
- latest content

### Matches page
Purpose:
- act as the main schedule and results hub

Primary sections:
- upcoming matches
- completed matches
- filters by event or team later

### Match detail page
Purpose:
- central page for each series

Primary sections:
- match header
- date, status, event
- scoreline
- map breakdown
- player stats
- team comparison snapshot
- prediction block
- editorial notes
- source labels

### Teams page
Purpose:
- directory of all teams

Primary sections:
- team cards or list
- logo
- name
- quick summary
- links to team pages

### Team detail page
Purpose:
- central hub for a single team

Primary sections:
- header
- roster
- recent matches
- upcoming matches
- team summary stats
- related articles

### Players page
Purpose:
- directory of players

Primary sections:
- searchable player list
- team and summary stats
- links to player pages

### Player detail page
Purpose:
- player stat summary and context page

Primary sections:
- player header
- season overview
- recent match log
- mode splits
- editorial notes

### Articles page
Purpose:
- browse all published writing

Primary sections:
- article feed
- category filters later
- featured content block

### Article detail page
Purpose:
- full editorial reading experience

Primary sections:
- title and metadata
- article body
- related team or match links
- related articles

### About page
Purpose:
- explain what the site is
- explain source hierarchy
- establish trust

Primary sections:
- project purpose
- source model
- data labeling explanation
- future vision

---

## Admin blueprint

### Admin dashboard
Should show:
- total teams
- total players
- total matches
- total articles
- recent ingest runs
- pending issues or parser failures
- upcoming matches missing predictions

### Admin teams
Should allow:
- create team
- edit team
- update logo
- set slug
- set active status

### Admin players
Should allow:
- create player
- edit player
- assign team
- manage roster relationships
- update optional metadata

### Admin matches
Should allow:
- create match
- edit match
- set event and schedule
- update score
- enter maps
- assign source and verification status

### Admin articles
Should allow:
- create draft
- edit article
- publish article
- set category
- link related team or match

### Admin predictions
Should allow:
- create prediction
- select related match
- choose winner
- set predicted score
- set confidence
- publish or draft

### Admin sources
Should allow:
- create source record
- edit attribution text
- set trust level
- store source notes

### Admin ingest
Should allow:
- view ingest runs
- inspect errors
- review unmatched entities later

---

## Ingest workflow blueprint

### Step 1: Fetch
Pull source content from a target URL.

### Step 2: Store raw document
Save:
- source
- URL
- timestamp
- fetch status
- raw content
- checksum

### Step 3: Parse into staging objects
Extract:
- teams
- players
- dates
- stats
- references

### Step 4: Normalize
Match source values to canonical database entities.

Examples:
- team aliases
- player aliases
- map name consistency
- mode name consistency

### Step 5: Review exceptions
Log unmatched or suspicious records for review.

### Step 6: Publish
Write approved normalized data into canonical app-facing tables.

---

## MVP definition

### Public MVP
- homepage
- matches page
- match detail page
- teams page
- team detail page
- players page
- player detail page
- articles page
- article detail page
- about page

### Admin MVP
- admin auth
- teams CRUD
- players CRUD
- matches CRUD
- articles CRUD
- sources CRUD
- ingest log visibility

### Data MVP
- seeded sample data
- public match data support
- player and team stats support
- source attribution labels
- verification status support

---

## Build order

### Milestone 1
Infrastructure foundation:
- Proxmox
- Ubuntu VM
- Docker
- reverse proxy
- HTTPS

### Milestone 2
App and database setup:
- Next.js
- PostgreSQL
- Prisma
- initial schema
- seed data

### Milestone 3
Public MVP pages:
- homepage
- matches
- teams
- players
- articles
- about

### Milestone 4
Admin tooling:
- auth
- dashboard
- CRUD flows

### Milestone 5
Ingest foundation:
- worker
- raw document storage
- ingest tracking

### Milestone 6
Fandom pipeline:
- fetch
- parse
- normalize
- publish

### Milestone 7
Stats pages:
- player leaderboard
- team leaderboard
- enhanced player/team pages

### Milestone 8
Breaking Point integration

### Milestone 9
Predictions and editorial expansion

### Milestone 10
Head-to-head tools

### Milestone 11
Reliability and operations

### Milestone 12
Scrim support

---

## Notes

HardBlock should launch with a focused, polished foundation rather than trying to solve every data problem on day one.

The strongest first version is:
- fast
- trustworthy
- clearly labeled
- easy to update
- useful for both stats browsing and matchup analysis

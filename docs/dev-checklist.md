# HardBlock Development Checklist

This document turns the technical blueprint into an execution checklist with concrete build tasks in order.

---

## Phase 0 - Project definition

### Product and branding
- [x] Choose project name
- [ ] Confirm domain name
- [ ] Finalize site tagline
- [ ] Finalize homepage hero copy
- [ ] Define source label wording for public display

### Scope definition
- [ ] Confirm V1 feature scope
- [ ] Confirm V1 pages
- [ ] Confirm which Phase 2 features are delayed until after launch
- [ ] Decide whether scrims are admin-only at first or public later

### Public pages in V1
- [ ] Homepage
- [ ] Matches page
- [ ] Match detail page
- [ ] Teams page
- [ ] Team detail page
- [ ] Players page
- [ ] Player detail page
- [ ] Articles page
- [ ] Article detail page
- [ ] About page

### Admin pages in V1
- [ ] Admin dashboard
- [ ] Admin teams
- [ ] Admin players
- [ ] Admin matches
- [ ] Admin articles
- [ ] Admin sources
- [ ] Admin ingest

---

## Phase 1 - Infrastructure foundation

### Host machine prep
- [ ] Confirm spare PC is stable
- [ ] Update BIOS if needed
- [ ] Enable virtualization in BIOS
- [ ] Confirm NVMe health
- [ ] Confirm wired ethernet connection
- [ ] Confirm machine will be dedicated to hosting

### Proxmox setup
- [ ] Download Proxmox ISO
- [ ] Create bootable USB installer
- [ ] Install Proxmox on spare PC
- [ ] Configure hostname
- [ ] Configure network
- [ ] Apply Proxmox updates
- [ ] Confirm web UI access

### Production VM setup
- [ ] Create Ubuntu Server production VM
- [ ] Assign CPU, RAM, and disk
- [ ] Install Ubuntu Server
- [ ] Configure VM networking
- [ ] Confirm SSH access
- [ ] Create non-root admin user

### VM hardening
- [ ] Add SSH key authentication
- [ ] Disable password-based SSH login
- [ ] Disable root SSH login
- [ ] Install UFW
- [ ] Open only required ports
- [ ] Install fail2ban
- [ ] Update all system packages

### Public access setup
- [ ] Buy or connect domain
- [ ] Configure DNS
- [ ] Add Cloudflare if using it
- [ ] Configure dynamic DNS if needed
- [ ] Configure router port forwarding
- [ ] Verify public access to server

### Deployment base
- [ ] Install Docker
- [ ] Install Docker Compose plugin
- [ ] Install Git
- [ ] Create project directory on server
- [ ] Set up reverse proxy
- [ ] Configure HTTPS
- [ ] Verify public HTTPS test page

---

## Phase 2 - Repository and app scaffold

### Repository setup
- [ ] Create GitHub repo structure
- [x] Add README.md
- [x] Add docs/blueprint.md
- [ ] Add docs/dev-checklist.md
- [ ] Add .gitignore
- [ ] Add branch strategy
- [ ] Enable Issues
- [ ] Create labels
- [ ] Create milestones
- [ ] Create GitHub Project board

### Next.js app initialization
- [ ] Initialize Next.js app
- [ ] Enable TypeScript
- [ ] Install Tailwind CSS
- [ ] Configure app router
- [ ] Create base layout
- [ ] Create shared navigation
- [ ] Add global styles
- [ ] Add dark theme base styling

### Developer tooling
- [ ] Install ESLint
- [ ] Install Prettier
- [ ] Create environment variable template
- [ ] Create utility folder structure
- [ ] Create shared component folder structure

---

## Phase 3 - Database and ORM

### Database setup
- [ ] Add PostgreSQL to Docker Compose
- [ ] Create persistent DB volume
- [ ] Configure DB credentials
- [ ] Verify application DB connection

### Prisma setup
- [ ] Install Prisma
- [ ] Initialize Prisma config
- [ ] Configure DB connection string
- [ ] Generate Prisma client

### Initial schema
- [ ] Create teams model
- [ ] Create players model
- [ ] Create team_rosters model
- [ ] Create events model
- [ ] Create matches model
- [ ] Create match_maps model
- [ ] Create player_match_stats model
- [ ] Create team_match_stats model
- [ ] Create articles model
- [ ] Create predictions model
- [ ] Create sources model
- [ ] Create raw_documents model
- [ ] Create ingest_runs model

### Schema details
- [ ] Add enums for match status
- [ ] Add enums for source type
- [ ] Add enums for verification status
- [ ] Add enums for article status
- [ ] Add enums for article category
- [ ] Add enums for match type

### Migration and seed
- [ ] Create initial migration
- [ ] Apply migration
- [ ] Create seed script
- [ ] Seed sample teams
- [ ] Seed sample players
- [ ] Seed sample matches
- [ ] Seed sample articles
- [ ] Verify seeded data in database

---

## Phase 4 - Admin authentication

### Auth setup
- [ ] Choose admin auth approach
- [ ] Create login page
- [ ] Protect /admin routes
- [ ] Add session handling
- [ ] Add logout flow
- [ ] Verify unauthorized users are blocked

### Admin identity
- [ ] Create first admin account path
- [ ] Store credentials or secrets securely
- [ ] Document admin login process

---

## Phase 5 - Shared UI foundation

### Shared layout components
- [ ] Build header
- [ ] Build desktop nav
- [ ] Build mobile nav
- [ ] Build footer
- [ ] Build page container component

### Shared content components
- [ ] Build team chip component
- [ ] Build player row component
- [ ] Build match card component
- [ ] Build result card component
- [ ] Build stat card component
- [ ] Build article card component
- [ ] Build source badge component
- [ ] Build verification badge component
- [ ] Build empty state component
- [ ] Build loading state component

### Editorial components
- [ ] Build featured article block
- [ ] Build prediction card
- [ ] Build matchup spotlight block
- [ ] Build "my take" section block

---

## Phase 6 - Public MVP pages

### Homepage
- [ ] Create homepage route
- [ ] Add hero section
- [ ] Add tagline and support copy
- [ ] Add upcoming matches section
- [ ] Add recent results section
- [ ] Add featured article section
- [ ] Add trending section
- [ ] Add latest content section

### Matches
- [ ] Create matches page
- [ ] Show upcoming matches
- [ ] Show completed matches
- [ ] Add basic filters
- [ ] Link to match detail pages

### Match detail
- [ ] Create match detail route
- [ ] Build match header
- [ ] Show event, date, and status
- [ ] Show scoreline
- [ ] Add map breakdown section
- [ ] Add player stats section placeholder
- [ ] Add team comparison snapshot
- [ ] Add source labels
- [ ] Add editorial block placeholder

### Teams
- [ ] Create teams page
- [ ] Show all teams
- [ ] Add team cards or rows
- [ ] Link to team detail pages

### Team detail
- [ ] Create team detail route
- [ ] Add team header
- [ ] Add roster section
- [ ] Add recent matches section
- [ ] Add upcoming matches section
- [ ] Add team stat summary
- [ ] Add related articles block

### Players
- [ ] Create players page
- [ ] Show searchable player list
- [ ] Display team and summary info
- [ ] Link to player detail pages

### Player detail
- [ ] Create player detail route
- [ ] Add player header
- [ ] Add season overview section
- [ ] Add recent match log
- [ ] Add mode splits placeholder
- [ ] Add editorial notes block

### Articles
- [ ] Create articles page
- [ ] Show published articles
- [ ] Add article cards or list
- [ ] Create article detail route
- [ ] Render article body
- [ ] Add related content block

### About
- [ ] Create about page
- [ ] Explain project purpose
- [ ] Explain source trust model
- [ ] Explain official vs third-party vs scrim
- [ ] Add attribution summary

---

## Phase 7 - Admin CRUD

### Admin dashboard
- [ ] Create admin dashboard route
- [ ] Show teams count
- [ ] Show players count
- [ ] Show matches count
- [ ] Show articles count
- [ ] Show recent ingest runs
- [ ] Show parser failure placeholder
- [ ] Show matches missing predictions

### Teams admin
- [ ] Create admin teams list page
- [ ] Create add team form
- [ ] Create edit team form
- [ ] Add logo URL field
- [ ] Add slug handling
- [ ] Add active toggle

### Players admin
- [ ] Create admin players list page
- [ ] Create add player form
- [ ] Create edit player form
- [ ] Add team assignment
- [ ] Add optional role field
- [ ] Add optional country field

### Rosters admin
- [ ] Create roster assignment workflow
- [ ] Add player-team relationship controls
- [ ] Add start and end dates
- [ ] Add active roster flag

### Matches admin
- [ ] Create admin matches list page
- [ ] Create add match form
- [ ] Create edit match form
- [ ] Add team selectors
- [ ] Add event selector
- [ ] Add schedule fields
- [ ] Add status field
- [ ] Add score fields
- [ ] Add map entry workflow
- [ ] Add source selector
- [ ] Add verification status selector

### Articles admin
- [ ] Create admin articles list page
- [ ] Create article add form
- [ ] Create article edit form
- [ ] Add title, excerpt, and body fields
- [ ] Add category field
- [ ] Add draft/published status
- [ ] Add related team selector
- [ ] Add related match selector

### Predictions admin
- [ ] Create admin predictions page
- [ ] Add prediction creation form
- [ ] Link prediction to match
- [ ] Add predicted winner
- [ ] Add predicted score
- [ ] Add confidence field
- [ ] Add analysis summary

### Sources admin
- [ ] Create admin sources list page
- [ ] Create add source form
- [ ] Create edit source form
- [ ] Add source type field
- [ ] Add URL field
- [ ] Add attribution text
- [ ] Add trust level field
- [ ] Add license notes field

---

## Phase 8 - Worker and ingest foundation

### Worker setup
- [ ] Create worker service
- [ ] Create scripts folder
- [ ] Create worker logging utility
- [ ] Add DB access to worker
- [ ] Add manual run command
- [ ] Add scheduled run structure

### Raw fetch pipeline
- [ ] Create raw fetch utility
- [ ] Save source URL
- [ ] Save fetch timestamp
- [ ] Save response status
- [ ] Save raw content
- [ ] Save checksum or hash
- [ ] Add retry logic
- [ ] Add basic rate limiting

### Ingest tracking
- [ ] Create ingest run start record
- [ ] Track run status
- [ ] Track items fetched
- [ ] Track items parsed
- [ ] Track items failed
- [ ] Save completion time
- [ ] Show run history in admin

---

## Phase 9 - Fandom ingestion

### Source setup
- [ ] Add Fandom source record
- [ ] Create config for target page
- [ ] Create Fandom fetch script
- [ ] Save raw page successfully

### Parsing
- [ ] Inspect Fandom page structure
- [ ] Parse player names
- [ ] Parse team names
- [ ] Parse stat columns
- [ ] Parse mode splits if present
- [ ] Parse match-level rows if present
- [ ] Log parser failures

### Normalization
- [ ] Create team alias mapping
- [ ] Create player alias mapping
- [ ] Normalize mode values
- [ ] Detect duplicates
- [ ] Log unmatched entities
- [ ] Create admin review path later if needed

### Publish
- [ ] Write normalized data to canonical stat tables
- [ ] Attach source IDs
- [ ] Attach verification status
- [ ] Attach external references if available
- [ ] Verify data appears on public pages

---

## Phase 10 - Stats pages

### Stats landing
- [ ] Create /stats page
- [ ] Add player stats entry block
- [ ] Add team stats entry block
- [ ] Add quick leaders section

### Player leaderboard
- [ ] Create /stats/players page
- [ ] Add sortable table
- [ ] Add search
- [ ] Add team filter
- [ ] Add mode filter
- [ ] Add minimum threshold
- [ ] Add source labels

### Team leaderboard
- [ ] Create /stats/teams page
- [ ] Add sortable table
- [ ] Add record and win percentage fields
- [ ] Add recent form metric
- [ ] Add source labels

### Player page enhancement
- [ ] Replace placeholders with real stat aggregates
- [ ] Add recent trend section
- [ ] Add best performance block
- [ ] Add mode comparison cards

### Team page enhancement
- [ ] Add real team stat summaries
- [ ] Add recent form calculations
- [ ] Add map pool summaries
- [ ] Add enhanced match summary sections

---

## Phase 11 - Breaking Point ingestion

### Source setup
- [ ] Add Breaking Point source record
- [ ] Create config for target pages
- [ ] Create raw fetch script
- [ ] Save raw source pages

### Parsing
- [ ] Parse team pages
- [ ] Parse player pages
- [ ] Parse stat sections
- [ ] Log parser assumptions
- [ ] Log parser failures

### Source conflict rules
- [ ] Define source precedence rules
- [ ] Define merge policy
- [ ] Log conflicting values
- [ ] Create conflict review path
- [ ] Prevent silent overwrite of canonical data

### Publish
- [ ] Publish approved Breaking Point data
- [ ] Attach source labels
- [ ] Verify public attribution display

---

## Phase 12 - Editorial and predictions

### Predictions
- [ ] Create public predictions page
- [ ] Display matchup, winner, score, and confidence
- [ ] Link predictions to match pages

### Match page editorial
- [ ] Add pre-match preview block
- [ ] Add post-match recap block
- [ ] Link related articles
- [ ] Add support for "my take" notes

### Homepage editorial
- [ ] Add featured prediction block
- [ ] Add editorial spotlight section
- [ ] Add featured matchup analysis block

---

## Phase 13 - Head-to-head

### H2H landing
- [ ] Create head-to-head landing page
- [ ] Add team selector
- [ ] Add featured rivalry links
- [ ] Add dynamic route generation

### H2H detail page
- [ ] Create head-to-head detail route
- [ ] Show overall record
- [ ] Show last five meetings
- [ ] Show team form comparison
- [ ] Show mode comparison
- [ ] Show key player comparison
- [ ] Add editorial analysis block

---

## Phase 14 - Reliability and operations

### Backups
- [ ] Create PostgreSQL backup script
- [ ] Schedule nightly DB backups
- [ ] Verify backup location
- [ ] Test restore procedure
- [ ] Add Proxmox snapshot schedule
- [ ] Define backup retention policy

### Monitoring
- [ ] Add uptime monitoring
- [ ] Add application error logging
- [ ] Add worker log rotation
- [ ] Add ingest failure alerts
- [ ] Add repeated parser failure alerts

### Security and hardening
- [ ] Review exposed ports
- [ ] Verify admin routes are protected
- [ ] Verify secrets are not committed
- [ ] Add rate limiting if needed
- [ ] Add secure headers in proxy or app

---

## Phase 15 - Scrim support later

### Scrim schema
- [ ] Create scrim_blocks model
- [ ] Create scrim_maps model
- [ ] Create scrim_team_stats model
- [ ] Create scrim_player_stats model
- [ ] Create scrim_sources model

### Scrim workflow
- [ ] Create admin scrim form
- [ ] Add team selectors
- [ ] Add map result entry
- [ ] Add source field
- [ ] Add confidence field
- [ ] Add private/public visibility toggle
- [ ] Add notes field

### Public scrim display rules
- [ ] Keep scrim data separate from official data
- [ ] Add distinct public scrim labeling
- [ ] Prevent scrim data from polluting official aggregates

---

## Immediate next steps

### First execution sprint
- [x ] Rename `docs/bluprint.md` to `docs/blueprint.md`
- [ x] Add this `docs/dev-checklist.md` file
- [ ] Confirm README is updated
- [ ] Create GitHub labels
- [ ] Create GitHub milestones
- [ ] Create GitHub Project board
- [ ] Install Proxmox
- [ ] Create Ubuntu production VM
- [ ] Install Docker and Compose
- [ ] Initialize Next.js app
- [ ] Add PostgreSQL and Prisma
- [ ] Create initial schema
- [ ] Seed sample data

### First public-facing build sprint
- [ ] Build shared layout
- [ ] Build homepage
- [ ] Build matches page
- [ ] Build team pages
- [ ] Add admin auth
- [ ] Add admin teams and matches CRUD

# Implementation Plan: Commander Deck Themer

**Branch**: `001-deck-theme-generator` | **Date**: 2026-02-08 | **Spec**: `/Users/szymon/Documents/deck/specs/001-deck-theme-generator/spec.md`
**Input**: Feature specification from `/specs/001-deck-theme-generator/spec.md`

## Summary

Build a Rails web app that lets users submit a Commander decklist and theme, generates themed card data and alternate images, and presents a public deck page with a grid view and download access.

## Technical Context

**Language/Version**: Ruby 4.0.1, Rails 8.1.2  
**Primary Dependencies**: Rails, ActiveRecord, ActiveStorage, tailwindcss-rails 4.4.0, MiniMagick 5.3.1, Faraday 2.14.1  
**Storage**: SQLite  
**Testing**: RSpec, Capybara  
**Target Platform**: Web (Rails server)  
**Project Type**: Web application  
**Performance Goals**: A 100-card deck processes to themed list and grid view in under 2 minutes (SC-002)  
**Constraints**: Public URLs without authentication; support plain-text decklist uploads; respect theming rules in FR-012 to FR-019  
**Scale/Scope**: Single-deck processing per request; modest traffic (hundreds of decks/day)

## Constitution Check

The constitution file contains placeholders only, so no enforceable gates are defined. Proceeding with standard quality checks.

## Project Structure

### Documentation (this feature)

```text
specs/001-deck-theme-generator/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
└── tasks.md
```

### Source Code (repository root)

```text
# Web application
app/
├── controllers/
├── models/
├── services/
├── views/
├── jobs/
└── assets/

config/

test/ or spec/
```

**Structure Decision**: Rails web application using standard `app/` layout with service objects for deck parsing, theming, and image generation.

## Phase 0: Outline & Research

### Research Tasks

- Best practices for Rails image composition with card frames and overlays.
- Scryfall API usage patterns and rate limits for bulk card lookups.
- Storage strategy for generated images in Rails with ActiveStorage.

### Research Output

See `research.md`.

## Phase 1: Design & Contracts

### Data Model

See `data-model.md`.

### API Contracts

See `/contracts/openapi.yaml`.

### Quickstart

See `quickstart.md`.

### Agent Context Update

Run `.specify/scripts/bash/update-agent-context.sh codex` and preserve any manual additions.

## Phase 2: Plan (generated later)

`tasks.md` will be created by `/speckit.tasks`.

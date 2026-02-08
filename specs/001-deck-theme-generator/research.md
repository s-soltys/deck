# Research: Commander Deck Themer

## Decision: Rails + Ruby for web app (Ruby 4.0.1, Rails 8.1.2)

**Rationale**: Aligns with the requested stack and provides full-stack web capabilities with conventions for MVC, jobs, and asset pipelines.
**Alternatives considered**: Node.js (Express/Next), Python (Django).

## Decision: SQLite for persistence

**Rationale**: Lightweight storage for MVP, simple local development, sufficient for modest traffic.
**Alternatives considered**: PostgreSQL, MySQL.

## Decision: tailwindcss-rails for styling (4.4.0)

**Rationale**: Requested stack, quick iteration on UI with utility classes and component composition.
**Alternatives considered**: Bootstrap, custom SCSS.

## Decision: Scryfall API for card data

**Rationale**: Public, well-known MTG card data source with images and rich metadata.
**Alternatives considered**: MTGJSON, Gatherer scraping.

## Decision: MiniMagick for card image compositing (5.3.1)

**Rationale**: Mature Ruby image processing library suitable for overlaying themed art and text on existing card frames.
**Alternatives considered**: RMagick, external image service.

## Decision: ActiveStorage for generated images (Rails 8.1.2)

**Rationale**: Built-in Rails abstraction for storing and serving generated assets without custom storage logic.
**Alternatives considered**: Local file storage without ActiveStorage, third-party storage SDKs.

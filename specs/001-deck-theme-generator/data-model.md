# Data Model: Commander Deck Themer

## Deck

- **id**: UUID
- **public_slug**: short, unique identifier for public URLs
- **title**: optional user-facing name
- **decklist_text**: raw input text
- **status**: enum (submitted, parsed, themed, imaged, failed)
- **error_summary**: optional
- **created_at / updated_at**

## Theme

- **id**: UUID
- **deck_id**: belongs to Deck
- **description**: theme description text
- **commander_name**: themed commander name

## Card

- **id**: UUID
- **oracle_name**: canonical name
- **scryfall_id**: external reference
- **type_line**: card types
- **color_identity**: list of colors
- **is_legendary**: boolean
- **is_basic_land**: boolean
- **is_planeswalker**: boolean
- **primary_image_url**: selected printing image

## DeckCard

- **id**: UUID
- **deck_id**: belongs to Deck
- **card_id**: belongs to Card
- **quantity**: integer
- **parse_status**: enum (ok, missing, invalid)
- **notes**: optional parsing errors

## ThemedCard

- **id**: UUID
- **deck_card_id**: belongs to DeckCard
- **themed_name**: generated name (subject to FR-012, FR-013)
- **art_description**: generated description
- **role_alignment**: text tag for role/character alignment

## GeneratedImage

- **id**: UUID
- **themed_card_id**: belongs to ThemedCard
- **image_blob**: ActiveStorage attachment
- **status**: enum (pending, generated, failed)
- **error_summary**: optional

## Relationships

- Deck has one Theme
- Deck has many DeckCards
- DeckCard belongs to Card and has one ThemedCard
- ThemedCard has one GeneratedImage

## Validation Rules

- Decklist must be non-empty and parseable into at least 1 card
- Commander decklists expected to total 100 cards (including commander)
- Themed name respects legendary and basic land rules
- Themed role alignment respects defensive/aggressive mapping constraints
- Color identity and type framing constraints enforced for themed outputs

## State Transitions

- submitted → parsed → themed → imaged
- Any state can transition to failed with error_summary

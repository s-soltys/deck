# Feature Specification: Commander Deck Themer

**Feature Branch**: `001-deck-theme-generator`  
**Created**: 2026-02-08  
**Status**: Draft  
**Input**: User description: "this is an app which allows me to theme a magic the gathering commander deck. the user flow is: I upload a decklist, and provide a theme - I describe the theme (e.g. universe, a fantasy world, a movie etc.) and tell who is the commander from this world. Then based on this the app loads card info from a well known API (images, card name, stats etc.) and for each card the app defines: the themed name, a description of the alternative themed image. Then based on this, the app generates a visual grid decklist (similar to apps like moxfield) and for each card it generates an alternative card image (by taking the original card and just pasting the newly generated image of the themed card over the area where the original card has its image and also by replacing the card name with the themed name). There is no authentication in the first version."

## Clarifications

### Session 2026-02-08

- Q: Which decklist input format should be supported for upload? → A: Plain text list with one card per line and optional quantity.
- Q: Which card printing should be used when multiple images exist? → A: Most recent regular printing.
- Q: Are there theme content restrictions? → A: Any theme allowed; user is responsible for rights.
- Q: Should results be persisted for later access? → A: Persistent saved deck with public URL.
- Q: How should missing card data be handled? → A: Continue and mark missing cards.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Generate themed card list (Priority: P1)

A player uploads a Commander decklist, describes a theme, and provides the themed commander name so they can get a complete themed card list with a themed name and themed art description for every card.

**Why this priority**: It delivers the core value even without visual output and confirms the deck can be themed end-to-end.

**Independent Test**: Can be fully tested by submitting a 100-card decklist and a theme and verifying each card has a themed name and art description.

**Acceptance Scenarios**:

1. **Given** a valid Commander decklist and a theme description, **When** the user submits them, **Then** every card returns with its original data plus a themed name and themed art description.
2. **Given** a decklist containing unknown or misspelled cards, **When** the user submits it, **Then** the system reports the unknown entries and continues processing known cards.

---

### User Story 2 - View themed deck grid (Priority: P2)

A player views the themed deck as a visual grid so they can scan the deck similarly to common decklist tools.

**Why this priority**: It turns the themed data into an immediately usable deck browsing experience.

**Independent Test**: Can be fully tested by generating a themed list and confirming the grid shows all cards with names and images.

**Acceptance Scenarios**:

1. **Given** a completed themed card list, **When** the user opens the deck view, **Then** the system displays a grid of all cards with images and names.

---

### User Story 3 - Generate alternate card images (Priority: P3)

A player generates alternate card images so each card shows the themed art and themed name on the card frame.

**Why this priority**: It provides the final, shareable visual output for the themed deck.

**Independent Test**: Can be fully tested by generating alternate images for at least one card and verifying the themed art and name appear on the card.

**Acceptance Scenarios**:

1. **Given** a completed themed card list, **When** the user requests alternate images, **Then** each card produces an alternate image that replaces the card art area and card name with the themed versions.

---

### Edge Cases

- What happens when the decklist is empty or does not meet Commander deck size rules?
- How does the system handle multiple copies of a card in the decklist?
- What happens when a card has multiple printings with different images?
- How does the system handle theme descriptions that are extremely short or empty?
- What happens when the card data source has missing image or stats data?
- How does the system handle long-running generation for large decks?
- What happens when a decklist line is malformed or missing a card name?
- What happens when a card’s “legendary” status is unclear or missing in card data?
- What happens when the selected printing lacks an image?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow users to submit a Commander decklist without creating an account.
- **FR-002**: System MUST allow users to provide a theme description and a themed commander name alongside the decklist.
- **FR-003**: System MUST accept plain text decklists with one card per line and optional quantities and parse them into a normalized list of cards and counts.
- **FR-004**: System MUST retrieve card names, images, and basic stats from a public card data source for each card in the decklist.
- **FR-004a**: System MUST select the most recent regular printing when multiple images exist for a card.
- **FR-005**: System MUST generate a themed name and a themed art description for every card in the decklist.
- **FR-006**: System MUST display a visual grid decklist that includes card images and names.
- **FR-007**: System MUST generate an alternate card image that replaces the card art area and card name with the themed versions.
- **FR-008**: System MUST surface clear error messages for cards that cannot be resolved and continue processing remaining cards.
- **FR-009**: System MUST allow any theme content and display a notice that users are responsible for usage rights.
- **FR-010**: System MUST persist generated decks and provide a public URL for later access without authentication.
- **FR-011**: System MUST mark any unresolved cards in the results rather than failing the entire run.
- **FR-012**: System MUST preserve legendary status in themed names (legendary cards become named characters, and non-legendary cards do not become named characters).
- **FR-013**: System MUST keep the names of basic lands unchanged in the themed output.
- **FR-014**: System MUST align themed versions with the source card’s character or role (for example, defensive cards map to defensive-themed counterparts).
- **FR-015**: System MUST keep themed naming and imagery aligned with the card’s color identity.
- **FR-016**: System MUST preserve card type framing in the theme (creatures remain creatures, spells remain spell effects, and artifacts remain objects).
- **FR-017**: System MUST preserve core creature type identity where it materially defines the card (for example, Dragons remain large mythic creatures).
- **FR-018**: System MUST treat planeswalkers as singular named characters in the theme.
- **FR-019**: System MUST keep equipment, auras, and vehicles framed as items, effects, and conveyances respectively, not characters.

### Key Entities *(include if feature involves data)*

- **Decklist**: User-submitted list of card names and quantities, plus format metadata.
- **Theme**: User-provided theme description and themed commander name.
- **Card**: Canonical card data including name, image, and basic stats.
- **Themed Card**: Card plus themed name and themed art description.
- **Alternate Image**: Visual output that applies themed art and name to the card frame.

### Assumptions

- Commander decklists are expected to contain 100 cards including the commander.
- Users provide decklists as plain text with one card per line and optional quantities.
- The first version focuses on single-deck processing, not bulk imports or multi-deck management by the same user.

### Dependencies

- Access to a public card data source that provides card images and basic stats.
- Ability to produce themed art assets from the provided theme description.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 90% of submitted Commander decklists result in a complete themed list with fewer than 5 unresolved cards.
- **SC-002**: 90% of users can complete a themed deck submission and view the themed list within 2 minutes.
- **SC-003**: For 90% of runs, a 100-card deck produces alternate images for at least 95 cards.
- **SC-004**: 80% of first-time users report they can understand the theme inputs and results without external help.

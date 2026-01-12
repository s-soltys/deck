---
description: Theme a MTG Commander deck and emit themed_deck.json
---

Given a Commander decklist ($DECKLIST as text or file path), a theme ($THEME), and optional commander override ($COMMANDER), produce themed_deck.json with this exact structure:
If $DECKLIST or $THEME are not provided, prompt the user for the missing values. Only generate the file when all required datapoints are provided.
{
  "deck_name": "...",
  "deck_prompt": "...",
  "cards": [
    {
      "name": "official MTG card name (Scryfall/Gatherer)",
      "themed_name": "theme-adapted name",
      "image_prompt": "card-specific prompt (complements deck_prompt)",
      "quantity": number
    }
  ]
}

Rules:
- Use the theme for naming/imagery; keep card identity recognizable.
- Keep prompts concise but vivid; avoid lore dumps.
- Preserve quantities from input (basics may have qty >1; most others =1).
- If the decklist marks a commander (e.g., #!Commander) or $COMMANDER is set, theme that face card and reflect it in deck_name/deck_prompt.
- Do not invent cards not in the list. Use official names for "name".
- Output valid JSON only, no trailing commas or extra text.
- Legendary creatures must always be named characters from the theme.
- Character assignments should be proportional to strength: major theme characters should be represented by strong/powerful cards in the deck, but theme appropriateness takes priority.
- Theme comes first in naming; reference original card names in themed names when necessary, but not at all costs—theme coherence is paramount.
- Always verify card names against Scryfall API (https://api.scryfall.com/cards/named?exact={name} or search endpoint) to ensure official MTG card names are used. Follow MTG naming principles (see References) when verifying names.
- When creating themed_name and image_prompt, first fetch card details from Scryfall API (including type, abilities, flavor text, power/toughness, mana cost) to inform the theming process. Reference MTG naming principles for consistency in themed naming.

Steps:
1) Validate inputs: if $DECKLIST is missing, prompt "Please provide the decklist (text or file path):" and wait for input. If $THEME is missing, prompt "Please provide the theme:" and wait for input. Only proceed when both are provided.
2) If $DECKLIST is a path, read it; otherwise treat it as the raw list.
3) Parse cards and quantities; capture commander(s) and identify all legendary creatures.
4) For each card, query Scryfall API to get official card name and details:
   - Use exact name search: https://api.scryfall.com/cards/named?exact={name} or fuzzy search if needed
   - Extract: official name, type, abilities, flavor text, power/toughness, mana cost, oracle text
   - Normalize card names to official Scryfall names for the "name" field
   - Follow MTG naming principles (see References below) when verifying and using card names
5) Craft deck_name and a concise deck_prompt encoding theme + art direction.
6) For each card: using the fetched card details, set name (official from API), themed_name, image_prompt, quantity. For legendary creatures, assign named theme characters (matching strength proportionally when possible, but prioritizing theme fit). Use card details (abilities, type, flavor) to inform themed naming and descriptions. When creating themed names, reference MTG naming principles for consistency.
7) Return only the JSON object above.

References - MTG Card Naming Principles:
- Magic: The Gathering Comprehensive Rules, Section 201 (Card Names): https://media.wizards.com/2024/downloads/MagicCompRules%2004102024.pdf
  - Rule 201.1: Card name is printed on upper left corner
  - Rule 201.2: Card's name is always considered the English version, regardless of printed language
- "By Any Other Name" by Mark Rosewater: https://magic.wizards.com/en/news/making-magic/any-other-name-2005-04-25
  - Discusses creative naming techniques, functional descriptiveness, and thematic coherence
- Scryfall API Documentation: https://scryfall.com/docs/api

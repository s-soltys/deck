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

Steps:
1) Validate inputs: if $DECKLIST is missing, prompt "Please provide the decklist (text or file path):" and wait for input. If $THEME is missing, prompt "Please provide the theme:" and wait for input. Only proceed when both are provided.
2) If $DECKLIST is a path, read it; otherwise treat it as the raw list.
3) Parse cards and quantities; capture commander(s) and identify all legendary creatures.
4) Craft deck_name and a concise deck_prompt encoding theme + art direction.
5) For each card: set name, themed_name, image_prompt, quantity. For legendary creatures, assign named theme characters (matching strength proportionally when possible, but prioritizing theme fit).
6) Return only the JSON object above.

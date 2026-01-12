---
description: Theme a MTG Commander deck and emit themed_deck.json
argument-hint: DECKLIST="<path|raw list>" THEME="<theme/skin details>" [COMMANDER="<name>"]
---

Given a Commander decklist ($DECKLIST as text or file path), a theme ($THEME), and optional commander override ($COMMANDER), produce themed_deck.json with this exact structure:
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

Steps:
1) If $DECKLIST is a path, read it; otherwise treat it as the raw list.
2) Parse cards and quantities; capture commander(s).
3) Craft deck_name and a concise deck_prompt encoding theme + art direction.
4) For each card: set name, themed_name, image_prompt, quantity.
5) Return only the JSON object above.

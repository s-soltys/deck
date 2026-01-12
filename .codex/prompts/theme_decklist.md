---
description: Create a themed decklist JSON from a provided decklist
argument-hint: [DECKLIST=<file|pasted>]
---

Ask the user to provide a decklist reference, either a file path or pasted decklist text.
Once a decklist reference is provided, give 2-3 short suggestions for possible themes.
Ask the user to choose a theme (flavour or Universes Beyond).
After the user provides a theme, create a JSON file in this exact format:

{
  "theme": "Theme of the deck",
  "general_prompt": "Prompt to be injected for each individual card prompt",
  "cards": [
    {
      "name": "official_card_name",
      "themed_name": "alternative in-theme version of the name",
      "themed_image_description": "a prompt to be given to AI to generate the image of the themed version of the card",
      "quantity": 1
    }
  ]
}

Make sure the JSON aligns with this format.

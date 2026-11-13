# DSE Visual Bible (example)

An example visual bible for a short AI-animated education series: black ink line art on warm paper, vertical 9:16 episodes.

It was built for the *Agentic Business Schooled* animated shorts and is shared as a reference for the episode-building exercise. Use it to see what a visual bible contains, or as a starting library for your own episodes.

## What's inside

- `visual-bible.md` — the global rules: palette, line, modes, cinematography, motion, prompt language, and what is prohibited.
- `style/` — the style plates every generation is anchored to.
- `characters/`, `wardrobe/`, `locations/`, `props/` — one folder per entity, each with a `spec.md` (identity, required marks, forbidden marks) and its approved reference plates.
- `style.json` — the style contract the local episode tools read: paper colour, allowed modes, style-board paths, and the prompt seams. The active bible is selected in `/workspace/local-agents/pipeline.json`.
- Design rule: Cortex (the Evaluator) and any AI agent character added from now on wear solid black ink clothing (and hat, if any) so they stand out from the humans. The existing cast, including ARIA, VERA, LUMEN, SCOUT, ÉLISE, the architect, the copywriter, the designer, and the sage, keep their current wardrobe. This is recorded in `style.json` under `character_rules` and in the prompt preamble.
- `registry.json` — a generated index of every entity and plate. The stills agent reads this.
- `marks.md` — a generated table of which character owns which identity mark, so new characters stay distinct.
- `index.html` — open in a browser to browse every plate.

Start with `visual-bible.md`, then open `index.html`.

## Note on sources

The style was developed from three reference boards that are **not** included here. Every plate in this repo is an original generated image.

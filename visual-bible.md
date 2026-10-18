# Visual Bible v1

Black ink on warm paper. The series reads as a hand-drawn graphic story: open contour, a few solid black shapes, and almost no ornament. Empty paper is the light. One black mass is usually enough shadow.

The language comes from three supplied boards in `sources/style-boards/`. Those boards are style input only. Everything in `characters/`, `wardrobe/`, `locations/`, `props/`, and `style/` is an original plate. Do not reproduce the sunflower vase, the reclining brush face, or the jeweled dancer.

Model used for this library: Nano Banana 2 (`gemini-3.1-flash-image`), square, 1K.

## How the library is organized

Each character, wardrobe look, location, and prop has its own folder. The folder holds a `spec.md` and the approved plates. The spec is the source of truth for that entity's identity, required marks, and forbidden marks. This file only holds the rules that apply to everyone.

```text
visual-bible/
  visual-bible.md      global rules (this file)
  registry.json        generated index of every entity and plate
  marks.md             generated table of who owns which identity mark
  index.html           generated page for browsing every plate
  characters/<id>/     spec.md, front.png (anchor), other angles
  wardrobe/<id>/       spec.md, look.png (anchor)
  locations/<id>/      spec.md, establishing.png (anchor)
  props/<id>/          spec.md, insert.png (anchor)
  style/               the six style plates and their spec
  _drafts/<id>/        work in progress, never referenced by an episode
```

`registry.json`, `marks.md`, and `index.html` are built by `python3 scripts/library.py registry`. Do not edit them by hand. Open `index.html` to review the plates.

## Illustration rules

- Black ink only, on a warm off-white ground. No color.
- Two line weights may share a picture: a hairline contour and a heavy brush stroke.
- Solid black is reserved for hair, deepest shadow, pupils, screens, doorways, night sky, and graphic accents.
- Everything else stays the paper color. No gray washes, gradients, or halftone.
- Hatching is sparse, and only where a form needs shadow.
- Ornament is rare. A spiral, curl, or dot appears only when that entity's spec requires it. Do not scatter extras in the empty paper.
- Backgrounds stay sparse. If a wall has nothing to say, leave it blank.
- No text, captions, signatures, borders, or frames.

Three modes, used on purpose:

| Mode | Use | Plate |
| --- | --- | --- |
| Brush | Emotion, extreme close-up | `style/brush-portrait.png` |
| Contour | Objects, rooms, clothing folds | `style/still-life.png` |
| Silhouette | Walking, distance, graphic punches | `style/silhouette.png` |

## Cast

The lead is Samantha in the episodes. The elder is held in reserve. The six agents are separate people and must not borrow the lead's hair, earring, pendant, or vest. Full marks for each are in that character's `spec.md`, and the side-by-side view is in `marks.md`.

| Id | Who | Plates |
| --- | --- | --- |
| `lead` | The lead | front, three-quarter, profile, full-body, sitting, expressions |
| `elder` | The elder | front, profile |
| `aria` | ARIA, platform | front |
| `vera` | VERA, interview | front |
| `lumen` | LUMEN, campaign | front |
| `scout` | SCOUT, current events | front |
| `elise` | ÉLISE, styling | front |
| `sage` | SAGE, nerves | front |

The lead has bare cheeks. Never add a spiral, birthmark, or tattoo to her face.

Four general people have no story name. An episode may give one of them a role. They stay distinct from the cast above, and from each other. A crowd, a judge panel, or passersby are still unmarked figures with no plates.

| Id | Who | Plates |
| --- | --- | --- |
| `man-tie` | A man in his forties | front |
| `woman-shawl` | A woman in her fifties | front |
| `man-cowlick` | A young man | front |
| `woman-braid` | A young woman | front |

## Wardrobe

`lead-everyday` is her default. `lead-coat` is for exteriors. `lead-stage` is the gown, and it is the same garment as the `gown` prop. `lead-draped` is an option, not a default. Do not add stacked necklaces, armbands, or a dance pose to it.

## Environments

Rooms and streets are line drawings with one black shape. Day is empty paper. Night is a black field with a small pool of paper-white light. No signs, no lettering, no crowds.

Locations: `apartment`, `street`, `cafe`, `train-platform`, `night-street`, `factory`.

## Props

Recurring objects stay simple: `photograph`, `letter`, `phone`, `necklace`, `gown`, `light-socket`, `iron`, `outlet`. The agent is the exception: `agent` is a toolbox with levers and dials around it, and one spiral on the front. Dials are blank. If an object matters to the story, generate from its plate. Do not invent a second design.

## Extending the library

New characters, places, and objects come from episode needs, but they live in the shared library so later episodes can reuse them.

1. `python3 scripts/library.py new character <id> --episode E04` writes `_drafts/<id>/spec.md`. Fill in the identity, the required marks, and the forbidden marks. Use `wardrobe`, `location`, or `prop` instead of `character` for the other kinds.
2. `python3 scripts/library.py anchor <id>` generates three anchor candidates. The prompt is built from the style lock, the spec, the style boards, and two approved plates of the same kind as style anchors.
3. `python3 scripts/library.py pick <id> b` makes the chosen candidate the anchor. The others move to `_drafts/<id>/rejected/`.
4. `python3 scripts/library.py pack <id>` generates the other plates listed in the spec. Each plate is drawn from the anchor.
5. Review every plate against the spec. Redraw one with `pack <id> --plates profile --force`.
6. `python3 scripts/library.py promote <id>` moves the pack into the library and rebuilds the registry.
7. `python3 scripts/library.py check` before any episode render.

To add an angle to an existing entity, run `pack <id> --plates profile`. The plate lands in `_drafts/<id>/`, and `promote <id>` adds it to the library folder.

Rules:

- Each new character needs two or three marks that no one else uses. Check `marks.md` first. Silhouette and hair come first. Ornament comes second. `check` fails if two characters require the same mark.
- Every new character's forbidden marks list the lead's earring, pendant, and vest, plus any mark that would make them read as someone else.
- Background people, such as judges, audiences, or passersby, are not characters. They get no marks and no plates. Describe them in the shot prompt as unmarked figures.
- A location starts with one establishing plate. Add `reverse`, `night`, or `detail` only when a shot needs it.
- Episodes never reference anything in `_drafts/`.
- To stop using an entity, set `status: retired` in its spec. Do not delete the folder while an episode still uses it.

## Cinematography

Reference plates are square. Production frames are 9:16, but they keep the same rules.

- Leave a large field of paper. The subject does not have to fill the frame.
- One foreground black shape is enough: a doorway, a shadow, a column, hair.
- Prefer close-ups and inserts. They match the brush and contour modes and they are easier to animate.
- Profile and silhouette are first-class framings, not exceptions.
- Eye level, or slightly above a seated person. No dramatic lens distortion.

## Motion

Still plates are built for limited animation.

Prefer a blink, a small head turn, a shift in the eyes, hair or cloth moving, a slow walk, an entrance or exit, or a silhouette crossing the frame.

Avoid, in a single shot, complex hand business, two people touching, fights, long walks, or more than one action.

## Prompt language

Every generation starts with the style lock in `scripts/library.py`, then names the subject and attaches the relevant plates. The short form:

```text
Black ink on warm off-white paper. Hairline contours and heavy brush strokes may share the picture. Large flat black only for hair, deepest shadow, pupils, and graphic accents. Everything else stays the paper color. No gray wash, gradient, halftone, or color. Sparse hatching only. A spiral, curl, or dot only when the subject requires that exact mark. No stray spirals. Generous empty paper. No text, border, frame, or signature. Do not copy the sunflower vase, the reclining brush face, or the jeweled dancer.
```

In episode shot prompts, name people and places by id rather than by path:

```json
"entities": [{"id": "lead", "plate": "three-quarter"}, {"id": "apartment"}]
```

The stills agent attaches each plate and appends that entity's required and forbidden marks from the registry. `plate` defaults to the entity's anchor.

## Prohibited

- Color, gray paint, gradients, screentone
- Photorealism, 3D, anime, clean vector, watercolor
- Text, logos, captions, watermarks
- Busy rooms, crowds, signage
- A second design for a locked character, wardrobe, or prop
- Copying the three source boards

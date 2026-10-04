# Dusk Lantern — design notes

Paper lanterns over a koi pond at dusk, haunted by the ghosts of Edo-period
woodblock prints. The desktop is the hour after sunset: the sky has gone
indigo, the lanterns have just been lit, and something is looking back from
the dark.

## Emotional target

**Should feel:** nocturnal, warm-lit, eerie but playful, graphic, story-led —
a ghost story told by lantern light.

**Should not feel:** cute, festival-kitsch, red-and-black sushi bar, synthwave
neon, pastel candy, corporate dark mode, a generic "Japan" theme.

## Visual thesis

- **Ground — the dusk sky.** Indigo with real chroma, not a neutral grey. Every
  surface is a step of the same sky, from raised haze down to nightfall.
- **Light — the lantern.** Amber is the only light source. It leads: focus
  border, accent, the active state. Text is lantern-lit paper, a warm cream on a
  cool ground (a deliberate temperature split).
- **Below — the pond.** Koi vermilion, lotus pink, pond teal, water glint and the
  last blue of the sky sit underneath the lantern and answer it.
- **Characters — the ghosts.** Wallpapers carry one figure each on the flat
  ground, lit by a pool of lantern light. The interface stays quiet so the
  figure can be the character.

## Palette

Three families, named by material. Hexes live in `colors.toml`; these are the
roles they play.

| Material | Hex | Omarchy key(s) | Role |
|---|---|---|---|
| dusk indigo sky | `#1d1c3a` | `background` | Ground; also the exact wallpaper fill |
| deeper dusk | `#13122c` | `dark_background` | Recessed surfaces |
| nightfall | `#0b0a20` | `darker_background` | Deepest surfaces, bar wells |
| raised haze | `#2b2a48` | `lighter_background` | Raised surfaces, title bars |
| twilight violet | `#40356c` | `selection`, `selection_background` | Selection — a patch of later sky, not a light |
| dusk mist | `#9d9ab9` | `muted` | Comments, hints, inactive text |
| lantern-lit paper | `#f0d3a3` | `foreground` | Body text |
| paper in shadow | `#bea784` | `dark_foreground` | Secondary text |
| paper at the flame | `#f9e5c3` | `light_foreground`, `bright_foreground`, `selection_foreground` | Emphasis; Omarchy also derives the cursor from it |
| **lantern amber** | `#ffa024` | `accent`, `orange` | **Lead.** Focus border, active state, prompts |
| flame core lemon | `#e7d355` | `yellow` | Warnings, modified state |
| burnt wick | `#8e5224` | `brown` | Quiet warm structure |
| koi vermilion | `#fd622d` | `red` | Errors, alerts, bar attention state |
| lotus pink | `#ff8ca3` | `magenta` | Keywords, branches |
| pond teal | `#5dbca0` | `green` | Success, strings, executables |
| water glint | `#55baba` | `cyan` | Links, symlinks |
| last-light blue | `#6ec6f7` | `blue` | Info, paths, functions |

Bright variants (`bright_*`) are the same materials nearer the surface or
nearer the flame: lighter and slightly less saturated, never a new hue.

### Deliberate slot remapping

Slot names are consumer schema labels, not colour instructions.

- `red` is the koi, not a generic danger red. Errors are vermilion because the
  koi is the one thing in the scene that is that colour.
- `orange` is the lantern itself and duplicates `accent`.
- `green` and `cyan` are both pond water. They are near-twins on purpose; in
  `ls` output executables and symlinks read as one family. If that ever costs
  real clarity, separate them by lightness rather than adding a new hue.
- `yellow` is the hot core of the flame, not a second accent.
- There is no white anywhere. The brightest value is warm paper.

### Measured

- Text on ground 11.4:1 WCAG, muted 6.1:1, lantern amber 8.1:1, koi vermilion
  5.4:1, selection text 8.8:1.
- Background L 0.245 OKLCH with chroma 0.055 — a tinted ground, not a neutral.
- Accent chroma median 0.14, peak 0.20 (lantern and koi carry the saturation).

## Wallpapers

One figure per image on the exact ground colour `#1d1c3a`, 3840×2160, lit by a
soft radial pool of lantern amber. The figures are public-domain Edo-period
prints, cut out by colour and recoloured with a luminance gradient map that
passes only through palette colours (nightfall → twilight → wick/koi → lantern
→ paper).

| File | Subject | Source |
|---|---|---|
| `01-lantern-ghost.png` | Oiwa, the lantern ghost | Katsushika Hokusai, *Hyaku monogatari* (One Hundred Ghost Tales), c. 1831. Rijksmuseum scan, CC0. |
| `02-skeleton-spectre.png` | The giant skeleton spectre | Utagawa Kuniyoshi, *Takiyasha the Witch and the Skeleton Spectre*, c. 1844. Public domain. The two right-hand panels of the triptych are spliced and the samurai below are faded out. |
| `03-lantern-cat.png` | A cat tangled in a fallen paper lantern | Kobayashi Kiyochika, *Neko to chōchin* (Cat and Lantern), 1877. Public domain. The lightest note in the set: playful rather than eerie. |
| `04-moths.png` | Moths drawn to the light | Kubo Shunman, surimono of moths, Metropolitan Museum of Art (DP139026), CC0. Poem calligraphy removed; moths recoloured in lantern tones. |
| `05-crow.png` | A crow in flight | Kawanabe Kyōsai, *Crow Flying in the Snow*, Metropolitan Museum of Art (DP211822), CC0. The gradient map is inverted so the ink itself glows amber. |

The scans come from Wikimedia Commons. All are public domain or CC0, so they can
be redistributed with the theme.

What makes a wallpaper work here: one large, simple figure that fills the
screen as a single shape, reading mostly as lantern amber on violet. Busy
armour, patterned robes, framing devices (storm swirls, round windows) and
figures cut off by the print edge all weakened earlier candidates. Each
wallpaper should be a different subject: no second version of the same legend.
Figures should carry the lantern colours; a figure left as a dark silhouette
reads as plain dark rather than lit.

Cut-out notes for future additions: the figure must separate from its ground by
colour (warm figure on cool ground works best). A figure whose hair or face
matches the background (Hokusai's Okiku, for example) cannot be cut out cleanly
and should not be forced. Keep to crisp, line-drawn woodblock prints; painted,
soft-focus ghosts break the set's drawing style.

## Surfaces

- **Hyprland:** active border is lantern amber (from `accent`); inactive is the
  raised haze at 60% opacity, so unfocused windows recede into the sky.
- **Shell:** bar, menus and notifications sit on the dusk ground with paper text;
  selected rows use lantern amber; the bar's attention state uses koi vermilion.
- **Terminal / Splinterm:** Splinterm reads the theme's `colors.toml` and
  generated `foot.ini` directly; no separate terminal palette is shipped.
- **Icons:** Yaru Purple, from the twilight family, so amber stays rare.
- **Unlock:** `unlock.png` is the lantern ghost cut out on transparency; Plymouth
  draws it on the dusk ground with paper text. `preview-unlock.png` is a mockup
  of that screen for the switcher.
- **GTK:** the standard Omarchy GTK layout with the terminal palette; hover and
  selection stay quiet (twilight violet), with no amber washes.
- **Zen:** the same roles as `colors.toml`; surfaces step through the dusk ramp
  and lantern amber marks focus.
- **Vencord:** upstream Midnight, recoloured: dusk panels, paper text, lantern
  amber as the accent ramp, and Midnight's moon on the home button.
- **Cava:** the theme colours from pond blue and teal at the base to flame,
  lantern and koi at the top.
- **Base24:** `dusk-lantern-base24.yaml` holds the same materials in Base24 slot
  order. It is a reference export; no installed consumer reads it.

## Guardrails

- Keep lantern amber rare and meaningful: focus, accent, active. Never body text.
- Do not add a white, a neutral grey ground, or a second lead accent.
- New wallpapers: one figure, exact ground colour, palette-only gradient map,
  lantern glow kept subtle. No scenery panoramas, no anime.
- The cursor follows `bright_foreground` (warm paper) because Omarchy derives it
  there; making it amber would need a hand-written terminal config.

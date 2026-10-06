# Obake — design notes

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
- **Around — the dusk.** The cool colours are not a pond but more of the same
  sky: ghost fire, moonmist, dusk glow and a ghost's plum robe, four violet
  lights told apart by lightness, never more saturated than the sky in the
  prints. Koi vermilion stays as the one hot warning.
- **Characters — the ghosts.** Wallpapers carry one figure each on the flat
  ground, lit by a pool of lantern light. The interface stays quiet so the
  figure can be the character.

## Palette

Two families, named by material, and only the two the wallpapers contain:
the lantern's warm light and the dusk's violet. Hexes live in `colors.toml`; these are the
roles they play.

| Material | Hex | Omarchy key(s) | Role |
|---|---|---|---|
| dusk indigo sky | `#1d1c3a` | `background` | Ground; also the exact wallpaper fill |
| deeper dusk | `#13122c` | `dark_background` | Recessed surfaces |
| nightfall | `#0b0a20` | `darker_background` | Deepest surfaces, bar wells |
| raised haze | `#2b2a48` | `lighter_background` | Raised surfaces, title bars |
| twilight violet | `#40356c` | `selection`, `selection_background` | Selection — a patch of later sky, not a light |
| dusk mist | `#9d9ab9` | `muted` | Comments, hints, inactive text |
| lantern-lit paper | `#e3c697` | `foreground` | Body text, lowered for long reading |
| paper in shadow | `#bea784` | `dark_foreground` | Secondary text |
| paper at the flame | `#f9e5c3` | `light_foreground`, `bright_foreground`, `selection_foreground` | Emphasis; Omarchy also derives the cursor from it |
| **lantern amber** | `#fea22a` | `accent`, `orange` | **Lead.** Focus border, active state, prompts |
| lantern glow | `#ffc36a` | `yellow` | Warnings, modified state; the lit-paper menu row |
| burnt wick | `#a3642a` | `brown` | Quiet warm structure, btop frames |
| koi vermilion | `#f56d2a` | `red` | Errors, alerts, bar attention state |
| ghost robe | `#c098c2` | `magenta` | Keywords, branches |
| onibi (ghost fire) | `#c0abe7` | `green` | Success, strings, executables |
| moonmist | `#cfccf1` | `cyan` | Links, symlinks |
| dusk glow | `#9797d3` | `blue` | Info, paths, functions |

Bright variants (`bright_*`) are the same materials nearer the surface or
nearer the flame: lighter and slightly less saturated, never a new hue.

### Deliberate slot remapping

Slot names are consumer schema labels, not colour instructions.

- `red` is the koi, not a generic danger red. Errors are vermilion because the
  koi is the one thing in the scene that is that colour.
- `orange` is the lantern itself and duplicates `accent`.
- `green`, `cyan`, `blue` and `magenta` are all the dusk: four violet lights at
  or below the sky's own peak chroma (0.087), separated by lightness and a
  small hue drift towards plum. There is no teal, green or sky blue in the
  prints, so there is none here.
- `yellow` is the lantern's glow, not a second accent.
- There is no white anywhere. The brightest value is warm paper.

### Measured

- Koi, lantern, glow and wick are measured from the wallpapers at their peak
  chroma; the dusk family never exceeds the sky's.
- Text on ground 10.0:1 WCAG (lowered from 11.4 for long reading), muted 6.1:1,
  lantern amber 8.1:1, koi vermilion 5.6:1, selection text 8.8:1.
- Background L 0.245 OKLCH with chroma 0.055 — a tinted ground, not a neutral.
- Accent chroma median 0.087, peak 0.18: the lantern and koi carry the
  saturation, the dusk stays quiet.

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
  menu and launcher select in ink on lit paper (`shell.menu.toml`,
  `shell.launcher.toml`: a glow fill with dusk-indigo text and no frame); the
  bar's attention state uses koi vermilion.
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
- **Cava:** from dusk glow and moonmist at the base up through the lantern's
  glow to koi at the top.
- **btop / cliamp:** wick box frames, lantern accent, graphs rising from the
  dusk into the lantern and the koi.
- **Base24:** `obake-base24.yaml` holds the same materials in Base24 slot
  order. It is a reference export; no installed consumer reads it.

## Guardrails

- Keep lantern amber rare and meaningful: focus, accent, active. Never body text.
- Do not add a white, a neutral grey ground, or a second lead accent.
- New wallpapers: one figure, exact ground colour, palette-only gradient map,
  lantern glow kept subtle. No scenery panoramas, no anime.
- The cursor follows `bright_foreground` (warm paper) because Omarchy derives it
  there; making it amber would need a hand-written terminal config.

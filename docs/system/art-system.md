---
type: system
---

# Арт-система

Арты генерируются в Midjourney. Поле `art_prompt` содержит готовый промпт, скопированный напрямую. Схема карточки и поля `art_prompt` / `art_image` описаны в `CLAUDE.md` (раздел «Система карточек»).

## Привязка PNG-арта к заметке

Готовый арт хранится как PNG и отображается прямо в MD-заметке через встраивание Obsidian.

**Конвенция:**

- **Одно изображение на сущность**, имя файла = её `id` (`kebab-case`, как у карты/фракции).
- **Папки:**
  - фракции — `assets/art/factions/<id>.png`
  - существа — `assets/art/cards/minions/<id>.png`
  - заклинания — `assets/art/cards/spells/<id>.png`
  - герои — `assets/art/cards/heroes/<id>.png`
  - оружие — `assets/art/cards/weapons/<id>.png` *(опциональный модуль)*
- **Поле `art_image`** во фронтматтере хранит этот путь (тег арта для инструментов/валидации).
- **Встраивание** в теле заметки — **стандартным Markdown** с относительным путём: `![<имя>](../../assets/art/.../<id>.png)`. Путь относителен к самому md-файлу (из `docs/factions/` или `cards/<тип>/` до корня — `../../`). Так картинка рендерится и в Obsidian, и на GitHub. **Не использовать `![[…]]`** — это Obsidian-синтаксис, GitHub его показывает как текст.

**Как пользоваться:** положи PNG по нужному пути с именем `<id>.png` — Obsidian отрисует его в заметке. Пока файла нет — на месте встраивания пустой плейсхолдер (заметка остаётся валидной). Менять MD не нужно: появление/замена файла сразу меняет картинку.

## Структура промпта

```
[ОПИСАНИЕ СУБЪЕКТА], [МОДИФИКАТОР ФРАКЦИИ], [БАЗОВЫЙ СТИЛЬ]
```

Промпт собирается из трёх частей в указанном порядке. Базовый стиль и модификатор фракции — константы, описание субъекта — уникально для каждой карты.

---

## Базовый стиль (финал каждого промпта)

```
painted trading card art, in the style of Arcane League of Legends animated series, painterly textured brushstrokes, dramatic chiaroscuro lighting, post-apocalyptic atmosphere, highly detailed concept art, dark moody palette with vivid accent lighting, portrait composition --ar 2:3 --v 6 --style raw
```

Этот хвост добавляется к **каждому** промпту без изменений.

---

## Модификаторы фракций

### Шакалы `jackals`
```
sandy yellow and rust red color palette, dust and sand particles, rusted improvised motorcycles and buggies, patchwork scrap armor and pipe weapons, tribal war paint, desperate raider gang aesthetic, sun-bleached wasteland under harsh light
```

### Пепел `ash`
```
radioactive chartreuse and burnt orange glow, retro-futuristic 1950s nuclear aesthetic, vacuum tube circuitry and analog dials, lead shielding with radiation hazard symbols, reactor energy crackling around the subject, corroded metal surfaces with atomic era insignia
```

### Химеры `chimera`
```
mutagen violet and toxic green bioluminescence, organic mutated flesh fused with exposed circuit boards, no straight angles, alien biology meets salvaged electronics, wet glistening organic surfaces, grotesque yet elegant mutation aesthetic
```

### Бастион `bastion`
```
gunmetal grey and amber warning-light color scheme, soot-stained riveted steel armor plating, heavy diesel engines and exhaust smoke, tracked war machines and mobile fortresses, brutal industrial mass, dieselpunk heavy machinery
```

### Сеть `net`
```
neon cyan and electric violet rim lighting, deep black background with holographic data stream particles, chrome cybernetic implants integrated into the subject, neural lace aesthetics, digital glitch distortion effects at the edges, high-tech urban decay environment
```

### Оазис `oasis`
```
warm golden sunlight breaking through cracked concrete ruins, lush leaf-green and teal accents, solar sail arrays integrated into organic living structures, moss and vines reclaiming destroyed architecture, hopeful warmth contrasted with battle-worn surfaces
```

### Мираж `mirage`
```
magenta and deep amber reality distortion glow, doubled and echoing silhouettes shimmering like a heat mirage, soldered amulet-antennas and old electronics as ritual objects, circuit traces forming glowing rune-like patterns, anomalous physics warping geometry, occult-technological fusion
```

---

## Логотипы фракций

Логотип — это **эмблема-знак** фракции (для бейджей, разделителей, UI), отдельная от карточного арта. Не портрет и не сцена: плоский узнаваемый символ в цветах фракции на изолированном фоне. База логотипа постоянна, символ — уникален. PNG логотипов (по желанию) — `assets/art/factions/logos/<id>.png`.

### База логотипа (хвост каждого промпта)

```
bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

> Совет: для более чистого знака можно добавить низкую стилизацию `--s 100` (или `--s 50`). Для прозрачного фона в MJ v6+ — заменить «isolated on plain dark background» на «on plain white background» и снять фон постобработкой.

### Готовые промпты

**Шакалы `jackals`** — оскал стаи, налётчики числом
```
aggressive emblem of a snarling jackal skull with bared fangs, flanked by crossed makeshift pipe-blades, rough tribal raider war-banner shape, sandy yellow and rust red palette, dust-worn stencil texture, scavenger gang insignia, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

**Пепел `ash`** — атом и реакторный огонь
```
emblem of a stylized atom whose nucleus is a burning flame, three orbital rings echoing a radiation trefoil, reactor sigil, radioactive lime green and burnt reactor orange, glowing nuclear hazard aesthetic, scorched metal stamp, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

**Химеры `chimera`** — мутировавшая спираль жизни
```
emblem of a mutated DNA double-helix twisting into fanged organic tendrils, asymmetric biomorphic silhouette with no straight lines, mutagen violet and toxic green, wet bioluminescent glow, genpunk biohazard insignia, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

**Бастион `bastion`** — клёпаный щит-крепость
```
emblem of a heavy riveted steel shield forming an armored bulwark, bold geometric fortress silhouette with industrial gear framing, gunmetal grey with amber warning-light accents, soot-stained dieselpunk stamp, brutal heavy-industry insignia, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

**Сеть `net`** — глитч-глаз из схем
```
emblem of a stylized eye formed from circuit-board traces and network nodes, digital glitch fracture splitting the silhouette, neon cyan and electric violet on black, holographic glitch aesthetic, cyberpunk hacker sigil, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

**Оазис `oasis`** — росток сквозь трещину
```
emblem of a single sprout breaking upward through cracked earth, encircled by a radiant sun-ray halo, clean balanced silhouette, leaf green and teal with warm golden sun glow, hopeful solarpunk insignia, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

**Мираж `mirage`** — двоящийся знак-антенна
```
emblem of a doubled echoing diamond sigil that shimmers and splits like a heat mirage, soldered antenna lines forming concentric rune-circles, magenta and gold reality-distortion glow, anomalous shimmer, occult-technological sigil, bold faction emblem, heraldic military insignia badge, centered iconic composition, clean recognizable silhouette, limited two-color palette with glowing accent, subtle weathered post-apocalyptic texture, flat vector graphic design, high contrast, isolated on plain dark background, sticker style --no text, letters, words, numbers, watermark, signature --ar 1:1 --v 6 --style raw
```

---

## Правила составления промпта

1. **Описание субъекта** — конкретный персонаж, устройство или сцена. Включать: позу, доминирующий визуальный элемент, действие или состояние.
2. **Не указывать** текст, цифры, логотипы, интерфейсы — только визуальный образ.
3. **Для заклинаний** — описывать эффект как визуальное явление, не персонажа.
4. **Для оружия** *(опциональный модуль)* — предмет крупным планом на нейтральном или фракционном фоне.
5. **Для героев** — три четверти фигуры, более детальный и эпичный субъект чем у обычных юнитов.

## Пример карточки

```markdown
---
id: heat-boiler
name: "Тепловой котёл"
type: minion
faction: ash
cost: 5
attack: 2
health: 6
rarity: common
tags: [mech, heavy]
art_prompt: "heavily armored guardian in a ruined nuclear bunker, massive lead-plated exosuit with glowing reactor core on the back, analog pressure gauges and vacuum tubes embedded in the chest plate, arms raised in defensive stance, radioactive chartreuse and burnt orange glow, retro-futuristic 1950s nuclear aesthetic, vacuum tube circuitry and analog dials, lead shielding with radiation hazard symbols, reactor energy crackling around the subject, corroded metal surfaces with atomic era insignia, painted trading card art, in the style of Arcane League of Legends animated series, painterly textured brushstrokes, dramatic chiaroscuro lighting, post-apocalyptic atmosphere, highly detailed concept art, dark moody palette with vivid accent lighting, portrait composition --ar 2:3 --v 6 --style raw"
art_image: "assets/art/cards/minions/heat-boiler.png"
artist: ""
---

![Тепловой котёл](../../assets/art/cards/minions/heat-boiler.png)

*«Третий реактор не взорвался. Он просто ушёл в поле. Котёл пошёл следом.»*

## Способность
**Провокация. Перегрев.**
*(стена `2/6`: в начале каждого хода `+1` к атаке — видно на правой полосе; **Сброс** наносит цели урон, равный текущей атаке, и возвращает атаку к базовой `2`)*
```

---

Лор и эстетика фракций для описания субъекта — [обзор фракций](../factions/_overview.md).

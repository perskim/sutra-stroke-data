# sutra-stroke-data

한자 획 자료 두 파일입니다. 경전 사경 앱 **Sutra+typing.works**(iOS · Android, (주)퍼스펙티브)의 사경 화면이 «지금 쓸 획»을 보여 주고 쓴 획을 알아보는 데 씁니다.
[KanjiVG](https://kanjivg.tagaini.net)와 [Make Me a Hanzi](https://github.com/skishore/makemeahanzi)에서 앱에 실린 글의 한자만 골라, 한국에서 쓰는 자형에 맞게 고친 것입니다.
두 원본의 사용 조건에 따라 고친 자료를 같은 사용권으로 여기에 공개합니다. 이 저장소에는 획 자료와 그 사용권 글만 있습니다(경전 본문 · 앱 코드는 없습니다).

판: 2026-11-25 · 앱에 싣는 파일과 바이트까지 같습니다.

| 파일 | 바탕 | 사용권 | 글자 수 |
|---|---|---|---|
| `strokes.kanjivg.json` | KanjiVG `r20260714` (main) | CC BY-SA 3.0 — `LICENSE-CC-BY-SA-3.0.txt` | 1,064 |
| `strokes.mmah.json` | Make Me a Hanzi `graphics.txt` (`bddc96d`) | Arphic Public License — `ARPHICPL.TXT` | 1,127 |

두 사용권은 한 파일에 섞을 수 없어 출처마다 파일을 나눴습니다.

## 원본과 만든 이

- **KanjiVG** — Copyright (C) 2009/2010/2011 Ulrich Apel. <https://kanjivg.tagaini.net> · Creative Commons Attribution-ShareAlike 3.0.
  받은 판: `kanjivg-20260714-main.zip` (sha256 `b5df6cd2bc249dd49b8041eb99e38ba9f8dc6b9ea57962a80084b4a315d1a7fc`).
- **Make Me a Hanzi** — Shaunak Kishore. <https://github.com/skishore/makemeahanzi>. `graphics.txt` 의 획 모양은 Arphic PL KaitiM GB · UKai 글꼴
  (Copyright (C) 1999 Arphic Technology Co., Ltd.)에서 나온 자료라 Arphic Public License 를 따릅니다.
  받은 판: 커밋 `bddc96d41bef78427ed0e034e9f7e31d71fd1b92` 의 `graphics.txt` (sha256 `a28c478b5178e98f67f510b2d52fde08a69dc664654ef43498253b9b764d46ee`).

## 무엇을 고쳤나

고친 내용은 파일마다 머리의 `changes` 에도 적혀 있습니다 — `changes.general`(전체에 한 일) · `changes.chars`(글자마다 한 일).

### `strokes.kanjivg.json` (형식 `strokes.v1`)

- 앱에 실린 글의 한자만 골랐습니다(main SVG 만, 변형 파일은 쓰지 않음).
- 획마다 베지어 중심선을 펴서 길이에 고르게 16점으로 다시 뽑고, 단위 정사각(x/109 · y/109, y 아래로)에 소수 넷째 자리까지 옮겼습니다. 획순과 쓰는 방향은 KanjiVG 그대로입니다.
- 한국 자형에 맞게 고친 글자 10자:
  - 일본 꼴 → 한국 꼴 4자 — 僧(曽 → 曾) · 器(大 → 犬) · 海 · 繁(毋 → 母, 母 의 획순은 한국식)
  - KanjiVG 에 없어 KanjiVG 부품으로 조립한 6자 — 卽(皀 + 卩) · 增(土 + 曾) · 揭(扌 + 曷) · 緣(糸 + 彖) · 說(言 + 兌) · 叵(匚 + 口)
- 艹 · 辶 은 KanjiVG 의 3획 꼴 그대로입니다(앱의 바탕 글꼴 Noto Serif CJK KR 과 같은 꼴). 그래서 쓰는 획 수가 사전 획수보다 艹 · 辶 하나마다 1 적습니다. 이렇게 쓰는 획 수가 사전 획수와 다른 57자(艹 · 辶 55자, 글꼴 꼴대로 점 없이 쓰는 者 · 諸 2자)는 `writeDiff` 에 까닭과 함께 있습니다.
- 싣지 않은 글자 100자는 `skipped` 에 까닭과 함께 있습니다 — KanjiVG 의 획 수가 한국식과 다른 53자, KanjiVG 에 없는 37자, 획 수를 아직 확인하지 못한 9자, 부품으로 만들 수 없는 1자(虛).
- 칸: `chars[글자]` = 획순대로, 획마다 중심선 점 16개 `[x, y]` · `write[글자]` = 쓰는 획 수 · `writeDiff` · `skipped` · `source` · `license` · `changes`.

### `strokes.mmah.json` (형식 `outline.v1`)

- 앱에 실린 글의 한자만 골랐습니다.
- 좌표를 MMAH 의 1024 격자(y 위로)에서 단위 정사각 x/1024 · (900 − y)/1024(y 아래로)로 옮겼습니다(소수 넷째 자리).
- 획 윤곽의 곡선을 펴서 다각형으로 만들고 줄였습니다(허용 어긋남 0.6 격자 단위, Ramer–Douglas–Peucker). 중심선(medians)은 길이에 고르게 16점으로 다시 뽑았습니다.
- 획순: 1,074자는 KanjiVG 획과 짝지어 KanjiVG 획순(한국 획순)에 맞췄습니다(`order: "kanjivg"`) — 그 가운데 실제로 획 자리나 방향이 바뀐 255자는 `changes.chars` 에 하나씩 적혀 있습니다. 두 자료가 획을 나누고 잇는 곳이 다른 37자(阝 의 귀를 한 획으로 · 艹 의 가로를 둘로 나눈 꼴 …)는 두 획을 한 단위로 합쳐 짝지었습니다. 짜임이 너무 달라 짝이 맞지 않는 96자는 MMAH 획순 그대로입니다(`order: "mmah"`).
- 2026-11-25(전수 점검): KanjiVG 에 없는 한국 꼴 19자는 일본 꼴(靑 ← 青 · 淸 ← 清 · 寬 ← 寛 · 虛 ← 虚 …)을 획순 참고로 씁니다. 짝을 다 못 짓던 글자 가운데 王 · 龶 · 堇 · 虍 가 다른 글자와 다른 차례이던 8자(勤 寬 徵 毒 淸 璃 虛 靑)를 KanjiVG 순서로 맞추고, 騃 의 馬 를 馬 · 騎 와 같은 차례(왼 세로 먼저)로 놓았습니다 — 바뀐 차례는 모두 눈으로 확인했습니다.
- 2026-11-25: 艹 를 十十 넷으로 쓴 해서 꼴 19자(薩 夢 華 莊 萬 藥 …)는 한국 순서 — 왼 一 · 왼 丨 · 오른 一 · 오른 丨 — 로 놓았습니다(MMAH 는 丨 一 丨 一).
- MMAH 에 없는 卽 은 MMAH 의 白 + 匕 + 即 의 卩 으로 조립했습니다.
- 2026-11-24: MMAH 에 없는 한국 꼴 25자를 같은 방법으로 MMAH 부품에서 지었습니다 — 같은 짜임의 MMAH 글자에서 부품 자리를 빌려 부품 획을 옮겨 늘이거나(喫 = 吃 의 口 + 契 · 淸 = 氵 + 靑 · 敎 = 爻 + 子 + 攵 · 旣 = 白 + 匕 + 旡 · 麤 = 鹿 셋 …), 꼴이 같은 MMAH 이체자를 씁니다(爲 ← 為 · 僞 ← 偽 · 晩 ← 晚 · 兎 ← 兔). 글자마다 무엇으로 지었는지는 파일 머리 `changes.chars` 에 있습니다. 남은 14자는 `missing` 에 있습니다.
- 쓰는 획 수(= 이 모양의 획 수)가 사전 획수와 다른 100자는 `writeDiff` 에 까닭과 함께 있습니다.
- 칸: `chars[글자].outline` = 획마다 채울 다각형들 `[[x, y], …]` · `.median` = 획마다 중심선 점 16개 · `.order` · `.write` · `writeDiff` · `missing` · `source` · `license` · `changes`.
- 파일 머리 `license` 의 «docs/licenses/» 는 앱 저장소 안의 자리이고, 이 저장소에서는 맨 위의 `ARPHICPL.TXT` 입니다(Arphic Public License 가 요구하는 대로 이름과 내용을 고치지 않았습니다).

## 쓰실 때

- `strokes.kanjivg.json` — CC BY-SA 3.0. 출처를 밝히고(예: «KanjiVG © Ulrich Apel, CC BY-SA 3.0 · 한국 자형으로 고침: Sutra+typing.works»), 고친 것이 있으면 무엇을 고쳤는지 적고, 고친 자료는 같은 사용권으로 내 주세요.
- `strokes.mmah.json` — Arphic Public License. 복사본마다 `ARPHICPL.TXT` 를 고치지 않고 함께 두고, 고쳤다면 고친 파일에 무엇을 언제 고쳤는지 적고, 고친 것을 같은 사용권으로 누구나 받을 수 있게 해 주세요.
- 이 글은 사용권을 간추린 안내일 뿐입니다. 조건은 두 사용권 글이 정합니다.

문의: typingworks@pers.kr

---

# sutra-stroke-data (English)

Two files of Chinese-character stroke data. The handwriting (sutra-copying) screen of **Sutra+typing.works** (iOS and Android, by Perspective, Inc.) uses them to show which stroke to write next and to recognise the strokes you have written.
They are subsets of [KanjiVG](https://kanjivg.tagaini.net) and [Make Me a Hanzi](https://github.com/skishore/makemeahanzi), limited to the characters that occur in the app's texts and adapted to the glyph forms used in Korea.
As both upstream licences require, the adapted data is published here under the same licences. This repository holds only the stroke data and its licence texts (no sutra texts, no app code).

Version: 2026-11-25 · byte-identical to the files shipped in the app.

| File | Based on | Licence | Characters |
|---|---|---|---|
| `strokes.kanjivg.json` | KanjiVG `r20260714` (main) | CC BY-SA 3.0 — `LICENSE-CC-BY-SA-3.0.txt` | 1,064 |
| `strokes.mmah.json` | Make Me a Hanzi `graphics.txt` (`bddc96d`) | Arphic Public License — `ARPHICPL.TXT` | 1,127 |

The two licences cannot be mixed in one file, so the data is kept in one file per source.

## Upstream works and authors

- **KanjiVG** — Copyright (C) 2009/2010/2011 Ulrich Apel. <https://kanjivg.tagaini.net> · Creative Commons Attribution-ShareAlike 3.0.
  Release used: `kanjivg-20260714-main.zip` (sha256 `b5df6cd2bc249dd49b8041eb99e38ba9f8dc6b9ea57962a80084b4a315d1a7fc`).
- **Make Me a Hanzi** — Shaunak Kishore. <https://github.com/skishore/makemeahanzi>. The stroke shapes in `graphics.txt` derive from the Arphic PL KaitiM GB and UKai fonts
  (Copyright (C) 1999 Arphic Technology Co., Ltd.) and are therefore under the Arphic Public License.
  Version used: `graphics.txt` at commit `bddc96d41bef78427ed0e034e9f7e31d71fd1b92` (sha256 `a28c478b5178e98f67f510b2d52fde08a69dc664654ef43498253b9b764d46ee`).

## What was changed

Every change is also recorded in each file's `changes` field — `changes.general` (what was done to the whole file) and `changes.chars` (what was done to a single character; these notes are in Korean).

### `strokes.kanjivg.json` (format `strokes.v1`)

- Only the characters of the app's texts (main SVG files only, no variants).
- Each stroke's Bézier centreline is flattened and resampled to 16 points evenly by arc length, then mapped to the unit square (x/109, y/109, y down) with 4 decimals. Stroke order and drawing direction are KanjiVG's.
- Ten characters adapted to Korean forms:
  - four Japanese forms replaced by Korean forms — 僧 (曽 → 曾), 器 (大 → 犬), 海 and 繁 (毋 → 母, with the Korean stroke order of 母);
  - six characters absent from KanjiVG, assembled from KanjiVG components — 卽 (皀 + 卩), 增 (土 + 曾), 揭 (扌 + 曷), 緣 (糸 + 彖), 說 (言 + 兌), 叵 (匚 + 口).
- 艹 and 辶 keep KanjiVG's three-stroke forms (the same shapes as the app's trace font, Noto Serif CJK KR), so the written stroke count is one less than the Korean dictionary count for each 艹/辶. The 57 characters whose written count differs from the dictionary count (55 with 艹/辶, plus 者 and 諸, written without the dot as in the font) are listed in `writeDiff` with the reason.
- 100 characters are left out and listed in `skipped` with the reason: 53 whose KanjiVG stroke count differs from the Korean count, 37 that KanjiVG lacks, 9 whose stroke count we have not yet verified, and 1 (虛) that cannot be assembled from components.
- Fields: `chars[char]` = strokes in order, each 16 centreline points `[x, y]` · `write[char]` = strokes to write · `writeDiff` · `skipped` · `source` · `license` · `changes`.

### `strokes.mmah.json` (format `outline.v1`)

- Only the characters of the app's texts.
- Coordinates mapped from MMAH's 1024 grid (y up) to the unit square x/1024, (900 − y)/1024 (y down), 4 decimals.
- Stroke outlines' curves flattened to polygons and simplified (tolerance 0.6 grid units, Ramer–Douglas–Peucker); medians resampled to 16 points by arc length.
- Stroke order: 1,074 characters are matched stroke by stroke to the KanjiVG data above and follow the KanjiVG (Korean) order (`order: "kanjivg"`) — the 255 of them whose strokes actually moved or were reversed are noted one by one in `changes.chars`. For 37 of them the two sources split or join strokes differently (the ear of 阝 as one stroke, a 艹 whose horizontal is split in two …), so two strokes are matched as one unit. The 96 characters whose structures disagree too much keep MMAH's order (`order: "mmah"`).
- 2026-11-25 (full audit): 19 Korean forms absent from KanjiVG take the Japanese form as the order reference (靑 ← 青, 淸 ← 清, 寬 ← 寛, 虛 ← 虚 …). Among characters that could not be matched as a whole, the 8 whose 王 · 龶 · 堇 · 虍 ran in a different order from every other character (勤 寬 徵 毒 淸 璃 虛 靑) now follow the KanjiVG order, and the 馬 of 騃 follows 馬 and 騎 (left vertical first). Every changed order was checked by eye.
- 2026-11-25: the 19 characters whose 艹 is drawn as four strokes (十十) in the kaishu form (薩 夢 華 莊 萬 藥 …) put it in the Korean order — left 一, left 丨, right 一, right 丨 (MMAH has 丨 一 丨 一).
- 卽, absent from MMAH, is assembled from MMAH's 白 + 匕 + the 卩 of 即.
- 2026-11-24: 25 more characters MMAH lacks in their Korean form are built the same way from MMAH components — parts moved into the boxes of the matching parts of an MMAH character of the same structure (喫 = 口 of 吃 + 契, 淸 = 氵 + 靑, 敎 = 爻 + 子 + 攵, 旣 = 白 + 匕 + 旡, 麤 = three 鹿 …), or an MMAH variant of the same shape (爲 ← 為, 僞 ← 偽, 晩 ← 晚, 兎 ← 兔). What each is built from is in `changes.chars`. The remaining 14 are listed in `missing`.
- The 100 characters whose written stroke count differs from the Korean dictionary count are listed in `writeDiff` with the reason.
- Fields: `chars[char].outline` = per stroke, the polygons to fill `[[x, y], …]` · `.median` = per stroke, 16 centreline points · `.order` · `.write` · `writeDiff` · `missing` · `source` · `license` · `changes`.
- The path «docs/licenses/» in the file's `license` field is where the licence sits in the app's own repository; here it is `ARPHICPL.TXT` at the top level, with its name and contents unaltered as the Arphic Public License requires.

## If you use these files

- `strokes.kanjivg.json` — CC BY-SA 3.0. Give credit (for example “KanjiVG © Ulrich Apel, CC BY-SA 3.0 · adapted to Korean forms by Sutra+typing.works”), say what you changed if you change it, and release your adaptation under the same licence.
- `strokes.mmah.json` — Arphic Public License. Keep `ARPHICPL.TXT` unaltered with every copy; if you modify the file, state in it what you changed and when, and make your modifications freely available under the same licence.
- This page is only a summary. The two licence texts are what govern.

Contact: typingworks@pers.kr

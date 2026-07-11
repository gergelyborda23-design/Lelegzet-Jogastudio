# Lélegzet — Design rendszer

Meleg, földes, prémium jóga-arculat egy kis újbudai stúdióhoz. A hangulat: nyugalom,
természetes fény, lassú tempó. Inspiráció: a „Vidda" referencia meleg krém/olíva iránya.

---

## 1. Alapelvek

1. **Lélegző terek** — bőséges whitespace, semmi zsúfoltság. A levegő maga a dizájn.
2. **Meleg, földes nyugalom** — krém alap, olíva-zöld akcentus, agyag pont-szín. Semmi rikító.
3. **Editorial tipográfia** — serif display + tiszta sans kontraszt, mint egy jó magazinban.
4. **Lágy, lekerekített formák** — gyengéd radius, puha, meleg árnyékok, semmi éles doboz.
5. **Valódi fény, valódi testek** — természetes fotók, nem sztereotip stockok.
6. **Csendes mozgás** — finom, lassú átmenetek (fade, enyhe emelkedés). A UI is „lélegzik".

---

## 2. Színpaletta (hex + szerep)

| Token | Hex | Szerep |
|---|---|---|
| `--cream` | `#F4EFE6` | Fő háttér (meleg papír) |
| `--cream-deep` | `#EAE2D3` | Váltakozó szakasz-háttér (homok) |
| `--surface` | `#FBF8F2` | Kártya / felület (törtfehér) |
| `--ink` | `#2B2A26` | Fő szöveg (meleg majdnem-fekete) |
| `--ink-soft` | `#6E6A5F` | Másodlagos szöveg, feliratok |
| `--olive` | `#57634A` | Primer akcentus — gombok, linkek, kiemelés |
| `--olive-hover` | `#454F3A` | Gomb hover |
| `--olive-deep` | `#2E3626` | Sötét szakaszok, footer háttér |
| `--clay` | `#B06B4E` | Pont-szín (terrakotta) — nagyon takarékosan, kiemelésre |
| `--sand` | `#DED6C5` | Szegélyek, elválasztók |
| `--cream-on-dark` | `#F1ECE0` | Szöveg sötét háttéren |

**Kontraszt-szabály:** sötét szöveg (`--ink`) csak világos alapon (`--cream`, `--surface`);
sötét szakaszon (`--olive-deep`) mindig `--cream-on-dark`. Feliratok min. 4.5:1.

---

## 3. Tipográfia

- **Display / címsorok:** `Fraunces` (serif, opsz — meleg, organikus, prémium). Google Fonts.
- **Törzs / UI:** `Manrope` (sans, tiszta, barátságos geometrikus). Google Fonts.

```
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,300;9..144,400;9..144,500;9..144,600&family=Manrope:wght@400;500;600;700&display=swap" rel="stylesheet">
```

**Típus-skála (fluid, clamp):**

| Szerep | Méret | Font / súly |
|---|---|---|
| Display (hero H1) | `clamp(2.6rem, 6vw, 4.6rem)` | Fraunces 400, line-height 1.05 |
| H2 (szakaszcím) | `clamp(2rem, 3.5vw, 3rem)` | Fraunces 400 |
| H3 (kártyacím) | `1.375rem` | Fraunces 500 |
| Címke / eyebrow | `0.8rem` | Manrope 600, letter-spacing `.16em`, UPPERCASE |
| Törzs | `1.0625rem` (17px) | Manrope 400, line-height 1.7 |
| Kicsi / felirat | `0.9rem` | Manrope 500 |

> **Figma-figyelmeztetés:** a Fraunces/Manrope a HTML-ben szép; a Figma write-to-canvas
> egyedi betűt nem visz át — ott rendszerbetű lesz, kézzel kell a Fraunces/Manrope-ra állítani.

---

## 4. Térköz-ritmus

4px-es alapskála: `4, 8, 12, 16, 24, 32, 48, 64, 80, 96, 120`.
- **Szakasz-padding (függőleges):** `clamp(64px, 10vw, 120px)`
- **Tartalom max-szélesség:** `1200px`, oldalsó padding `clamp(20px, 5vw, 48px)`
- **Kártya belső padding:** `32px` (desktop), `24px` (mobil)
- **Elem-közök:** cím→törzs `16px`, törzs→gomb `24px`, kártyák közt `24px`

---

## 5. Formák, árnyék, gomb, kártya

**Lekerekítés:** `--r-sm: 12px`, `--r-md: 20px`, `--r-lg: 32px`, `--r-pill: 999px`.

**Árnyékok (meleg tónus):**
- `--shadow-sm: 0 2px 10px rgba(60,50,30,.05)`
- `--shadow-md: 0 12px 40px rgba(60,50,30,.08)`
- `--shadow-lg: 0 26px 70px rgba(50,42,26,.12)`

**Gombok:**
- *Primer:* olíva háttér, krém szöveg, `--r-pill`, padding `15px 30px`, súly 600.
  Hover: `--olive-hover` + enyhe emelkedés (`translateY(-2px)`) + `--shadow-md`.
- *Másodlagos:* átlátszó háttér, `1.5px solid --olive`, olíva szöveg, `--r-pill`.
  Hover: olíva háttér, krém szöveg.
- Átmenet: `all .25s ease`.

**Kártyák:** `--surface` háttér, `--r-lg`, `1px solid --sand`, `--shadow-sm`.
Hover (interaktív kártyán): `--shadow-md` + `translateY(-4px)`.
Kiemelt kártya (pl. „legnépszerűbb" bérlet): `--olive` szegély 1.5px + kis `--clay` címke.

---

## 6. Kész CSS-változók (másolható `:root`)

```css
:root{
  --cream:#F4EFE6; --cream-deep:#EAE2D3; --surface:#FBF8F2;
  --ink:#2B2A26; --ink-soft:#6E6A5F;
  --olive:#57634A; --olive-hover:#454F3A; --olive-deep:#2E3626;
  --clay:#B06B4E; --sand:#DED6C5; --cream-on-dark:#F1ECE0;
  --r-sm:12px; --r-md:20px; --r-lg:32px; --r-pill:999px;
  --shadow-sm:0 2px 10px rgba(60,50,30,.05);
  --shadow-md:0 12px 40px rgba(60,50,30,.08);
  --shadow-lg:0 26px 70px rgba(50,42,26,.12);
  --maxw:1200px; --pad:clamp(20px,5vw,48px);
  --section-y:clamp(64px,10vw,120px);
  --font-display:'Fraunces',Georgia,serif;
  --font-body:'Manrope',system-ui,sans-serif;
}
```

---

## 7. Fotó-katalógus (mit hová)

A `webdesign figma/stock fotók/` mappából. Csak a márkába illőket használjuk;
a szerzetes/templom/szobor képeket kerüljük (travel-hangulat, nem stúdió).

| Fájl | Tartalom | Javasolt hely |
|---|---|---|
| `airamdphoto-36760973` | Sziluett lótusz, meleg háttérfény | **Hero** (teljes kép, szöveg rá) / Yin |
| `mikhail-nilov-7500026` | Világos stúdió, növények, ablak | **Rólunk** / Vinyasa |
| `vlada-karpovich-4534867` | Crow póz, világos stúdió, nagy ablak | Rólunk / óratípus / galéria |
| `soylulusacafotos-15685823` | Fekete-fehér editorial hátrahajlás | **Yin / idézet-szakasz** |
| `unni-rajan-...-37244208` | Gyerekpóz fűben, mala, naplemente | **CTA** / nyugalom-akcentus |
| `joao-pedro-...-15552293` | Meditáció vízesésnél, meleg | Természet-akcentus |
| `shootsaga-32794958` | Fa-póz sziklán, erdő | Óratípus / galéria |
| `shootsaga-32847435` | Előrehajlás erdei ösvényen | Galéria |
| `jonathanborba-13911189` | Harcos-póz dzsungel (piros matrac) | Tartalék |
| `wolfart-13173125` | Fejenállás kültér | Tartalék / dinamikus akcentus |

> Az oldalon minden fotónál ügyelni kell: **arc ne legyen levágva**, és sötét overlay
> kerüljön a szöveg mögé (kontraszt), ha kép fölé írunk.

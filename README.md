# Arcade BK — statički sajt

Single-page sajt za klub Arcade u Banji Koviljači. Retrowave/CRT estetika sa neon paletom (cyan / magenta / yellow / deep purple).

- **Live:** https://arcade-bk.vercel.app/ *(trenutno u test modu — vidi „Pre objave")*
- **Repo:** https://github.com/jankovicsrb-droid/arcadebk

## Struktura

```
arcadebk/
├── index.html       # Glavna i jedina stranica
├── styles.css       # Svi stilovi
└── assets/
    └── logo.png     # Logo kluba
```

Bez build koraka, bez dependency-ja, bez JavaScript-a — otvoriš `index.html` u browseru i radi. Fontovi se učitavaju sa Google Fonts (`Audiowide`, `Chakra Petch`, `JetBrains Mono`), što je jedini eksterni zahtev.

Deploy je statički (Vercel servira root folder kako jeste, nema `vercel.json` niti build komande).

## Sekcije

1. **Hero** — logo, naslov, dva CTA-a, tri stat-a
2. **Aktivnosti** — 7 kartica (PS5, PS4, Bilijar, Stoni fudbal, Pikado, Društvene igre, Jamb)
3. **Cenovnik** — tabelarni prikaz svih tarifa
4. **Rođendani & zabave** — privatan i delimičan zakup
5. **Lokacija** — adresa, radno vreme, stilizovana mapa
6. **Kontakt** — Viber, WhatsApp, Telegram, E-mail
7. **Footer**

## Pre objave

Sajt je namerno u **test modu** — dve stvari koje moraju da se skinu kad sadržaj bude finalan:

- [ ] `[TEST]` prefiks u `<title>` (`index.html`, linija 5)
- [ ] `<meta name="robots" content="noindex, nofollow">` (`index.html`, linija 7) — dok ovo stoji, sajt se ne indeksira

Podaci koje treba potvrditi sa klubom:

- [ ] **Radno vreme** — trenutno `Pon–Pet 16:00–02:00 / Sub–Ned 14:00–04:00` (sekcija Lokacija)
- [ ] **Koordinate** `44.302N · 19.297E` u uglu mape — dekorativne, nisu izmerene
- [ ] **Kapacitet** `SAVRŠENO ZA EKIPU OD 6 - 25` na rođendanskom posteru
- [ ] **Hero stat** `12h+` radno vreme i `24/7` rezervacije — `24/7` protivreči tekstu u sekciji Kontakt („odgovaramo u toku radnog vremena")

Tehnički dug (ništa blokirajuće):

- [ ] `og:image` je relativna putanja — za link preview na društvenim mrežama treba apsolutni URL
- [ ] `assets/logo.png` je 448 KB, a prikazuje se na max 320px — vredi kompresovati
- [ ] Mapa u sekciji Lokacija je stilizovani placeholder (`.map-frame`), ne prava mapa. Dugme „Otvori u mapi" ipak vodi na ispravan Google Maps upit.

## Kontakt podaci

Telefon `+381 69 403 0749` pokriva sva tri chat kanala:

| Kanal | Link |
|---|---|
| Viber | `viber://chat?number=%2B381694030749` |
| WhatsApp | `https://wa.me/381694030749` |
| Telegram | `https://t.me/+381694030749` |
| E-mail | `mailto:vezilicn@gmail.com` |

Mejl je lični, ne zvanični klupski, pa se **adresa namerno ne prikazuje** na stranici — kartica piše samo „Otvori mejl →", a `mailto:` radi normalno. Kad klub dobije zvaničnu adresu, promeni `href` i po želji prikaži je u `.handle` polju.

## Paleta i tipografija

CSS varijable su na `:root` u `styles.css`:

```css
--cyan:        #22e1ff   /* PlayStation, info akcenti */
--magenta:     #ff3df0   /* CTA, highlight */
--yellow:      #fff14d   /* badges, mapa pin, naglašavanja */
--purple-deep: #0a0014   /* glavna pozadina */
--purple-mid:  #1c0533
--purple-glow: #2d0860
--ink:         #f6e4ff   /* tekst */
--ink-dim:     rgba(246,228,255,0.65)
```

Fontovi:

- `Audiowide` — display (h1, h2, dugmad, brendiranje)
- `Chakra Petch` — body
- `JetBrains Mono` — meta-tekst, kicker labele, mali UI tekst

## Karakteristike dizajna

- **Neon backdrop** — gradijentno sunce + perspektivni grid preko cele stranice (`body::before`)
- **CRT scanlines** — globalni overlay sa vinjetom (`body::after`, `mix-blend-mode: multiply`)
- **Neon glow** — `text-shadow` i `filter: drop-shadow` na akcentima
- **Clip-path „iseckani" uglovi** na karticama i dugmadima
- **Sun-grid horizont** u hero sekciji (`.hero-grid`)

## Responsive

Implementirana su četiri breakpointa na dnu `styles.css`:

| Breakpoint | Šta se menja |
|---|---|
| `≤1100px` | Manji padding sekcija, hero naslov 72px |
| `≤900px` | Hero u jednu kolonu (logo ide iznad teksta), aktivnosti 2 kolone, `.bday` i `.map-wrap` u jednu kolonu, kontakt 2 kolone, zaglavlje cenovnika se krije |
| `≤600px` | Sve u jednu kolonu, nav prelazi u horizontalni scroll (ticker se krije), dugmad puna širina, redovi cenovnika se prelamaju u kartice (naziv + jedinica levo, cena desno) |
| `≤400px` | Hero naslov 36px, logo 130px, manji stat-ovi |

## Licenca / asseti

- Logo (`assets/logo.png`) je vlasništvo kluba Arcade BK.
- Fontovi su Google Fonts (besplatni za komercijalnu upotrebu).

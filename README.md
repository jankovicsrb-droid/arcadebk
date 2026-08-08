# Arcade BK — Statički sajt

Single-page sajt za klub Arcade u Banji Koviljači. Full retrowave/CRT estetika sa neon paletom (cyan / magenta / yellow / deep purple).

## Struktura

```
arcade-bk/
├── index.html       # Glavna i jedina stranica
├── styles.css       # Svi stilovi
└── assets/
    └── logo.png     # Logo klub-a
```

Bez build koraka — otvoriš `index.html` u browseru i radi. Fontovi se učitavaju sa Google Fonts (`Audiowide`, `Chakra Petch`, `JetBrains Mono`).

## Sekcije

1. **Hero** — logo + naslov + CTA-ovi
2. **Aktivnosti** — 7 kartica (PS5, PS4, Bilijar, Stoni fudbal, Pikado, Društvene igre, Jamb)
3. **Cenovnik** — tabelarni prikaz svih tarifa
4. **Rođendani & zabave** — informacije o privatnom zakupu
5. **Lokacija** — adresa + radno vreme + stilizovana mapa-placeholder
6. **Kontakt** — Viber, WhatsApp, Telegram, E-mail kartice
7. **Footer**

## TODO — popuniti pre objave

Sve placeholder vrednosti su označene tako da se lako nađu pretragom (`+381 6X`, `XXXXXXXX`, `info@arcade-bk.rs`, `arcade_bk`).

- [ ] **Telefon** za Viber i WhatsApp linkove
    - U `index.html`: `viber://chat?number=%2B381XXXXXXXXX` i `https://wa.me/381XXXXXXXXX`
    - U handle tekstu: `+381 6X XXX XXXX`
- [ ] **Telegram username** — trenutno `@arcade_bk` (i `https://t.me/arcade_bk`)
- [ ] **Email** — trenutno `info@arcade-bk.rs`
- [ ] **Radno vreme** — trenutno default `Pon–Pet 16:00–02:00 / Sub–Ned 14:00–04:00` (sekcija "Lokacija")
- [ ] **Google Maps link** — sekcija "Lokacija", dugme "Otvori u mapi" (`href="#"`). Idealno embed-ovati pravu mapu umesto stilizovanog placeholder-a u `.map-frame`.
- [ ] **Koordinate** — `44.302N · 19.297E` u donjem-desnom uglu mape (placeholder)
- [ ] (Opciono) Rođendan-poster tekst `SAVRŠENO ZA EKIPU OD 6 - 25` — proveriti realan kapacitet
- [ ] (Opciono) Hero stat `12h+` radno vreme — proveriti

## Paleta i tipografija

CSS varijable su na `:root` u `styles.css`:

```css
--cyan:        #22e1ff   /* PlayStation, info akcenti */
--magenta:     #ff3df0   /* CTA, highlight */
--yellow:      #fff14d   /* badges, mapa pin, naglašavanja */
--purple-deep: #0a0014   /* glavna pozadina */
--purple-mid:  #1c0533
--ink:         #f6e4ff   /* tekst */
--ink-dim:     rgba(246,228,255,0.65)
```

Fontovi:
- `Audiowide` — display (h1, h2, dugmad, brendiranje)
- `Chakra Petch` — body
- `JetBrains Mono` — meta-text, kicker labele, mali UI tekst

## Karakteristike dizajna

- **CRT scanlines** — globalni overlay preko cele stranice (`body::after`)
- **Neon glow** — `text-shadow` i `filter: drop-shadow` na akcentima
- **Clip-path "iseckani" uglovi** na karticama i dugmadima — daje arcade/sci-fi osećaj
- **Sun-grid horizont** u hero sekciji (`.hero-grid`)

## Responsive

Trenutno fiksiran desktop layout (1280px+). **Mobile breakpoint nije implementiran** — to je sledeći korak ako sajt treba da radi na telefonu (a verovatno treba). Predlog:
- Hero `grid-template-columns: 1fr` ispod 900px, logo manji
- `.activities`, `.contact-grid`, `.bday`, `.map-wrap` → 1 kolona ispod 900px
- `.section` padding 24–32px ispod 600px
- `.pl-header` i `.pl-row` → preformatirati u kartice ispod 700px (grid-template-columns ne radi dobro za 4-kolone na mobilnom)
- Top bar nav → hamburger ili horizontalni scroll

## Licenca / asseti

- Logo (`assets/logo.png`) je vlasništvo klub-a Arcade BK.
- Fontovi su Google Fonts (besplatno za komercijalnu upotrebu).
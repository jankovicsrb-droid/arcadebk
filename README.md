# Arcade BK - statički sajt

Single-page sajt za klub Arcade u Banji Koviljači. Retrowave/CRT estetika sa neon paletom (cyan / magenta / yellow / deep purple).

- **Domen:** https://arcadebk.rs
- **Vercel:** https://arcade-bk.vercel.app/
- **Repo:** https://github.com/jankovicsrb-droid/arcadebk

## Struktura

```
arcadebk/
├── index.html       # PRIVREMENO: „Uskoro" landing (ono što domen trenutno prikazuje)
├── sajt.html        # Pun sajt - radna verzija, noindex dok se ne završi
├── styles.css       # Svi stilovi za obe stranice
└── assets/
    └── logo.png     # Logo kluba
```

## Trenutno stanje - „Uskoro" landing

Domen prikazuje privremenu stranicu jer pun sajt još čeka podatke (cene za računare i volan, kapacitet za rođendane). Pun sajt živi na `/sajt.html` i može se otvoriti u browseru radi pregleda, ali nosi `noindex, nofollow` da ga Google ne pokupi u nedovršenom stanju.

Landing je na istoj temi i deli isti `styles.css`: stilovi su na dnu fajla, u bloku označenom `„USKORO" stranica`.

### Kako se radi switch kad sajt bude gotov

```bash
git rm index.html          # baci privremeni landing
git mv sajt.html index.html
```

Pa u novom `index.html` obriši red:

```html
<meta name="robots" content="noindex, nofollow">
```

I opciono obriši `„USKORO"` blok sa dna `styles.css`: oko 60 linija koje više ništa ne stilizuju. Push na `main` i Vercel odmah objavi.

Bez build koraka, bez dependency-ja, bez JavaScript-a - otvoriš `index.html` u browseru i radi. Fontovi se učitavaju sa Google Fonts (`Audiowide`, `Chakra Petch`, `JetBrains Mono`), što je jedini eksterni zahtev.

Deploy je statički (Vercel servira root folder kako jeste, nema `vercel.json` niti build komande).

## Sekcije

1. **Hero**: logo, naslov, dva CTA-a, tri stat-a
2. **Aktivnosti**: 9 kartica (PS5, PS4, Bilijar, Računari, Volan, Stoni fudbal, Pikado, Društvene igre, Jamb)
3. **Cenovnik**: tarife i cene pića, u segmentima
4. **Rođendani & zabave**: privatan i delimičan zakup
5. **Lokacija**: adresa, radno vreme, stilizovana mapa
6. **Kontakt**: Viber, WhatsApp, Telegram, E-mail
7. **Footer**

## Radno vreme

**Svakog dana 15:00 – 00:00.** Pojavljuje se na dva mesta u `index.html`:

- sekcija Lokacija, `.addr-card` red sa `⏱` ikonicom
- hero stat `15–00` (drugi po redu)

Treći hero stat je `7/7 Dana u nedelji`. Ranije je tu stajalo `24/7 Rezervacije`, što je protivrečilo tekstu u sekciji Kontakt („odgovaramo u toku radnog vremena") - otvoreno je 9h dnevno, ne 24h.

## Cenovnik

Cenovnik je podeljen u segmente preko `.pl-group` zaglavlja unutar jednog `.pricelist` kontejnera: Igre i aktivnosti, Pivo, Bezalkoholna pića, Kafa, Alkoholna pića, Kokteli i mikseri.

Dodavanje novog segmenta je jedan `<div class="pl-group">// NAZIV</div>` pa `.pl-row` redovi ispod njega. `.pl-header` (zaglavlje kolona) se stavlja samo tamo gde se značenje kolona menja, trenutno dva puta: na igrama i na prvoj grupi pića.

Cene igara su **po satu**, a minimum zakupa je 30 minuta. Dva izuzetka: stoni fudbal se naplaćuje po 15 minuta, pikado po kreditu. Oba izuzetka se vide iz kolone „Jedinica", a minimum zakupa stoji u `.section-tag` sekcije Aktivnosti.

## Otvoreno

Sadržaj koji treba potvrditi sa klubom:

- [ ] **Kapacitet** `SAVRŠENO ZA EKIPU OD 6 - 25` na rođendanskom posteru
- [ ] **Pomorandža i breskva** (200 din) su unete pod tim imenima kako ih je vlasnik naveo; ako su sokovi, vredi precizirati naziv
- [ ] **Zapremine** su poznate samo za piva (sva su 0,33 l); sokovi i ostala pića nemaju navedenu količinu, pa im u koloni „Jedinica" stoji `din / kom`

Tehnički dug (ništa blokirajuće):

- [ ] `assets/logo.png` je 448 KB, a prikazuje se na max 320px - vredi kompresovati
- [ ] Mapa u sekciji Lokacija je stilizovani placeholder (`.map-frame`), ne prava mapa. Dugme „Otvori u mapi" ipak vodi na ispravan Google Maps upit.
- [ ] Nema `robots.txt` ni `sitemap.xml`: za jednu stranicu nije neophodno, ali ne škodi

## SEO / link preview

Sajt više **nije** u test modu - `[TEST]` prefiks i `noindex, nofollow` su uklonjeni, Google sme da indeksira.

Apsolutni URL-ovi u `<head>`-u su vezani za `https://arcadebk.rs/`:

- `<link rel="canonical">`
- `og:url`
- `og:image` → `https://arcadebk.rs/assets/logo.png` (1200×1108, dimenzije deklarisane preko `og:image:width/height`)

**Ako se domen ikad promeni, ova četiri mesta treba ažurirati.** Relativna `og:image` putanja ne radi - Viber, WhatsApp i Facebook zahtevaju apsolutan URL da bi prikazali preview.

Logo je skoro kvadratan, pa je `twitter:card` namerno `summary`, a ne `summary_large_image` (koja očekuje 1.91:1).

## Kontakt podaci

Telefon `+381 69 403 0749` pokriva sva tri chat kanala:

| Kanal | Link |
|---|---|
| Telefon | `tel:+381694030749` |
| Viber | `viber://chat?number=%2B381694030749` |
| WhatsApp | `https://wa.me/381694030749` |
| Telegram | `https://t.me/+381694030749` |
| Instagram | `https://www.instagram.com/arcade_bk/` |
| E-mail | `mailto:vezilicn@gmail.com` |

Kontakt mreža je `repeat(3, 1fr)`: šest kartica staje u dva čista reda. Ako se broj kartica menja, treba uskladiti i `.contact-grid` da ne ostanu siročići u poslednjem redu.

Mejl je lični, ne zvanični klupski, pa se **adresa namerno ne prikazuje** na stranici - kartica piše samo „Otvori mejl →", a `mailto:` radi normalno. Kad klub dobije zvaničnu adresu, promeni `href` i po želji prikaži je u `.handle` polju.

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

- `Audiowide`: display (h1, h2, dugmad, brendiranje)
- `Chakra Petch`: body
- `JetBrains Mono`: meta-tekst, kicker labele, mali UI tekst

## Karakteristike dizajna

- **Neon backdrop**: gradijentno sunce + perspektivni grid preko cele stranice (`body::before`)
- **CRT scanlines**: globalni overlay sa vinjetom (`body::after`, `mix-blend-mode: multiply`)
- **Neon glow**: `text-shadow` i `filter: drop-shadow` na akcentima
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

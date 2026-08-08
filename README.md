# Arcade BK - statički sajt

Single-page sajt za klub Arcade u Banji Koviljači. Retrowave/CRT estetika sa neon paletom (cyan / magenta / yellow / deep purple).

- **Domen:** https://arcadebk.rs
- **Vercel:** https://arcade-bk.vercel.app/
- **Repo:** https://github.com/jankovicsrb-droid/arcadebk

## Struktura

```
arcadebk/
├── index.html       # Glavna i jedina stranica
├── styles.css       # Svi stilovi
├── robots.txt       # Pravila za pretraživače i putanja do sitemap-a
├── sitemap.xml      # Kanonski URL javne stranice
└── assets/
    ├── logo.png          # Originalni logo kluba
    ├── og-preview.jpg    # Široki preview za deljenje linka
    └── arcadebk-qr.png   # QR kod sajta
```

Bez build koraka, bez dependency-ja, bez JavaScript-a - otvoriš `index.html` u browseru i radi. Fontovi se učitavaju sa Google Fonts (`Audiowide`, `Chakra Petch`, `JetBrains Mono`), što je jedini eksterni zahtev.

Deploy je statički (Vercel servira root folder kako jeste, nema `vercel.json` niti build komande).

## Sekcije

1. **Hero**: logo, naslov, dva CTA-a, tri stat-a
2. **Aktivnosti**: 8 kartica (PS5, Bilijar, Računari, Volan, Stoni fudbal, Pikado, Društvene igre, Jamb)
3. **Cenovnik**: cene pića, u segmentima
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

Cenovnik je podeljen u segmente preko `.pl-group` zaglavlja unutar jednog `.pricelist` kontejnera: Pivo, Bezalkoholna pića, Kafa, Alkoholna pića, Kokteli i mikseri. Cene igara prikazane su samo u sekciji Aktivnosti, da se sadržaj ne duplira.

Dodavanje novog segmenta je jedan `<div class="pl-group">// NAZIV</div>` pa `.pl-row` redovi ispod njega. `.pl-header` (zaglavlje kolona) trenutno se nalazi samo na prvoj grupi pića.

Cene igara su prikazane na karticama u sekciji Aktivnosti. Minimum zakupa je 30 minuta; stoni fudbal se naplaćuje po 15 minuta, a pikado po kreditu. PS5 košta 300 din/sat sa 2 džojstika, odnosno 400 din/sat sa 4 džojstika.

## Otvoreno

Sadržaj koji treba potvrditi sa klubom:

- [ ] **Pomorandža i breskva** (200 din) su unete pod tim imenima kako ih je vlasnik naveo; ako su sokovi, vredi precizirati naziv
- [ ] **Zapremine** su poznate samo za piva (sva su 0,33 l); sokovi i ostala pića nemaju navedenu količinu, pa im u koloni „Jedinica" stoji `din / kom`

Tehnički dug (ništa blokirajuće):

- [ ] `assets/logo.png` je 448 KB, a prikazuje se na max 460px - vredi kompresovati
- [ ] Mapa u sekciji Lokacija je stilizovani placeholder (`.map-frame`), ne prava mapa. Dugme „Otvori u mapi" ipak vodi na ispravan Google Maps upit.

## SEO / link preview

Sajt je javan i indeksabilan. Nema `noindex` ni `[TEST]` prefiksa nigde.

Do 8.8.2026. je na `/` stajala privremena „Uskoro" stranica dok se čekale cene, a pun sajt je živeo na `/sajt.html` sa `noindex`. Oba su spojena u jedan `index.html`. Ako ikad zatreba, ta landing stranica i njeni stilovi stoje u git istoriji, u commitu pre onog koji ih je zamenio.

Apsolutni URL-ovi u `<head>`-u su vezani za `https://arcadebk.rs/`:

- `<link rel="canonical">`
- `og:url`
- `og:image` → `https://arcadebk.rs/assets/og-preview.jpg` (1200×630, dimenzije deklarisane preko `og:image:width/height`)

**Ako se domen ikad promeni, ova četiri mesta treba ažurirati.** Relativna `og:image` putanja ne radi - Viber, WhatsApp i Facebook zahtevaju apsolutan URL da bi prikazali preview.

Za link preview se koristi zasebna široka retrowave slika, pa je `twitter:card` podešen na `summary_large_image`. Originalni kvadratni logo ostaje favicon i logo u hero sekciji.

`robots.txt` dozvoljava pretraživačima pristup celom sajtu i navodi apsolutnu putanju do `sitemap.xml`. Sitemap sadrži samo kanonski URL `https://arcadebk.rs/`, jer je sajt single-page.

U `<head>` delu je dodat JSON-LD tipa `EntertainmentBusiness`, sa javnim podacima koji se već vide na stranici: naziv, opis, adresa, telefon, radno vreme, mapa, Instagram i logo. Formalni registracioni i poreski podaci nisu deo strukturiranih podataka.

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
| `≤600px` | Sve u jednu kolonu, nav se prelama u dva reda i centrira (ticker se krije), dugmad puna širina, redovi cenovnika se prelamaju u kartice (naziv + jedinica levo, cena desno) |
| `≤400px` | Hero naslov 36px, logo 130px, manji stat-ovi, nav na 9px |

Nav namerno **nema horizontalni scroll**. Ranije ga je imao, ali je Kontakt kao poslednja stavka ostajao van ekrana, a to je jedina stavka koja vodi ka rezervaciji. Sad se prelama u dva reda, pa su sve stavke uvek vidljive. Ako se ikad doda šesta stavka u nav, proveriti da i dalje staje u dva reda na 360px.

## Licenca / asseti

- Logo (`assets/logo.png`) je vlasništvo kluba Arcade BK.
- Fontovi su Google Fonts (besplatni za komercijalnu upotrebu).

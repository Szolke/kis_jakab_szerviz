# Kis-Jakab Zoltán Autószerviz – Projekt dokumentáció

## Projekt áttekintés

Egyoldalas bemutató weboldal egy szegedi autószerviznknek. Nincs backend, nincs build tool – egyszerű statikus HTML/CSS.

**Éles URL:** Cloudflare Pages-en fut (automatikus deploy a `main` branchről)  
**Elérhetőség:** +36 (30) 635 8159 · Szivárvány utca 5., Szeged, 6725

---

## Mappastruktúra

```
kis_jakab_szerviz/
├── index.html          # Egyetlen HTML oldal
├── css/
│   └── style.css       # Minden stílus itt van
├── images/
│   ├── hero-garage.jpg         # Hero háttérkép (Pexels #4489735, sötét garázs)
│   └── mechanic-workshop.jpg   # "Rólunk" szekció fotó (Pexels #8986105, kék overallos szerelő)
├── .gitignore
└── CLAUDE.md
```

---

## Design rendszer

### Színek (CSS változók, `style.css` tetején)

| Változó        | Érték     | Használat                  |
|----------------|-----------|----------------------------|
| `--blue`       | `#0a6fc2` | Gombok, linkek, ikonok     |
| `--blue-dark`  | `#084e8c` | Hover állapot              |
| `--blue-light` | `#e8f3fc` | Kártya háttér, hover bg    |
| `--accent`     | `#f0a500` | Sárga kiemelő, csillagok   |
| `--text`       | `#1a1a2e` | Fő szöveg                  |
| `--muted`      | `#5a6070` | Másodlagos szöveg          |
| `--border`     | `#d8e3ef` | Keretek                    |
| `--bg`         | `#f7f9fc` | Szekció háttér (világos)   |

### Betűtípusok (Google Fonts)

- **Barlow Condensed** (400/600/700/800) – Címek, nav, badge-ek
- **Barlow** (400/500/600) – Folyó szöveg, gombok

### Reszponzivitás

Töréspontok: `max-width: 680px` (mobil)  
Mobilverzión: nav menü elrejtve, egységes padding, képek stack-elve

---

## Szekciók

| Szekció         | HTML ID           | CSS osztályok                                    |
|-----------------|-------------------|--------------------------------------------------|
| Navigáció       | –                 | `nav`, `.nav-logo`, `.nav-links`                 |
| Hero            | –                 | `.hero`, `.hero-inner`, `.hero-stats`            |
| Szolgáltatások  | `#szolgaltatasok` | `.services-bg`, `.services-grid`, `.service-card`|
| Rólunk          | `#rolunk`         | `.why-layout`, `.why-grid`, `.why-image-wrap`    |
| Vélemények      | `#velemenyek`     | `.reviews-bg`, `.reviews-grid`                   |
| Nyitvatartás    | `#kapcsolat`      | `.hours-grid`                                    |
| CTA sáv         | –                 | `.contact-bg`                                    |
| Lábléc          | –                 | `footer`                                         |

---

## Komponensek

### Service kártyák (`.service-card`)

Minden kártya tartalmaz:
- **Bal oldali kék akcentcsík** (`border-left: 3px solid var(--blue)`) — hoverre `var(--accent)` sárgára vált
- **SVG ikon** a `.service-icon` div-ben (`color: var(--blue)`, `currentColor` stroke-kal)
- Cím (`.service-card h3`) és leíró szöveg

**Ha ikont cserélsz:** az `index.html`-ben a `.service-icon` div belsejébe tedd az új SVG-t. Inline SVG-t használunk (nincs külső fájl), `stroke="currentColor"` attribútummal — így a szín CSS-ből vezérelhető.

Aktuális ikonok és megfelelőik:

| Szolgáltatás              | Ikon típusa     |
|---------------------------|-----------------|
| Motor & Hajtáslánc        | csavarkulcs     |
| Felfüggesztés & Futómű    | kerék (küllős)  |
| Elektromos rendszerek     | villám          |
| Klíma szerviz             | hópehely        |
| Műszaki vizsgára felkész. | jelölőlap (✓)   |
| Olajcsere & Szűrők        | csepp           |

---

## Képek

A `images/` mappában tárolt képek Pexelről lettek letöltve (ingyenes, kereskedelmi használatra szabad).

| Fájl                    | Forrás                       | Pexels ID | Méret |
|-------------------------|------------------------------|-----------|-------|
| `hero-garage.jpg`       | Dimly lit industrial garage  | 4489735   | ~1920px wide |
| `mechanic-workshop.jpg` | Mechanic inspecting car      | 8986105   | ~800px wide  |

**Ha saját fotókat kapsz:** cseréld le ezeket a fájlokat ugyanolyan névvel – a CSS és HTML automatikusan felveszi.

**Ha új képet kell beilleszteni:**
- Hero háttér: `css/style.css`, `.hero` szabályon belül `url('../images/...')`
- HTML `<img>` elemek: `src="images/..."` (gyökérkönyvtártól relatív)

---

## Deployment

Cloudflare Pages automatikusan deployol a `main` branch minden pushánál. Nincs build parancs, a gyökér mappa kerül fel közvetlenül.

**Hogy deployolsz:**
```bash
git add .
git commit -m "Változtatás leírása"
git push origin main
```

---

## Lehetséges jövőbeli fejlesztések

- Hamburger menü mobilon (JS szükséges)
- Kapcsolatfelvételi form (Formspree vagy hasonló)
- Saját fotók beillesztése a stock képek helyett
- Google Maps beágyazás a nyitvatartás szekcióba
- Favicon hozzáadása

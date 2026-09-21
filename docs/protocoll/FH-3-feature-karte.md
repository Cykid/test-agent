# FH-3: Feature Karte — Protokoll

**Datum:** 2026-09-21
**Branch:** feature/FH-3-feature-karte
**Bearbeiter:** Agent (Claude Opus 4.7)

## Aufgabe

Erstellung einer modernen, produktbewerbenden HTML-Karte in der Mitte der
Seite. Die Karte enthält Bullet-Points und dreht sich per jQuery beim Hover.

## Durchgeführte Änderungen

- `index.html`
  - Titel auf „Focus HR — Feature Karte“ aktualisiert.
  - `<style>`-Block mit modernem, farbverlaufsbasiertem Design ergänzt.
    - Zentrierung der Karte über Flexbox auf `<body>` (`min-height: 100vh`).
    - Karten-Styling: abgerundete Ecken (20 px), sanfter Schatten,
      Farbverläufe im Badge, in den Feature-Icons und im CTA-Button.
    - Feature-Liste mit Häkchen-Icons via `::before`-Pseudo-Elementen.
    - `transform-style: preserve-3d` und `perspective: 1000px` für die
      Drehanimation.
  - Karten-Markup (`<article class="product-card">`) mit:
    - Badge „Neu“, Titel „Focus HR Pro“, Untertitel.
    - Vier Feature-Bullet-Points.
    - Preisanzeige.
    - Call-to-Action-Button „Jetzt kostenlos testen“.
  - `<script>`-Block am Seitenende:
    - `$(function () { … })` bindet Hover-Handler an die Karte.
    - `mouseenter` → `rotateY(360deg)`; `mouseleave` → `rotateY(0deg)`.
    - CSS-`transition` für 800 ms weiche Drehung.

## Akzeptanzkriterien-Abgleich

| Kriterium | Umsetzung |
|---|---|
| Karte in der Mitte | Body als Flex-Container, vertikal + horizontal zentriert. |
| Bullet-Points | Vier `<li>`-Einträge mit Häkchen-Design. |
| Modernes Design | Farbverlauf-Hintergrund, weiche Schatten, abgerundete Ecken, Badge, Pill-Preise, CTA. |
| jQuery Rotation bei Hover | `$('#productCard').on('mouseenter'/'mouseleave', …)` rotiert per `rotateY` um 360°. |

## Tests

- **Automatisierte Tests:** Keine im Repository vorhanden (reines statisches
  HTML-Projekt ohne Test-Framework). Es wurden keine neuen Tests eingeführt,
  weil das Projekt bisher keine Test-Infrastruktur besitzt.
- **Manuelle Prüfung:**
  - HTML-Struktur überprüft: alle öffnenden Tags haben schließende Gegenstücke
    (html, head, body, article, ul, li, div, span, button, style, script).
  - jQuery-CDN-Einbindung inkl. SRI-Hash unverändert übernommen.
  - Selektor `#productCard` und Klassennamen mit Markup abgeglichen.

## Statische Analyse

- Keine statischen Analysewerkzeuge konfiguriert (kein `package.json`,
  keine Linter). Ein Ad-hoc-HTML-Parser-Check per Python konnte in der
  Sandbox nicht ausgeführt werden (Permission).
- Manuelle Prüfung: Tag-Balance, Attributquoting und Semantik in Ordnung.

## Potenzielle Risiken

- **CDN-Abhängigkeit:** jQuery wird weiterhin per CDN geladen. Ohne
  Netzwerk oder bei CDN-Ausfall bleibt die Drehung aus (die Karte selbst
  bleibt sichtbar, da sie rein CSS-basiert dargestellt wird).
- **3D-Transform-Support:** Sehr alte Browser (< IE 10) unterstützen
  `rotateY`/`preserve-3d` nicht. Für moderne Browser (Chrome, Edge,
  Firefox, Safari) kein Problem.
- **Reduced Motion:** Die 360°-Drehung berücksichtigt `prefers-reduced-motion`
  nicht. Nutzer mit Bewegungsempfindlichkeit könnten die Rotation als
  störend empfinden.
- **Hover-only Interaktion:** Auf Touch-Geräten wird die Rotation nicht
  ausgelöst, da es keinen echten Hover gibt. Der Effekt ist rein dekorativ,
  daher tolerierbar.

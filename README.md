# Physics, Perfectly Explained

Interaktive, visuell hochwertige Erklärungen komplexer physikalischer Themen —
auf Master-Niveau, intuitiv statt auswendig. Reine statische Website, läuft
1:1 auf **GitHub Pages** (kein Build-Schritt, kein Backend, kein Tracking).

## Live

Nach dem Aktivieren von GitHub Pages (siehe unten):

- **Startseite / Themenübersicht:** `index.html`
- **Bloch-Kugel (Quantencomputing):** `topics/bloch-sphere.html`

## Projektstruktur

```
index.html              → Startseite (Hub): listet alle Themen als Karten
assets/
  theme.css             → geteiltes dunkles Theme (Farben, Typografie, Komponenten)
topics/
  bloch-sphere.html     → interaktive Bloch-Kugel (Three.js + KaTeX)
  _TEMPLATE.html        → Kopiervorlage für neue Themen
.nojekyll               → schaltet Jekyll ab, damit alles unverändert serviert wird
```

Jedes Thema ist eine eigenständige HTML-Datei unter `topics/`. Externe
Abhängigkeiten kommen ausschließlich per CDN:

- [Three.js](https://threejs.org/) `0.128.0` — 3D-Darstellung
- [KaTeX](https://katex.org/) `0.16.9` — Formelsatz

## Ein neues Thema hinzufügen

1. `topics/_TEMPLATE.html` kopieren, z. B. nach `topics/entanglement.html`.
2. Titel, Lead-Text und die `<section>`-Inhalte anpassen. Formeln als
   `<div class="formula" data-tex="...">` (Block) bzw.
   `<span data-tex-inline="...">` (inline).
3. In `index.html` die passende Themen-Karte von „coming soon“ auf einen
   echten Link umstellen: bei der `<div class="topic-card soon">` das
   `soon` entfernen und sie in ein `<a class="topic-card" href="topics/…">`
   verwandeln.

Das Aussehen kommt komplett aus `assets/theme.css` — dort zentral anpassen,
alle Seiten ziehen automatisch nach.

## GitHub Pages aktivieren

1. Änderungen auf den Standard-Branch (`main`) mergen.
2. Repo → **Settings → Pages**.
3. Unter **Build and deployment**: *Source* = **Deploy from a branch**,
   *Branch* = **`main`**, *Folder* = **`/ (root)`**, speichern.
4. Nach ein bis zwei Minuten ist die Seite unter
   `https://<user>.github.io/physics_perfectly_explained/` erreichbar.

Die Datei `.nojekyll` sorgt dafür, dass GitHub die Dateien unverändert
ausliefert (u. a. auch Pfade wie `topics/_TEMPLATE.html`).

## Konventionen (Bloch-Kugel)

Zustand nach Nielsen & Chuang:

```
|ψ⟩ = cos(θ/2)|0⟩ + e^{iφ} sin(θ/2)|1⟩
r   = (sinθ cosφ, sinθ sinφ, cosθ)
```

- `|0⟩` = Nordpol (+z), `|1⟩` = Südpol (−z)
- `|+⟩`/`|−⟩` = ±x, `|+i⟩`/`|−i⟩` = ±y
- Gates sind Rotationen der Kugel (Rechte-Hand-Regel, `R_n(θ)=e^{−iθ n·σ/2}`).

Die Gate-Zielzustände werden exakt über die 2×2-Matrizen berechnet; die
Animation dreht den Vektor per Quaternion um die jeweilige Gate-Achse.

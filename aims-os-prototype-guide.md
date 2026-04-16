# AIMS OS — PM Prototyping Guide
**Design System v1.0 — 2026-04-16**

> Este documento es el contexto de referencia para generar prototipos HTML consistentes con el AIMS OS Design System. Adjúntalo en Claude Code al inicio de cada sesión de prototyping.

---

## Cómo usar este documento

1. Abre Claude Code
2. Adjunta este archivo con `@aims-os-prototype-guide.md`
3. Pide el prototipo describiendo la vista que necesitas
4. Claude generará HTML usando solo clases y tokens de este DS

**Regla principal para Claude:** Usar únicamente las clases definidas en `aims-os-base.css` y los tokens CSS documentados aquí. No inventar clases, colores hex, o estilos inline que no vengan del DS.

---

## Setup

### Archivos requeridos en la misma carpeta
```
tu-prototipo.html
aims-os-base.css      ← todos los tokens + clases de componentes
```

### Head del HTML (copiar siempre)
```html
<link rel="stylesheet" href="aims-os-base.css">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.tailwindcss.com"></script>
<script>tailwind.config = { corePlugins: { preflight: false } }</script>
```

> **Usa `template.html` como punto de partida** — ya tiene el Layout Shell completo, la sidebar, el topbar, y los helpers de JS. Solo reemplaza el contenido de `<main class="main-content">`.

---

## Design Tokens

### App Background
```css
background: var(--color-app-bg);   /* #0a0a0f */
```

### Surface
| Token | Uso |
|---|---|
| `--color-surface-neutral-white` | Card background, panel bg |
| `--color-surface-neutral-default` | Hover states, input bg, chip bg |
| `--color-surface-neutral-subtle` | Subtle backgrounds |
| `--color-surface-neutral-emphasis` | Strong hover, selected bg |
| `--color-surface-primary-default` | Primary button, active indicator |
| `--color-surface-primary-subtle` | Active sidebar icon, primary tint |
| `--color-surface-primary-more-subtle` | Very light primary tint |
| `--color-surface-floating-default` | Dropdown / menu background |
| `--color-surface-success-subtle` | Success card/badge background |
| `--color-surface-error-subtle` | Error card/badge background |
| `--color-surface-alert-subtle` | Alert/warning background |
| `--color-surface-success-more-subtle` | Alert banner success bg |
| `--color-surface-error-more-subtle` | Alert banner error bg |

### Text
| Token | Uso |
|---|---|
| `--color-text-title` | Headings, values, primary text |
| `--color-text-subtitle` | Labels, secondary text |
| `--color-text-body` | Body copy, descriptions |
| `--color-text-label` | UI labels, list text |
| `--color-text-caption` | Small captions, placeholders |
| `--color-text-negative` | White text on dark/primary fills |
| `--color-text-disabled` | Disabled text |
| `--color-text-success` | Positive values, success messages |
| `--color-text-error` | Error messages, negative values |
| `--color-text-alert` | Warning messages |

### Border
| Token | Uso |
|---|---|
| `--color-border-neutral-lighter` | Card borders, dividers |
| `--color-border-neutral-default` | Input borders |
| `--color-border-primary-default` | Focus states, active borders |
| `--color-border-success-default` | Success input state |
| `--color-border-error-default` | Error input state |

### Icon
| Token | Uso |
|---|---|
| `--color-icon-neutral-dark` | Default icons (50% white) |
| `--color-icon-neutral-light` | Slightly brighter icons (70% white) |
| `--color-icon-primary-default` | Primary / blue icons |
| `--color-icon-success-default` | Success icons |
| `--color-icon-error-default` | Error icons |
| `--color-icon-alert-default` | Alert icons |

### Spacing
```
--spacing-3: 8px   --spacing-4: 12px  --spacing-5: 16px
--spacing-6: 20px  --spacing-7: 24px  --spacing-8: 32px
--spacing-9: 40px  --spacing-10: 48px
```

### Border Radius
```
--radius-sm: 4px   --radius-md: 8px   --radius-lg: 16px
--radius-xl: 24px  --radius-full: 9999px
```

---

## Typography Classes

```html
<h1 class="text-title-xl">Page Title</h1>          <!-- 32px / 600 -->
<h2 class="text-title-md">Section Title</h2>        <!-- 24px / 600 -->
<h3 class="text-title-sm">Card Title</h3>           <!-- 20px / 600 -->
<p  class="text-subtitle-md">Subtitle</p>           <!-- 16px / 500 -->
<p  class="text-body-md">Body text</p>              <!-- 14px / 400 -->
<p  class="text-label-md">Label</p>                 <!-- 12px / 500 -->
<p  class="text-caption-lg">Caption</p>             <!-- 12px / 400 -->
```

---

## Layout Shell

Use `template.html` as the base. The shell structure is:

```html
<div class="app-shell">
  <header class="topbar">...</header>
  <div class="app-body">
    <aside class="sidebar">...</aside>
    <main class="main-content">
      <!-- YOUR CONTENT HERE -->
    </main>
  </div>
</div>
```

**Dimensions:**
- Topbar: 100% × 48px
- Sidebar (collapsed): 80px wide
- Sidebar (expanded): 250px wide — add class `.expanded`
- Main content: padding `16px 24px`

---

## Components

### Buttons

```html
<!-- Primary -->
<button class="btn btn-primary btn-md">Label</button>

<!-- Secondary -->
<button class="btn btn-secondary btn-md">Label</button>

<!-- Tertiary -->
<button class="btn btn-tertiary btn-md">Label</button>

<!-- Warning -->
<button class="btn btn-warning btn-md">Label</button>

<!-- Success / Positive -->
<button class="btn btn-positive btn-md">Label</button>

<!-- Main Action (gradient) -->
<button class="btn btn-main-action btn-md btn-pill">Label</button>

<!-- Sizes: btn-sm (28px) · btn-md (40px) · btn-lg (48px) -->
<!-- Pill shape: add btn-pill -->
<!-- Icon button -->
<button class="btn-icon"><svg>...</svg></button>
<button class="btn-icon-sm"><svg>...</svg></button>
```

---

### Text Fields

```html
<div class="field">
  <label class="field-label">Email</label>
  <input class="input input-md" type="email" placeholder="Enter email" />
  <span class="field-support">Supporting text</span>
</div>

<!-- States: add class to .input -->
<!-- .error · .success · .alert · :disabled -->
<!-- Sizes: .input-md (40px) · .input-sm (32px) -->
```

---

### Menu / Dropdown

```html
<div class="menu">
  <div class="menu-item">
    <svg class="menu-icon">...</svg>
    <span class="menu-label">Option A</span>
  </div>
  <div class="menu-item active">
    <svg class="menu-icon">...</svg>
    <span class="menu-label">Option B (selected)</span>
  </div>
  <div class="menu-divider"></div>
  <div class="menu-item disabled">
    <span class="menu-label">Disabled option</span>
  </div>
</div>

<!-- Size S: use .menu-item-s instead of .menu-item -->
<!-- Max height 288px — add overflow-y-auto for scrollable lists -->
```

---

### Badge Status

```html
<span class="badge badge-active">Active</span>
<span class="badge badge-inactive">Inactive</span>
<span class="badge badge-error">Error</span>
<span class="badge badge-alert">Pending</span>
<span class="badge badge-primary">In Progress</span>
<span class="badge badge-draft">Draft</span>
```

---

### Tags / Filter Pills

```html
<span class="tag">All</span>
<span class="tag active">Active</span>
<span class="tag">
  Status
  <span class="tag-dismiss">×</span>
</span>
```

---

### Tabs

```html
<div class="tabs">
  <div class="tab-item active" onclick="switchTab(this)">
    All <span class="tab-count">128</span>
  </div>
  <div class="tab-item" onclick="switchTab(this)">
    Active <span class="tab-count">84</span>
  </div>
  <div class="tab-item" onclick="switchTab(this)">
    Pending <span class="tab-count">32</span>
  </div>
</div>
```

---

### Toggle

```html
<label class="toggle">
  <input type="checkbox" checked />
  <span class="toggle-track"></span>
  <span class="toggle-thumb"></span>
</label>
```

---

### Highlight Icon

```html
<!-- Size: highlight-icon-l (40px) · highlight-icon-m (32px) · highlight-icon-s (24px) -->
<!-- State variants: informative / success / alert / error / neutral / yellow / lime / purple / lightblue -->
<!-- Color: -dark (higher contrast) · default (lower contrast) -->

<div class="highlight-icon highlight-icon-l highlight-icon--informative-dark">
  <svg width="24" height="24">...</svg>
</div>

<div class="highlight-icon highlight-icon-l highlight-icon--success-dark">
  <svg width="24" height="24">...</svg>
</div>

<div class="highlight-icon highlight-icon-l highlight-icon--error-dark">
  <svg width="24" height="24">...</svg>
</div>
```

---

### Highlight Card (KPI)

```html
<!-- KPI row — 3 cards -->
<div class="flex items-stretch gap-3">

  <div class="highlight-card">
    <div class="highlight-card__row">
      <div class="flex flex-col gap-2">
        <span class="highlight-card__label">Total Contacts</span>
        <div class="flex items-baseline gap-2">
          <span class="highlight-card__value">1,284</span>
          <span class="highlight-card__unit">contacts</span>
        </div>
      </div>
      <div class="highlight-icon highlight-icon-l highlight-icon--informative-dark">
        <svg width="24" height="24">...</svg>
      </div>
    </div>
    <span class="highlight-card__feedback positive">↑ +12.4% vs last month</span>
  </div>

  <!-- BG variants: highlight-card--primary-bg · --green-bg · --orange-bg -->
  <!--              --yellow-bg · --purple-bg · --light-blue-bg · --lime-bg · --red-bg -->
</div>
```

---

### Card Container

```html
<div class="card">
  Content
</div>

<!-- States: .selected · .error · .pinned -->
```

---

### Table

```html
<div class="table-container">
  <table class="table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Status</th>
        <th>Date</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Sarah Lawrence</td>
        <td><span class="badge badge-active">Active</span></td>
        <td class="text-caption-lg">Apr 15, 2026</td>
      </tr>
      <tr class="selected">
        <td>Marcus Reid</td>
        <td><span class="badge badge-primary">In Progress</span></td>
        <td class="text-caption-lg">Apr 14, 2026</td>
      </tr>
    </tbody>
  </table>
  <!-- Pagination below table -->
  <div class="pagination" style="border-top: 1px solid var(--color-border-neutral-lighter);">
    <span class="pagination__rpp-label">Rows per page:</span>
    <div class="pagination__rpp-select">25 ▾</div>
    <span class="pagination__range">1 - 25 of 120 items</span>
    <nav class="pagination__nav">
      <button class="pagination__btn" disabled>‹</button>
      <button class="pagination__btn">›</button>
    </nav>
  </div>
</div>

<!-- Size S: add class .table-sm to <table> -->
```

---

### Alert Banner / Toast

```html
<!-- Inline banner -->
<div class="alert-banner alert-banner--error" role="alert">
  <svg class="alert-banner__icon">...</svg>
  <div class="alert-banner__body">
    <span class="alert-banner__title">Connection failed</span>
    <span class="alert-banner__desc">Check your connection and try again.</span>
  </div>
  <div class="alert-banner__actions">
    <button class="alert-banner__cta">Retry</button>
    <button class="alert-banner__close">×</button>
  </div>
</div>

<!-- Types: alert-banner--error · --success · --alert -->

<!-- Toast (floating) — call from JS -->
<script>showToast('Changes saved', 'success');</script>
```

---

### Tooltip

```html
<div class="tooltip-trigger">
  <button class="btn-icon-sm">...</button>
  <span class="tooltip tooltip--top">Edit record</span>
</div>

<!-- Positions: tooltip--top · --bottom · --left · --right -->
```

---

### Empty State

```html
<div class="empty-state">
  <div class="empty-state__content">
    <div class="highlight-icon highlight-icon-l highlight-icon--informative-dark mb-2">
      <svg width="24" height="24">...</svg>
    </div>
    <span class="empty-state__title">No results found</span>
    <span class="empty-state__desc">Try adjusting your filters or search terms.</span>
  </div>
  <div class="empty-state__actions">
    <button class="btn btn-primary btn-md">Add item</button>
    <button class="btn btn-secondary btn-md">Clear filters</button>
  </div>
</div>
```

---

### Modal Dialog

```html
<div class="modal-overlay">
  <div class="modal">
    <div class="modal__header">
      <h2 class="modal__title">Confirm action</h2>
      <button class="btn-icon-sm">×</button>
    </div>
    <div class="modal__body">
      Are you sure you want to delete this item? This action cannot be undone.
    </div>
    <div class="modal__footer">
      <button class="btn btn-secondary btn-md">Cancel</button>
      <button class="btn btn-primary btn-md">Delete</button>
    </div>
  </div>
</div>
```

---

### Slide Out Panel

```html
<div class="slide-out" id="slideOut">
  <div class="slide-out__header">
    <span class="slide-out__title">Detail view</span>
    <button class="btn-icon-sm" onclick="document.getElementById('slideOut').classList.remove('open')">×</button>
  </div>
  <div class="slide-out__body">
    <!-- Content -->
  </div>
  <div class="slide-out__footer">
    <button class="btn btn-secondary btn-md">Cancel</button>
    <button class="btn btn-primary btn-md">Save</button>
  </div>
</div>

<!-- Open: add class .open — <div class="slide-out open"> -->
<!-- Trigger: document.getElementById('slideOut').classList.add('open') -->
```

---

### Chat Box

```html
<div class="chat-box">
  <textarea class="chat-box__input" rows="1" placeholder="Ask anything..."></textarea>
  <div class="chat-box__toolbar">
    <div class="chat-box__tools">
      <button class="chat-box__tool-btn"><svg>...</svg></button>
      <div class="chat-box__mode">Auto ▾</div>
    </div>
    <button class="chat-box__send idle" disabled>
      <svg>...</svg>
    </button>
  </div>
</div>
<!-- Send button auto-activates when textarea has content (JS in template.html) -->
```

---

### Pagination Logic

```javascript
// State
let currentPage = 1;
const rowsPerPage = 25;
const totalResults = 120;

function renderPagination() {
  const totalPages = Math.ceil(totalResults / rowsPerPage);
  const start = (currentPage - 1) * rowsPerPage + 1;
  const end = Math.min(currentPage * rowsPerPage, totalResults);
  document.getElementById('pg-range').textContent = `${start} - ${end} of ${totalResults} items`;
  document.getElementById('pg-prev').disabled = currentPage === 1;
  document.getElementById('pg-next').disabled = currentPage === totalPages;
}

// Rules:
// - Hide pagination if totalResults <= rowsPerPage
// - Reset currentPage = 1 on filter/search change
// - Reset currentPage = 1 on rows-per-page change
```

---

## Utility Classes

```html
<!-- Status dots -->
<span class="status-dot active"></span>    <!-- green, pulsing glow -->
<span class="status-dot error"></span>     <!-- red -->
<span class="status-dot alert"></span>     <!-- yellow -->
<span class="status-dot inactive"></span>  <!-- gray -->

<!-- Progress bar -->
<div class="progress-bar">
  <div class="progress-bar__fill success" style="width: 75%"></div>
</div>
<!-- Fill variants: .success · .primary · .alert · .error -->

<!-- AI insight strip -->
<div class="ai-strip">
  <svg>...</svg>
  AI insight text goes here.
</div>

<!-- Divider -->
<div class="divider"></div>

<!-- Section label -->
<span class="section-title">Section Name</span>
```

---

## JS Helpers (incluidos en template.html)

```javascript
// Switch tabs
switchTab(element)

// Show toast
showToast('Message text', 'success')  // types: success · error · alert

// Toggle slide out
document.getElementById('slideOut').classList.add('open')
document.getElementById('slideOut').classList.remove('open')

// Toggle sidebar expanded
document.getElementById('sidebar').classList.toggle('expanded')
```

---

## Cómo documentar un componente nuevo

Si creas una vista con un componente que no existe en este DS, documéntalo así al final del HTML para que el designer pueda incorporarlo:

```html
<!--
  NEW COMPONENT: [Nombre del componente]
  Descripción: [Qué hace, en qué contexto se usa]
  Propiedades: [variantes, estados, tamaños]
  Tokens usados: [lista de --color-* que aplicaste]
  HTML:
  [pegar el HTML del componente nuevo aquí]
-->
```

---

## Ejemplos de prompts efectivos para Claude Code

```
"Usando el AIMS OS DS (adjunto), crea una vista de aprobaciones con:
- KPI row de 3 Highlight Cards (total/aprobados/pendientes)
- Tabs: Todos / Pendientes / Aprobados / Rechazados
- Tabla con columnas: Nombre, Tipo, Solicitante, Fecha, Estado
- Paginación de 25 items
- Empty state cuando no hay resultados"

"Crea una vista de detalle de Worker usando el template.html como base.
Debe tener un Slide Out panel con información del worker,
un Alert Banner de error si el worker está caído,
y un Chat Box en la parte inferior."

"Agrega a este prototipo un Modal de confirmación para eliminar un item,
con el overlay correcto y los botones Cancel / Delete del DS."
```

---

*AIMS OS Design System · Figma: v6rmYKA2zmyXWOahlxLOeI · Versión 1.0*

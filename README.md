# AIMS OS — Prototyping Kit

Kit para que los PMs generen prototipos HTML consistentes con el Design System usando Claude Code.

---

## Cómo usarlo

### Paso 1 — Abre Claude Code
Abre una sesión nueva en Claude Code (terminal o app).

### Paso 2 — Pega el System Prompt
Copia todo el contenido de `SYSTEM-PROMPT.md` y pégalo como primer mensaje antes de describir tu vista.

### Paso 3 — Describe la vista que necesitas
Ejemplo:
> "Crea una vista de Invoices con header, 3 KPI cards, filtros por estado y fecha, y una tabla con columnas: Invoice ID, Client, Amount, Due Date, Status. El botón principal es 'New invoice'."

### Paso 4 — Guarda el archivo HTML generado
Claude genera un archivo `.html`. Ábrelo en el browser para ver el resultado.

---

## Archivos del repo

| Archivo | Para qué |
|---|---|
| `prototype-reference.html` | **Referencia visual** — así debe verse una vista bien hecha. Tiene toggle dark/light. |
| `template.html` | Punto de partida vacío para prototipos nuevos |
| `aims-os-prototype-guide.md` | Referencia técnica de todos los componentes disponibles |
| `SYSTEM-PROMPT.md` | Prompt que los PMs pegan al inicio de cada sesión |
| `aims-os-base.css` | CSS del Design System (se carga automáticamente vía link) |

---

## Referencia visual

Antes de generar una vista, abre `prototype-reference.html` en el browser.
Tiene un toggle **Dark / Light** en el topbar para ver ambos modos.
Úsala para verificar que tu prototipo generado se vea similar.

---

## Cómo se carga el CSS

Los prototipos cargan el CSS directamente desde este repo:

```
https://raw.githack.com/cachilupis/aims-os-prototyping-/main/aims-os-base.css
```

**Eso significa:** cuando el Design System se actualiza y se hace push al repo, todos los prototipos existentes se actualizan automáticamente al recargar el browser. No necesitas hacer nada.

---

## Componentes disponibles

Ver `aims-os-prototype-guide.md` para la lista completa con ejemplos HTML.

Los más usados:
- Botones: `btn-main-action`, `btn-primary`, `btn-secondary`, `btn-tertiary`
- KPI Cards: `hcard` con variantes `--blue`, `--green`, `--yellow`, `--neutral`
- Tabla: `table-container` + `table`
- Badges: `badge-active`, `badge-inactive`, `badge-alert`, `badge-error`, `badge-primary`
- Filtros / Tags: `tag`, `tag.active`
- Tabs: `tabs` + `tab-item`
- Slide Out panel: `slide-out` + `slide-out.open`
- Alert Banner: `alert-banner--alert`, `--error`, `--success`
- Paginación: `pagination`

---

## Cuando el Design System se actualice

1. El diseñador corre una sesión con Claude Code
2. Claude extrae los nuevos valores de Figma y edita `aims-os-base.css`
3. `git push`
4. Todos los prototipos existentes se actualizan solos al recargar

**Tiempo estimado por update: 10–15 minutos.**

---

## Preguntas frecuentes

**¿Puedo usar Tailwind para estilos?**
Solo para layout: `flex`, `grid`, `gap-*`, `p-*`, `m-*`, `w-*`, `h-*`. Nunca para colores, tipografía o borders — esos siempre desde las clases del DS.

**¿Qué hago si necesito un componente que no existe en el DS?**
Construyelo con los tokens CSS del DS (`var(--color-*)`, `var(--radius-*)`) y usa el prefijo `custom-` en la clase. Documéntalo al final del HTML con un comentario marcado `NUEVO COMPONENTE`.

**¿El prototipo necesita funcionar en mobile?**
No. Los prototipos están diseñados para desktop (1440px). El DS es desktop-first.

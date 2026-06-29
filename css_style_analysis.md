# CSS Style Analysis for the Project

## 1. Global Design Overview
- **Design Philosophy**: Minimalist, performance‑oriented UI with a focus on animation and visual hierarchy.
- **Color System**: Relies on CSS custom properties (variables) defined in `:root` and overridden in dark‑mode media query.
- **Typography**: Uses system‑font stacks with `clamp()` for fluid sizing; `@font-face` for custom fonts (`Work Sans`, `Roboto Flex`).

## 2. Custom Properties (CSS Variables)
| Variable | Light Theme Value | Dark Theme Value | Usage Context |
|----------|-------------------|------------------|----------------|
| `--white` | `#fffffd` | `#aaa` | Backgrounds, text |
| `--black` | `#000` | `#000` | Text, borders |
| `--blue` | `#332e71` | `#44425d` | Primary UI elements |
| `--blue-dark` | `#201c4a` | `#2b2a3c` | Darker accents |
| `--pink` | `#f81d94` | `#b65f8e` | Highlight, links, hover |
| `--green` | `#3fe6c5` | `#71b4a7` | Success messages, accents |
| `--animated-h` | `100%` | `100%` | Height for animated elements |
| `--animated-p` | `absolute` | `absolute` | Positioning context |
| `--animated-b` | `1rem` | `1rem` | Bottom offset |
| `--animated-r` | `1rem` | `1rem` | Right offset |
| `--GRAD` | `0` | `-50` to `150` (via contrast media) | Font variation for `Roboto Flex` |

## 3. Keyframe Animations
| Name | Description | Properties Animated |
|------|-------------|----------------------|
| `draw` | Draws an SVG stroke from full to zero with opacity transition. | `stroke-dashoffset`, `opacity` |
| `move` | Horizontal slide‑in from left edge to full width. | `left`, `transform` |
| `auto` (implicit) | Used for elements with `animation: auto linear draw both;` – runs infinitely, linear timing. | `stroke-dasharray`, `stroke-dashoffset`, `opacity` |

## 4. Animation Usage Patterns
- **`.animated` class**: Applies `draw` animation; uses CSS variables for timing and size; includes `view-timeline-name` and `view-timeline-axis` for scroll‑linked animations.
- **`.tamer`**: Background image with `mix-blend-mode: hard-light;` and `filter: grayscale(100%);` for artistic overlay.
- **Responsive Adjustments**: Media queries adjust `--animated-h` at `min-width: 1200px` and control animation range (`entry 1% cover 10%`).

## 5. Layout & Utility Classes
| Class | Purpose | Typical Properties |
|-------|---------|--------------------|
| `.flex` | `display: flex;` | Flex container |
| `.justify-center` | `justify-content: center;` | Center items |
| `.items-center` | `align-items: center;` | Center items cross‑axis |
| `.flex-col` | `flex-direction: column;` | Column layout |
| `.h-full` | `height: 100dvh;` | Full viewport height |
| `.w-full` | `width: 100dvw;` | Full viewport width |
| `.block` | `display: block;` | Block display |
| `.container` | Max width & auto margin | `max-width: 1220px; margin: 0 auto;` |
| `.strong` | Color accent | `color: var(--pink);` |
| `.overflow-x` | `overflow-x: hidden;` | Hide horizontal overflow |
| `.relative` | `position: relative;` | Relative positioning |
| `.sticky` | `position: sticky;` | Sticky positioning |
| `.view-timeline-name`, `.view-timeline-axis` | View‑timeline hooks for scroll‑based animations |
| `.animated` | Core animation wrapper | `animation: auto linear draw both;` plus custom properties |

## 6. Media Queries & Dark Mode
- **Dark Mode**: Triggered by `prefers-color-scheme: dark`; swaps background, text, and accent variables.
- **Contrast Media**: `prefers-contrast: more` / `less` adjust `--GRAD` for `Roboto Flex` weight.
- **Resolution Queries**: `@media (min-width: 500px)`, `@media (min-width: 900px)`, `@media (min-width: 1200px)` adjust layout widths and animation parameters.

## 7. Specific Component Styles
### Horizon Section
- `.horizon`: Full‑height sticky container with `view-timeline-name` for scroll‑linked animations.
- `.horizon__container`: Holds the animated content; uses `animation: linear move forwards;`.
- `.horizon__item`: Padding and layout for each item.
- `.horizon__content`: Central alignment, width fitting content, animation tied to timeline.

### Skill / Experience Badges
- `.skill`, `.experience`: Relative positioned blocks with pseudo‑elements (`::before`, `::after`) creating decorative lines.
- Pseudo‑elements use `var(--pink)` or `var(--black)` for color theming.

### Themed Backgrounds
- `.black-green`, `.white-blue`, `.blue-green`, `.green-blue`: Utility classes that set `background-color` and `color` using the variable system.

## 8. Accessibility & Performance Considerations
- **Reduced Motion**: Not explicitly disabled; animations are linear and may be heavy on low‑end devices.
- **Color Contrast**: Variables are chosen to meet contrast ratios; additional contrast media queries adjust `--GRAD`.
- **Font Loading**: `@font-face` with `font-display: swap` ensures text remains visible during font load.

## 9. Summary of CSS Methodology
1. **Variable‑Driven Theming** – Centralized color definitions enable easy dark‑mode switching.
2. **Utility‑First Layout** – Small, composable classes (`.flex`, `.justify-center`, `.items-center`) for rapid UI composition.
3. **Scroll‑Linked Animations** – Leveraging `view-timeline-name` and `animation-range` for performant, context‑aware motion.
4. **Performance Optimizations** – `font-display: swap`, `clamp()` sizing, and limited use of heavy animations.
5. **Responsive Design** – Media queries adjust layout and animation parameters based on viewport width.

---  
*Document generated from `style.css` and inline `<style>` block in `index.html`.*
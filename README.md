# Papa John's · Prototipo AURUM

> Prototipo en vivo de **Papa John's Chile** (proyecto AURUM) · producto 3D editorial renderizado en tiempo real con **Three.js**.

![AURUM · forest green UI on white canvas](https://img.shields.io/badge/Three.js-r165-000?logo=three.js&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-035542)
![Status: live prototype](https://img.shields.io/badge/status-live%20prototype-56dddb)

---

## ✦ ¿Qué es?

Una experiencia scroll-driven de una sola página donde cada pizza del menú es una escena 3D en tiempo real. El canvas es blanco, la tipografía es **Work Sans 900** en formato billboard, los acentos son **verde bosque / amarillo mantequilla / teal crema**, y un cuchillo de chef se sumerge en cada pizza a medida que scrolleas.

Nació como propuesta creativa para Papa John's Chile — pero el código está estructurado como **starter reutilizable** para proyectos editoriales + 3D en web.

---

## ✦ Stack

| Layer        | Tool                                  |
|--------------|---------------------------------------|
| 3D rendering | [Three.js](https://threejs.org) r165+ · WebGL2 |
| Bundler      | [Vite](https://vitejs.dev) 5         |
| Typography   | Work Sans 900 (display) + JetBrains Mono (UI) |
| Color system | CSS custom properties — see `src/css/main.css` |
| Geometry     | `CylinderGeometry`, `InstancedMesh`, `MeshStandardMaterial` |

No frameworks, no UI library, no Tailwind. Plain HTML, plain CSS variables, plain ES modules.

---

## ✦ Estructura del proyecto

```
papa-johns-prototipo/
├── index.html               # Vite entry · all sections live here
├── package.json
├── vite.config.js
├── LICENSE                  # MIT
├── README.md
├── public/
│   └── favicon.svg          # AURUM mark
└── src/
    ├── main.js              # Entry · wires scene + pizzas + scroll + RAF loop
    ├── css/
    │   └── main.css         # All styles (design tokens + components)
    └── js/
        ├── scene.js         # Renderer, camera, lights, floor, knife
        ├── pizzas.js        # Pizza factory + PIZZAS catalog
        └── scroll.js        # ScrollController (active chapter + side rail)
```

Each JS module is small, single-purpose, and pure. The entry point in `main.js` is the only place that knows about the others.

---

## ✦ Getting started

```bash
# 1. Install
npm install

# 2. Dev server (hot reload, http://localhost:5173)
npm run dev

# 3. Production build → dist/
npm run build

# 4. Preview the build
npm run preview
```

Requires **Node 18+**.

---

## ✦ Adaptar este repo para un proyecto nuevo

El repo es intencionalmente un **template**. Aquí va el camino de remix en 5 minutos:

### 1. Swap the catalog

Edit `src/js/pizzas.js` — change the `PIZZAS` array. Each entry maps 1:1 to a `<section class="chapter" data-pizza="N">` in `index.html`.

```js
export const PIZZAS = [
  { name: 'Your Product 1', radius: 1.0, toppings: [/* ... */] },
  { name: 'Your Product 2', radius: 1.0, toppings: [/* ... */] },
];
```

You can also rewrite `makePizza()` to build any other disc / sphere / box-based object — shoes, watches, bottles, anything.

### 2. Edit the sections

In `index.html`, each pizza chapter is just a section with:

```html
<section class="chapter" data-pizza="0">
  <span class="bg-word">YOUR LABEL</span>
  <div class="content">
    <div class="chapter-tag">…</div>
    <h2 class="chapter-name">Title <em>highlight</em></h2>
    <p class="chapter-desc">…</p>
    <div class="chapter-price">PRICE · <b>$0</b></div>
  </div>
</section>
```

The `bg-word` is the huge billboard text behind the content. Use `.yellow` or `.teal` modifiers to switch its color.

### 3. Recolor the system

Every color is a CSS variable in `src/css/main.css` → `:root`:

```css
:root {
  --forest:        #035542;   /* primary brand */
  --forest-press:  #024235;   /* hover / pressed */
  --billboard-blue:#2b7bb9;   /* secondary accent */
  --cream-teal:    #56dddb;   /* highlight */
  --butter-yellow: #f9e9a9;   /* highlight */
  --charcoal:      #333333;   /* body text */
  --paper:         #ffffff;   /* canvas */
  --line:          #e8e6df;   /* hairline */
}
```

Change five values → whole site re-skins.

### 4. Tune the scene

In `src/js/scene.js`:

- **Camera angle / FOV** — `PerspectiveCamera(35, …)` and `camera.position.set(0, 1.6, 5.2)`.
- **Lighting** — three lights (key, fill, back) tuned for high-key product photography. Add or remove freely.
- **Floor disc** — drop or restyle for a different background.
- **Knife** — the `buildKnife()` prop is a placeholder. Replace it with anything that should "interact" with the active scene.

### 5. Tune the scroll behavior

`src/js/scroll.js` exposes a `ScrollController` with a `getInViewProgress()` method (0..1 of how centered the active chapter is). In `main.js` we use it to dip the knife — swap in any animation you want.

---

## ✦ How the prototype works

1. All pizzas are built once and laid out along the **+X axis** at `PIZZA_SPACING` (3.5) units apart.
2. A `ScrollController` watches the seven `<section class="chapter">` elements and figures out which one is centered in the viewport.
3. The render loop smoothly translates `pizzaGroup.position.x` toward `-currentIndex * PIZZA_SPACING` so the active pizza lines up with the camera.
4. The knife (a `THREE.Group` with blade + tip + handle) follows the active pizza and dips as the chapter centers (`knifeY = 1.8 - progress * 2.0`).
5. The active pizza gets a gentle `sin(t * 1.2)` hover and slow `rotation.y` to feel "alive".

---

## ✦ Notas de performance

- **InstancedMesh** for every topping class — even 8 toppings × 20 instances stay at one draw call.
- **Pixel ratio capped at 2** to keep mobile retina sane.
- **No post-processing** in this build; the look comes from materials + lighting, not bloom. Add `EffectComposer` later if you want it.
- **Lazy scenes** are a good next step — only build the upcoming pizza when within N sections.

Target: 60fps on desktop, 50–60fps on a recent phone.

---

## ✦ Compatibilidad de navegadores

- WebGL2 required (every modern browser since 2017).
- ES modules + import maps via Vite (so modern only — IE is dead anyway).
- Tested on latest Chrome, Safari, Firefox, Edge.

---

## ✦ Licencia

MIT — ver [LICENSE](./LICENSE). Úsalo, forkealo, publícalo.

---

## ✦ Créditos

- Tipografía — [Work Sans](https://fonts.google.com/specimen/Work+Sans) (OFL) · [JetBrains Mono](https://www.jetbrains.com/lp/mono/) (OFL)
- Motor 3D — [Three.js](https://threejs.org) (MIT)
- Tooling — [Vite](https://vitejs.dev) (MIT)
- Marca & producto — Papa John's Chile

Construido como propuesta creativa de equipo senior, luego publicado como starter.

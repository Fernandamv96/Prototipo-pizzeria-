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



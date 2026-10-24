# AURUM · Prototipo 3D para una pizzería

[![Demo en vivo](https://img.shields.io/badge/demo-en%20vivo-035542)](https://fernandamv96.github.io/Prototipo-pizzeria-/)
![Three.js](https://img.shields.io/badge/Three.js-r165-000?logo=three.js&logoColor=white)
![HTML, CSS y JS](https://img.shields.io/badge/HTML%20%C2%B7%20CSS%20%C2%B7%20JS-sin%20build-56dddb)
[![Licencia: MIT](https://img.shields.io/badge/licencia-MIT-035542)](LICENSE)

Propuesta de rediseño web en la que cada pizza del menú es una escena 3D en tiempo real. El canvas es blanco y la tipografía es Work Sans 900 en formato *billboard*, con acentos verde bosque, amarillo mantequilla y teal crema.

**[▶ Ver demo en vivo](https://fernandamv96.github.io/Prototipo-pizzeria-/)**

> **Aviso:** es un proyecto académico y de portafolio, una propuesta conceptual sin afiliación con Papa John's ni con ninguna otra marca. Los nombres y marcas mencionados pertenecen a sus dueños.

## Páginas

| Archivo | Qué muestra |
| --- | --- |
| [`demo.html`](demo.html) | Prototipo principal: recorrido con *scroll* por el menú, con escenas 3D en Three.js |
| [`slider.html`](slider.html) | Carrusel *coverflow* 3D de pizzas |
| [`propuesta.html`](propuesta.html) | Documento de la propuesta de rediseño: concepto, paleta y tipografía |
| [`index.html`](index.html) | Redirige a la demo |

## Tecnologías

- **Three.js r165**, cargado como módulo ES desde unpkg: `CylinderGeometry`, `InstancedMesh` y `MeshStandardMaterial`.
- **HTML, CSS y JavaScript sin frameworks**: variables CSS para la paleta y módulos ES nativos.
- **GitHub Pages** con GitHub Actions: cada *push* a `main` publica el sitio tal cual, sin paso de build.

## Ejecutar en local

Las páginas son estáticas, pero los módulos ES necesitan un servidor (no funcionan con `file://`):

```bash
npx serve .          # o: python -m http.server 8000
```

Luego abre `http://localhost:3000/demo.html` (o el puerto que indique la herramienta).

## Licencia

[MIT](LICENSE) © Fernanda (Fernandamv96)

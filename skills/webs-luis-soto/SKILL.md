---
name: webs-luis-soto
description: Úsala al crear, rediseñar o dar movimiento a cualquier web de Luis Soto (Galicia XXI, Guláns, Acivro, SotoFlauta, Cecilia, bodas, Fisión, etc.). Aplica los criterios de animación de Emil Kowalski.
---

# Webs de Luis Soto con los criterios de Emil Kowalski

Guía para que todas las webs de Luis Soto tengan movimiento vivo pero profesional. Resume las skills de Emil Kowalski (github.com/emilkowalski/skills: emil-design-eng, animate, review-animations) y añade las convenciones de las webs de Luis.

## 1. Antes de animar algo, decide

| Frecuencia con que se ve | Decisión |
| --- | --- |
| Cientos de veces al día (atajos de teclado) | Sin animación |
| Decenas de veces (hover, listas) | Muy reducida o ninguna |
| Ocasional (visores, menús, hojas, avisos) | Animación estándar |
| Rara o primera vez (portada, entrada de la página) | Se puede lucir |

- Toda animación necesita un motivo: continuidad espacial, indicar un estado, explicar, dar respuesta al gesto o evitar un cambio brusco. «Queda bonito» no basta si se ve a menudo.
- Nunca se anima lo que se hace con el teclado (pasar fotos con las flechas, por ejemplo): el cambio es inmediato.

## 2. Curvas y duraciones

```css
--ease-out: cubic-bezier(0.23, 1, 0.32, 1);      /* entradas y salidas */
--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);  /* movimiento en pantalla */
--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);   /* hojas tipo iOS */
```

- Entra o sale: `ease-out`. Se mueve en pantalla: `ease-in-out`. Color o hover: `ease`. Movimiento continuo (cintas, progreso): `linear`. Nunca `ease-in` en la interfaz.
- Pulsar un botón: 100–160 ms. Menús y desplegables: 150–250 ms. Visores y hojas: 200–500 ms. La interfaz, por debajo de 300 ms. Las piezas de portada o explicativas pueden durar más.
- La salida, más rápida que la entrada.

## 3. Recetas

- **Botones**: `transition: transform 160ms var(--ease-out)` y `transform: scale(0.97)` en `:active`. Vale para todo lo que se pulsa.
- **Nada aparece de la nada**: nunca `scale(0)`. Se parte de `scale(0.95)` con `opacity: 0`.
- **Visor de fotos (modal)**: centrado, entra con opacidad y `scale(0.96)` en 250 ms. Usar `<dialog closedby="any">` con `showModal()` y un respaldo para Safari que cierre al pulsar fuera.
- **Hojas en móvil**: suben con `translateY(100%)` a `0` y `--ease-drawer`. Se cierran arrastrando: si la velocidad (`distancia / ms`) pasa de 0,11, se cierra aunque el recorrido sea corto. Por encima del tope, amortiguar en vez de frenar en seco. Capturar el puntero al empezar a arrastrar.
- **Listas que entran**: escalonar de 30 a 80 ms entre elementos, sin bloquear la interacción.
- **Aparecer al bajar**: solo en zonas de presentación y una sola vez (`IntersectionObserver`). Con `clip-path: inset(0 0 100% 0)` a `inset(0 0 0 0)` queda muy fino en fotos.
- **Pestañas con el color exacto**: duplicar la fila de pestañas con el estilo activo y recortarla con `clip-path` hacia la pestaña elegida.
- **Cambios que no encajan**: un `filter: blur(2–3px)` breve durante la transición une los dos estados.
- **Seguir al ratón**: siempre con un resorte (velocidad y amortiguación), nunca pegado directamente al puntero. Solo es decorativo.
- **Transiciones antes que keyframes** para lo que el usuario puede interrumpir. Keyframes solo para lo predeterminado: entradas, cintas o giros.

## 4. Rendimiento

- Animar solo `transform` y `opacity` (y `clip-path`).
- No mover hijos con una variable CSS del padre: aplicar el `transform` en el propio elemento.
- CSS para lo predeterminado y Web Animations API (`el.animate`) para lo programado. No hacen falta librerías.
- Los canvas animados se detienen cuando salen de pantalla.

## 5. Accesibilidad

- `prefers-reduced-motion: reduce`: quitar desplazamientos y giros, y mantener los cambios de opacidad y color que ayudan a entender.
- Hover con movimiento solo dentro de `@media (hover: hover) and (pointer: fine)`.
- Todo lo que se mueve solo (pases de fotos, cintas, logotipos que giran) lleva botón de pausa, y la elección se recuerda.
- Foco visible y objetivos táctiles de 44 px o más en móvil.

## 6. Convenciones de las webs de Luis

- **Nombre**: siempre «Luis Soto», sin tilde.
- **Idiomas**: gallego (por defecto), castellano e inglés, con selector GL / ES / EN y la elección recordada.
- **Colores**: selector de paletas (en Galicia XXI son cuatro: Sargadelos, Retablo, Camelia y Atlántico). Todos los colores como variables, con tema claro y oscuro. El cambio de paleta se hace con una transición circular de View Transitions desde el botón pulsado.
- **Móvil e iPad**: además del diseño adaptable, una página `movil.html` tipo app (pestañas abajo, carrusel, reproductor en hoja). `index.html` la abre sola en pantallas táctiles de hasta 1024 px, salvo que se pida la versión de escritorio.
- **Entrega para el servidor**: un único zip con `index.html`, `movil.html`, los `.js` compartidos y las carpetas `fotos/` y `audio/`, más un `LEME.txt` con instrucciones. Además, publicar la versión de un solo archivo en el enlace del artefacto.
- **Tipografía**: evitar Inter, Space Grotesk y Roboto. Una de presentación con carácter y otra de lectura, de Google Fonts y con respaldo.
- **Nada de aspecto «hecho con IA»**: sin emojis como marcadores, sin degradados violeta, sin etiquetas en mayúsculas sobre cada título y sin flechas «→» en los enlaces.

## 7. Revisión final (formato obligatorio)

Al revisar una web, presentar los cambios en una tabla:

| Antes | Después | Por qué |
| --- | --- | --- |
| `transition: all 300ms` | `transition: transform 200ms var(--ease-out)` | Propiedades concretas, nunca `all` |
| Entrada con `scale(0)` | `scale(0.95)` y `opacity: 0` | Nada aparece de la nada |
| Hover que se mueve sin condición | Dentro de `(hover: hover) and (pointer: fine)` | En táctil el hover salta al tocar |

Lista de comprobación: sin `transition: all`, sin `ease-in`, sin `scale(0)`, interfaz por debajo de 300 ms, hover condicionado, movimiento reducido respetado, pausa en lo automático, solo `transform` y `opacity`, nada animado desde el teclado, listas escalonadas.

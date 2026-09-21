# Catálogo — lo que sabemos de cada prenda

Se va llenando según llegan fotos. Las que vienen del Shopify están marcadas
como tal; las que vienen de foto propia tienen los archivos en
`assets/garments/`.

---

## Hallazgo de marca: qué significa "WiP?"

**WiP? = "What is Peace?"**

La camiseta gris lo deja escrito entero en el pecho. Es la clave de toda la
línea "WiP?" — Black Stone, White Bones, Pure Water, Cotton Candy, Greek
Stone. No son siglas sueltas: cada camiseta de esa serie hace la misma
pregunta en un color distinto.

Esto conviene que salga en la web en algún sitio, porque ahora mismo "WiP?"
no se entiende si no tienes la prenda en la mano.

**Confirmado con la segunda muestra**: la gris y la azul son *el mismo diseño*
— misma frase, mismas tres palomas en la misma posición, mismo logo detrás,
mismas etiquetas. Lo único que cambia es el color de la tela. Así que la línea
WiP? no son cinco camisetas distintas: es una pregunta estampada en cinco
colores. Eso es un argumento fuerte para enseñarlas juntas en la web, en la
misma burra, y no repartidas.

---

## Identidad visual confirmada

| Elemento | Qué es |
|---|---|
| **El logo** | Cuatrifolio **hueco** (no macizo) atravesado por una cruz, con una púa curvada metida en cada uno de los cuatro paños. Ancho: relación 400 × 259. |
| **Etiqueta de cuello** | `clout native`, en minúsculas, sans, sobre etiqueta blanca. |
| **Etiqueta de manga** | El logo en negro sobre etiqueta blanca, manga derecha. |
| **Tipografía de estampado** | Serif de contraste alto en minúsculas (la de "what is peace?"). Distinta de la Outfit que usa el Shopify. |
| **Las palomas** | Tres siluetas negras, siempre en la misma posición: una arriba a la izquierda, dos cruzando la frase. |

El logo de la web está **trazado de la foto de una espalda**, umbralizado y
convertido a vector. Va en `MARK_D` dentro de `index.html`.

Se trazaron las dos espaldas por separado, la gris y la azul, y **salen la
misma forma** — eso confirma que el trazado es fiel y no un artefacto de una
foto concreta. Se usa el de la azul, que tiene el estampado más limpio y más
contraste contra la tela. Si aparece el vector original sigue siendo mejor: se
cambia esa sola constante.

---

## Prendas

### "What is Peace?" — gris jaspeado

- **Fotos**: `assets/garments/what-is-peace-grey-front.jpg` / `-back.jpg`
- **Color**: gris jaspeado (heather grey)
- **Delante**: `what is peace?` en serif minúscula, atravesado por **tres
  palomas** negras en silueta. Una de ellas tapa parte de la palabra "peace",
  así que se lee `what is p▮ce?` — la paloma es la paz.
- **Detrás**: el logo grande, centrado, en negro plano.
- **Cuello**: etiqueta `clout native`.
- **Manga**: etiqueta con el logo.
- **Corte**: caja, manga corta, hombro caído leve.

- **Color de tela**: gris jaspeado, muestreado de la foto → **`#787675`**

**Handle probable**: *Greek Stone "WiP?" T-shirt* (39,99 €) — piedra griega,
gris. Pero *White Bones* también podría ser un gris claro. **Sin confirmar**,
y con menos seguridad que la azul.

### "What is Peace?" — azul claro

- **Fotos**: `assets/garments/what-is-peace-blue-front.jpg` / `-back.jpg`
- **Color de tela**: azul cielo pálido, muestreado de la foto → **`#c7d5dd`**
- **Diseño**: idéntico al de la gris. Delante `what is p▮ce?` con las tres
  palomas, detrás el logo grande, etiqueta `clout native` al cuello y etiqueta
  con logo en la manga derecha.

**Handle probable**: *Pure Water "WiP?" T-shirt* (39,99 €). El azul agua encaja
con el nombre y es el único azul de la serie. **Sin confirmar.**

---

## Colores de tela medidos

Muestreados de las fotos, sobre la cara iluminada del tejido. Sirven para la
web (las siluetas de la previsualización, y de referencia para los ambientes).

| Prenda | Color |
|---|---|
| "What is Peace?" gris jaspeado | `#787675` |
| "What is Peace?" azul claro | `#c7d5dd` |

---

## Del Shopify (sin foto propia todavía)

Precio y nombre salen del sitio actual; las fotos se cargan de su CDN.

| Prenda | Precio | Estado |
|---|---|---|
| Black Stone "WiP?" T-shirt | 39,99 € | — |
| White Bones "WiP?" T-shirt | 39,99 € | — |
| Pure Water "WiP?" T-shirt | 39,99 € | — |
| Cotton Candy "WiP?" T-shirt | 39,99 € | — |
| Greek Stone "WiP?" T-shirt | 39,99 € | — |
| "Sweet Lemon" Hoodie | 64,99 € | Agotado |
| "Sweet Lemon" Pants | 64,99 € | — |
| "YCSFPOTD" Hoodie | 64,99 € | — |
| "YCSFPOTD" Pants | 64,99 € | — |
| Native Magnolia Shirt | 35,00 € | Edición exclusiva |
| Native Life in Flowers Shirt | 35,00 € | Edición exclusiva |

**Pendiente**: "YCSFPOTD" tampoco está descifrado. Si es otra frase como
"WiP?", merece el mismo trato en la web.

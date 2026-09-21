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

**Confirmado con las cinco**: la gris, la azul y la negra son *el mismo diseño*
— misma frase, mismas tres palomas en la misma posición, mismo logo detrás,
mismas etiquetas. Lo único que cambia es el color de la tela, y en la negra
la tinta se invierte a blanco (etiqueta de manga incluida). Así que la línea
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

Se trazaron **las espaldas por separado** — gris, azul y negra — y salen la
misma forma. La rosa se comprobó contra la adoptada y coincide dentro del
mismo margen que las otras entre sí (4,4 % de píxeles), así que confirma sin
aportar nada nuevo. Eso confirma que el trazado es fiel y no un artefacto de una
foto concreta.

Se usa **el de la negra**: tinta blanca sobre tela negra es el mayor contraste
de los tres, y el estampado es el más nítido.

Probé también a promediar las tres (normalizar al mismo marco y votar píxel a
píxel) esperando cancelar la distorsión de cada prenda. **Salió peor**: las
diferencias entre prendas no son ruido aleatorio sino el estirado propio de
cada tela, así que promediarlas no las cancela, las mezcla — y el resultado
tiene las curvas más temblorosas que la mejor muestra sola. Queda anotado para
no repetirlo.

Si aparece el vector original sigue siendo mejor: se cambia `MARK_D` y ya.

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

### "What is Peace?" — negra

- **Fotos**: `assets/garments/what-is-peace-black-front.jpg` / `-back.jpg`
- **Color de tela**: negro con una gota de azul → **`#0f0e13`**
- **Diseño**: el mismo, con la tinta **invertida a blanco** — delante la frase
  y las palomas en blanco, detrás el logo blanco. La etiqueta de manga
  también se invierte: fondo blanco, logo negro.
- Es la muestra que mejor define el logo de las tres.

**Handle probable**: *Black Stone "WiP?" T-shirt* (39,99 €). Es el único negro
de la serie. **Casi seguro**, pero sin confirmar.

### "What is Peace?" — rosa

- **Fotos**: `assets/garments/what-is-peace-pink-front.jpg` / `-back.jpg`
- **Color de tela**: rosa empolvado → **`#cfa7b5`**. Más apagado de lo que
  parece de lejos: los claros de la foto son reflejo, no tela.
- **Diseño**: el mismo, tinta negra.
- **Ojo con estas dos fotos**: vienen a ~850 px de lado, no a 2000 como las
  demás. Valen para el catálogo pero **no para la web** — si hay originales
  más grandes, mejor.

**Handle probable**: *Cotton Candy "WiP?" T-shirt* (39,99 €). Es el único rosa
de la serie. **Casi seguro**, sin confirmar.

### "What is Peace?" — hueso

- **Fotos**: `assets/garments/what-is-peace-bone-front.jpg` / `-back.jpg`
- **Color de tela**: crema hueso, con un punto verdoso → **`#c8c8b4`**
- **Diseño**: el mismo, tinta negra.
- **Estado**: es la más gastada de las cinco. El estampado tiene **grietas y
  desgaste** visibles, y la tela está arrugada. Al comparar su logo con el
  adoptado difiere un 12 % de píxeles — el triple que las demás (4–6 %). Eso
  **no** es una variante del logo: es la tinta rota. Dato de la prenda.

**Handle**: *White Bones "WiP?" T-shirt* (39,99 €). Hueso, y es la única
crema de la serie.

---

## La serie WiP? está completa

Cinco camisetas, una pregunta:

| Color | Prenda | Tela |
|---|---|---|
| Hueso | White Bones | `#c8c8b4` |
| Azul claro | Pure Water | `#c7d5dd` |
| Gris jaspeado | Greek Stone | `#787675` |
| Negro | Black Stone | `#0f0e13` |
| Rosa | Cotton Candy | `#cfa7b5` |

Con la hueso cerrada, **la gris deja de ser ambigua**: es Greek Stone. Antes
dudaba entre esa y White Bones.

La única que invierte la tinta es la negra: blanco sobre negro, etiqueta de
manga incluida.

---

## Cómo quedan repartidas las salas

Las cinco WiP? cuelgan **juntas en la sala Peace**, no repartidas por color
como estaban. El motivo sale de la propia prenda: la frase del pecho es
*"what is peace?"*, así que esa serie **es** la pregunta de la sala. No hacía
falta inventar un criterio, lo llevan escrito.

| Sala | Colección | Qué cuelga |
|---|---|---|
| 1 · Peace | Las cinco WiP? | White Bones, Pure Water, Greek Stone / Black Stone, Cotton Candy |
| 2 · Mystery | YCSFPOTD | Sudadera y pantalón. Dos piezas y mucho aire: la sala que no enseña lo que guarda. |
| 3 · Nostalgia | Sweet Lemon + ediciones Native | Sudadera y pantalón Sweet Lemon / Magnolia y Life in Flowers |

---

## Una cosa de las fotos, no de la ropa

En la gris, la azul y la rosa aparecen manchas claras en el torso, siempre en
el mismo sitio. En la negra no. Que se repitan en la misma posición apunta a
**reflejo del foco al fotografiar**, no a desgaste de la prenda. Si en algún
momento se vuelven a tirar las fotos, merece la pena difuminar más esa luz:
ahora mismo se comen el color real de la tela y obligan a estimarlo.

---

## Colores de tela medidos

Muestreados de las fotos, sobre la cara iluminada del tejido. Sirven para la
web (las siluetas de la previsualización, y de referencia para los ambientes).

| Prenda | Color |
|---|---|
| "What is Peace?" gris jaspeado | `#787675` |
| "What is Peace?" azul claro | `#c7d5dd` |
| "What is Peace?" negra | `#0f0e13` |
| "What is Peace?" rosa | `#cfa7b5` |

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

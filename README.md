# Ziad Addami — Portfolio

Static one-page portfolio. No build step: open `index.html` in a browser.

## Imagen principal (hero)

La foto del hero ya no va incrustada en el HTML. Se carga desde:

    assets/hero.jpg

Para cambiarla, basta con dejar el archivo nuevo en esa ruta con ese nombre.
Mientras no exista, el hero muestra un marco de placeholder en lugar de una
imagen rota.

Recomendaciones para el archivo:

- Vertical o cuadrada, con el sujeto centrado (se escala a la altura completa).
- Lado largo de 2000–2600 px.
- JPG de calidad alta, por debajo de ~600 KB.
- El filtro en blanco y negro y el degradado de los bordes se aplican por CSS,
  así que la imagen puede subirse a color y sin recortar.

Si el archivo final es PNG o WebP, hay que actualizar la ruta del `<img class="hero-photo">`
en `index.html`.

## Estructura

Una sola pantalla, sin scroll: una sala en 3D donde los paneles de tus
imagenes derivan hacia el espectador, y encima un marco plano y fijo — el
wordmark a sangre, la lista de proyectos, las disciplinas y el indice.
Cada entrada abre una hoja superpuesta que se cierra con `Close` o `Esc`.

### Imagenes

El hero ya no lleva foto propia: la sala es el fondo. Las imagenes van todas
en `assets/work/`, numeradas `<proyecto>-<fotograma>`:

    assets/work/01-01.jpg   ← proyecto 1, primera imagen
    assets/work/02-03.jpg   ← proyecto 2, tercera imagen

Cada imagen aparece en tres sitios a la vez: como panel flotando en la sala,
en la retícula de su proyecto y en el indice general. Las que falten se
quedan como panel vacio, asi que se pueden anadir de una en una.

### Proyectos

Se declaran al principio del `<script>` de `index.html`:

    { name: '...', kind: 'Product', year: '2026', frames: 4,
      disciplines: ['Research', 'Concept', 'CMF', 'Prototype'],
      desc: '...' }

`frames` decide cuantos paneles aporta a la sala. `disciplines` alimenta
tanto la ficha del proyecto como la lista grande en verde de la portada,
que se construye sola con el conjunto de todas sin repetir.

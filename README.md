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

Una sola pantalla, sin scroll. El fondo es **el estudio**: una escena en 3D
construida con cajas de CSS, donde cada mueble es uno de los proyectos.
Encima va un marco plano y fijo con el wordmark, las listas y el reloj.

Cada mueble es un boton: al pasar por encima se enciende a la vez que su
linea en la lista de la izquierda, y al pulsarlo abre su hoja. La hoja se
cierra con `Close` o con `Esc`.

### La escena

Las coordenadas van en el espacio de la escena: x a la derecha, y hacia
abajo (asi que arriba es negativo) y z hacia el espectador, con el suelo en
y = 0. Cada pieza se coloca directamente en esas coordenadas dentro del
`<script>`.

Las caras no tienen luces: se sombrean por orientacion con un `brightness`
constante — la superior recibe mas, las laterales menos, la trasera casi
nada. Las dos unicas cosas que emiten en vez de reflejar son la pantalla del
MacBook y la cara inferior de la pantalla de la lampara.

El MacBook es atrezo, no proyecto: no se puede pulsar.

### Proyectos e imagenes

Se declaran al principio del `<script>`:

    { name: 'Desk', kind: 'Furniture', year: '2026', frames: 3, piece: 'desk',
      disciplines: ['Research', 'Structure', 'Joinery', 'Prototype'],
      desc: '...' }

`frames` decide cuantas imagenes tiene el proyecto. Van en `assets/work/`,
numeradas `<proyecto>-<fotograma>`:

    assets/work/01-01.jpg   ← Desk, primera imagen
    assets/work/03-02.jpg   ← Lamp, segunda imagen

Aparecen en la reticula de su proyecto y en el indice general. Las que
falten se quedan como hueco rayado.

`disciplines` alimenta la ficha del proyecto y tambien la lista grande en
rosa de la portada, que se construye sola con el conjunto de todas sin
repetir.

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

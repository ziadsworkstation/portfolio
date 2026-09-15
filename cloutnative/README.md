# Clout Native — the sky

No es una tienda, es un portal. Entras por dentro de una nube, la atraviesas,
y sales sobre un mar de nubes por el que vuelas. Las prendas flotan en el aire.

Sin build y sin dependencias: se abre `index.html` en el navegador. Todo va en
ese archivo — HTML, CSS, GLSL y JS. Ni Three.js ni nada de CDN.

## Cómo está hecho el cielo

Las nubes **no son imágenes**. Son un volumen raymarcheado en el fragment
shader (`FRAG`, dentro del `<script>`). Cada rayo atraviesa una losa de ruido
fractal entre `BOT` y `TOP`, y en cada muestra lanza una segunda marcha corta
hacia el sol para saber cuánta luz llega a ese punto. Ese autosombreado es lo
único que hace que se lean como volumen y no como niebla — si se toca algo,
que sea con cuidado.

Se genera entero, así que no se repite nunca y se puede volar a través.

Parámetros que merece la pena tocar, todos en el shader:

    BOT / TOP     dónde empieza y acaba la capa de nubes
    uCover        cuánto cielo tapan (por hora del día, ver abajo)
    dens()        la forma: `prof` es el perfil vertical, `fbm4` las masas
                  grandes, `fbm2` la erosión de los bordes

## Una sola cámara

La misma cámara dibuja las nubes y coloca las prendas. `buildCamera()` calcula
posición y base (`fwd` / `rgt` / `upv`), el shader la usa para lanzar los rayos
y `place()` la usa para proyectar cada elemento del DOM sobre la pantalla. Por
eso las prendas comparten perspectiva con el cielo en vez de flotar encima de
una foto de un cielo.

Las prendas son `<button>` de verdad con su `<img>`: se pueden tabular, tienen
texto alternativo y salen en el buscador. Solo su posición es 3D.

## El vuelo

El scroll es la distancia recorrida. `#runway` es un div vacío de `760vh` cuya
única función es dar longitud al scroll; `flightProgress()` lo convierte en
0–1 y la cámara avanza `ZSPAN` unidades.

La entrada (`enter()`) es una animación aparte: sube la cámara de dentro de la
nube hasta por encima de la capa en 3,2 s, con un fundido a blanco en el
momento más denso.

## Las tres horas

Peace, Mystery y Nostalgia no son un cambio de paleta: son la hora del cielo.
Cambian el sol, su color, el degradado, la cobertura de nube y las estrellas.
Están en `HOURS`, y se interpolan suavemente al cambiar.

## Lo que hay en el cielo

Todo se declara en el array `SKY`, en orden de profundidad:

    { k: 'garment',
      h: 'black-stone',            // handle de Shopify: define el enlace
      n: 'Black Stone "WiP?"',
      p: 39.99,
      pillar: 'Mystery',
      img: 'IMG-0276.jpg',         // fichero en el CDN de Shopify
      at: [-21, 89, 540],          // x, y, z en el mundo
      size: 13,                    // altura en unidades de mundo
      sold: true,                  // opcional
      exclusive: true,             // opcional
      say: '…' }                   // texto de la ficha

    { k: 'verse', at: [0, 78, 404], w: 700, wide: 30, html: '…' }

`at[2]` es la profundidad: sube ese número y la prenda aparece más tarde en el
vuelo. La cámara recorre de z≈96 a z≈1156.

**No hay carrito.** Cada prenda enlaza a su página real en Shopify, que es
donde están las tallas, el stock y el checkout.

## Rendimiento

Se renderiza a menos resolución que la pantalla y se escala (las nubes son
suaves, no se nota). Si baja de 34 fps, `quality` baja sola: menos pasos de
raymarch y menos resolución. Sin WebGL2 se cae a un cielo de degradados CSS
(`#flat`) y el resto del sitio sigue funcionando.

## Pendiente de comprobar en producción

- **Las fotos.** Van por URL al CDN de Shopify que ya las sirve. No se pudieron
  cargar desde donde se construyó esto — hay que abrirlo una vez con red.
- **Los enlaces de TikTok y Discord** están puestos a mano; faltan los reales.
- Las descripciones de cada prenda están escritas para esta versión, no salen
  del Shopify. Conviene repasarlas.

## Accesibilidad

Prendas y controles son botones con foco visible. `Esc` cierra la ficha. Con
`prefers-reduced-motion: reduce` el tiempo del shader se congela y la entrada
es casi instantánea.

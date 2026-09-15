# Clout Native

Sitio de una sola página para la marca. Sin build: se abre `index.html` en el
navegador. Todo va en ese archivo — HTML, CSS y JS.

## De dónde sale cada cosa

El texto de **About us**, los nombres, los precios y las fotos vienen tal cual
del Shopify actual (`cloutnative.com`). Las descripciones de cada prenda en la
ficha sí están escritas para esta versión — conviene repasarlas antes de
publicar.

## Las tres atmósferas

Los pilares de la marca — **Peace, Mystery, Nostalgia** — no son solo texto:
son el único control de tema que tiene la página. Al pulsar cualquiera de los
tres (en la cabecera, en el hero, en el pie o en los propios pilares del
manifiesto) cambia la paleta entera, el grano y la luz de fondo. La elección
se guarda en `localStorage`.

Cada paleta está definida como un bloque de variables al principio del `<style>`:

    :root[data-mood="mystery"] { --bg: …; --text: …; --accent: …; }

Para retocar un color, se toca ahí y afecta a toda la página.

## La marca

La nube con la ventana está dibujada en SVG dentro del `<script>`
(`cloudWindow()`), no es una imagen. Por eso se puede recolorear con el tema,
respirar, y el cielo de dentro se mueve con el cursor: la idea es que estás
mirando *a través* de la ventana, no *a* un logo.

Va en tres sitios (`data-mark="gate" | "top" | "hero" | "creed"`). Si se
quiere sustituir por el logo real de la marca, basta con cambiar lo que
devuelve esa función.

## Las prendas

Se declaran en el array `PIECES` del `<script>`:

    { h: 'black-stone',                  // handle en Shopify: define el enlace
      n: 'Black Stone "WiP?" T-shirt',
      p: 39.99,
      kind: 'tee',                       // 'tee' | 'heavy' — alimenta los filtros
      drop: true,                        // sale en la pestaña NEW DROP
      sold: true,                        // marca agotado y desactiva el botón
      exclusive: true,                   // insignia de edición exclusiva
      pillar: 'Mystery',                 // a qué pilar pertenece
      front: 'IMG-0276.jpg',             // fichero en el CDN de Shopify
      back:  'IMG-0277.jpg',             // opcional: se ve al pasar por encima
      d: '…' }                           // texto de la ficha

Las fotos se piden al CDN de Shopify que ya las sirve:
`https://cloutnative.com/cdn/shop/files/<fichero>?width=900`. Si una foto no
carga, la tarjeta se queda con un marcador rayado con el nombre de la prenda
en lugar de una imagen rota.

**No hay carrito propio.** Cada ficha enlaza a su página real en Shopify, que
es donde están las tallas, el stock y el checkout. Así no hay dos inventarios
que mantener.

## Pendiente de comprobar en producción

- **Las fotos.** Se referencian por URL del CDN de Shopify; no se pudieron
  cargar desde el entorno donde se construyó esto, así que hay que abrir la
  página una vez con red para confirmar que salen todas.
- **El formulario de newsletter.** Envía a `cloutnative.com/contact` con los
  campos que espera Shopify. Hay que probar que da de alta de verdad.
- **Los enlaces de TikTok y Discord** están puestos a mano
  (`tiktok.com/@cloutnative`, `discord.gg/cloutnative`) — hay que poner los
  reales.

## Accesibilidad y movimiento

Todo lo pulsable es un `<button>` o un `<a>` con foco visible. La ficha se
cierra con `Esc` y se recorre con `←` `→`. Con
`prefers-reduced-motion: reduce` se apagan las animaciones.

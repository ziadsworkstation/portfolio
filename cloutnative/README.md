# Clout Native — la habitación

No es una tienda, es un portal. Estás dentro de una habitación hecha de cielo:
paredes y techo pintados de nubes, suelo de hierba, y una puerta blanca
entreabierta al fondo. La atraviesas y estás en la siguiente. Las prendas
flotan en el aire de cada habitación.

Sin build y sin dependencias: se abre `index.html` en el navegador. Todo va en
ese archivo — HTML, CSS, GLSL y JS. Ni Three.js ni nada de CDN.

## Cómo está hecha la habitación

Está trazada en el fragment shader (`FRAG`, dentro del `<script>`). No es un
raymarch: como el rayo siempre mira hacia delante, basta con cortarlo contra
los planos de la caja y quedarse con el más cercano. El truco está en el hueco
de la puerta — si el rayo da en la pared del fondo dentro del rectángulo de la
puerta, **no para**: avanza a la habitación siguiente. Por eso se ve un
corredor de puertas encadenadas, y cada una que atraviesas añade luz.

    RW   9      mitad del ancho
    RH   11     alto
    RL   26     largo de cada habitación
    DW   1.75   mitad del ancho de la puerta
    DH   4.9    alto de la puerta

El cielo de las paredes es `mural()`: un ruido fractal en 2D, porque es pintura
sobre pared, no distancia. `turf()` es la hierba. La puerta blanca es un plano
girado sobre su bisagra (`uSwing`), con sus dos entrepaños, su manilla y su
sombra sobre la hierba.

## Una sola cámara

La misma cámara traza la habitación y coloca las prendas. `buildCamera()`
calcula posición y base, el shader la usa para lanzar los rayos y `place()`
la usa para proyectar cada elemento del DOM. Por eso las prendas comparten
perspectiva con la habitación en vez de flotar sobre una foto.

Las prendas son `<button>` de verdad con su `<img>`: se pueden tabular, tienen
texto alternativo y salen en el buscador. Solo su posición es 3D.

## El paseo

El scroll es la distancia andada. `#runway` es un div vacío de `760vh` cuya
única función es dar longitud al scroll. La cámara va de z=28 a z=128, cuatro
habitaciones. `enter()` es la primera puerta: te lleva de z=14 a z=28
atravesando el hueco, con un fundido a blanco al pasar.

## Las tres horas

Peace, Mystery y Nostalgia cambian la hora de la habitación: el azul, las
nubes, la hierba, la luz que entra por la puerta y las estrellas. Están en
`HOURS` y se interpolan al cambiar.

## El logo

`cloudWindow()` dibuja el cuatrifolio con la ventana en cruz, con degradado
cromado. **Es una reconstrucción**, no el vector oficial — si tienes el SVG
bueno, sustituye lo que devuelve esa función y todo lo demás sigue igual.

## Lo que hay en cada habitación

Todo se declara en el array `SKY`, en orden de profundidad:

    { k: 'garment',
      h: 'black-stone',          // handle de Shopify: define el enlace
      n: 'Black Stone "WiP?"',
      p: 39.99,
      pillar: 'Mystery',
      img: 'IMG-0276.jpg',       // fichero en el CDN de Shopify
      at: [-5.4, 6.2, 66],       // x, y, z dentro del corredor
      size: 3.1,                 // alto en unidades de mundo (la sala mide 11)
      sold: true,                // opcional
      say: '…' }                 // texto de la ficha

    { k: 'verse', at: [0, 8.4, 56], w: 760, wide: 12.5, html: '…' }

Los versos van a y=8.4, por encima del dintel: se leen como rótulo de la sala.
Las prendas se apartan del eje (|x| > 3) para no tapar la puerta.

**No hay carrito.** Cada prenda enlaza a su página real en Shopify, que es
donde están las tallas, el stock y el checkout.

## Rendimiento

Se renderiza a menos resolución que la pantalla y se escala. Si baja de 34 fps,
`quality` baja sola. Sin WebGL2 se cae a una habitación de degradados CSS
(`#flat`) y el resto sigue funcionando.

## Pendiente

- **Las fotos.** Van por URL al CDN de Shopify. No se pudieron cargar desde
  donde se construyó esto — hay que abrirlo una vez con red.
- **El logo oficial** en vector, para sustituir la reconstrucción.
- **TikTok y Discord**: los enlaces están puestos a mano.
- Las descripciones de cada prenda están escritas para esta versión.

## Accesibilidad

Prendas y controles son botones con foco visible. `Esc` cierra la ficha. Con
`prefers-reduced-motion: reduce` el tiempo del shader se congela y la entrada
es casi instantánea.

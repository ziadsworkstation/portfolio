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

Está **trazado de la foto de la espalda de una camiseta**
(`assets/garments/what-is-peace-grey-back.jpg`): se umbralizó el estampado
negro, se sacaron sus cinco contornos — el exterior y los cuatro paños
huecos — se suavizaron y se pasaron a curvas. El resultado vive en la
constante `MARK_D` de `index.html`, y `cloudWindow()` lo pinta plano donde va
pequeño y cromado sobre la puerta.

Es la forma real, no una reconstrucción a ojo. Pero viene de tela fotografiada,
así que si aparece el vector original sigue siendo mejor: se cambia `MARK_D` y
ya está, nada más lo toca.

Lo importante de la forma, que la versión anterior tenía al revés: el
cuatrifolio es **hueco**, no macizo, y cada uno de los cuatro paños lleva una
púa curvada hacia dentro.

## Una sala, cinco respuestas

La web es una sola colección: *What is Peace?* — una pregunta estampada en
cinco colores. Así que es **una sola habitación**, sin pasillo y sin scroll.
Entras por la puerta, te quedas de pie delante de las cinco, y ya está.

`PIECES` es la colección en orden. `RAILS` dice qué cuelga de cada barra —
tres a la izquierda del vano, dos a la derecha — y las prendas se reparten
solas a lo largo del largo que se le dé a la barra.

## La sala toma la hora de la prenda que miras

Cada camiseta tiene su hora (`hour`), sacada del color de su tela:

    White Bones   dawn      bruma cálida de amanecer
    Pure Water    clear     día limpio, el azul que le da nombre
    Greek Stone   overcast  cubierto, luz plana
    Black Stone   night     noche con estrellas
    Cotton Candy  dusk      atardecer malva

Al pasar por encima de una, la sala **deriva** hacia su hora; al quitarte,
vuelve a `clear`. Al pulsarla se queda ahí, las otras cuatro se apagan y sale
su ficha. `drift()` interpola todas las variables del cielo cada fotograma —
no hay transición escrita, es el cielo moviéndose.

Los textos de la interfaz **no se invierten cuando eliges la noche, sino
cuando la sala se ha oscurecido de verdad**: `drift()` mide la luminancia del
cielo interpolado y cambia `data-sky` al cruzar el umbral. Si se invirtieran
al pulsar, quedarían blancos sobre un cielo todavía claro.

## Las paredes mandan sobre el DOM## Las paredes mandan sobre el DOM

Las prendas son elementos del DOM, así que **el shader no puede taparlas**: sin
más, una burra de la sala 3 se vería a través de la pared de la sala 1. Eso lo
impone `place()` a mano — solo se ve lo que está en tu sala, más lo que cabría
por el hueco de la puerta (`|x| < 2.4` y `y < 4.4`). Si tocas la geometría de
la sala, hay que tocar también ese cono.

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

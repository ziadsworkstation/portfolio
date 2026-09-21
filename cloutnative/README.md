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

## Salas, colecciones y horas

Cada sala **es** una colección y **tiene** una hora fija. Se declara todo junto
en `ROOMS`:

    { hour: 'mystery', name: 'Mystery', sub: 'What the window does not show you' }

El shader recibe la tabla entera de paletas (`uPal`, `uCfg`) y qué hora guarda
cada sala (`uRoomHour`), así que **pinta cada tramo del corredor con su propia
hora**. Por eso, de pie en la sala de día, por el hueco de la puerta ves la de
noche. No hay transición que programar: la sala siguiente ya se está pintando
con su color antes de que entres.

Las tres palabras de arriba a la derecha ya no cambian el tema: te llevan
andando a la sala que guarda esa hora.

## Las burras y lo que cuelga

`RACKS` pone dos burras por sala, a `x = ±4.9`, apartadas del eje de la puerta.
`WARDROBE` dice de qué burra y en qué hueco cuelga cada prenda:

    { h: 'black-stone',        // handle de Shopify: define el enlace
      n: 'Black Stone "WiP?"',
      p: 39.99,
      room: 2,                 // en qué sala
      rail: 0,                 // 0 izquierda, 1 derecha
      slot: -1,                // -1, 0 o 1 a lo largo de la barra
      img: 'IMG-0276.jpg',
      tall: 3.1,               // alto en unidades de mundo (la sala mide 11)
      say: '…' }

La posición se calcula sola: `RAIL - tall/2`, así que **todas las prendas
cuelgan con el hombro a la altura de la barra** sea cual sea su largo.

La burra es un SVG plano (dos pies, dos montantes, tubo cromado y su sombra),
porque una barra puesta de frente al pasillo es casi plana de verdad.

## Las paredes mandan sobre el DOM

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

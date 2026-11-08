# Revisiones (árbitro adversarial independiente por vuelta)

Ponderada = 0,4·Diseño + 0,3·Usabilidad + 0,2·Creatividad + 0,1·Contenido.

Listón: ponderada ≥ 8,8, Creatividad ≥ 8,5 y ningún criterio por debajo de 8.

## Línea base (`main` @ 381783f)

| Medida | Resultado |
|---|---|
| Errores en consola | 5 por carga (logo de Linux) |
| axe (claro / oscuro) | 4 / 7 fallos |
| Lighthouse escritorio | Perf 100 · A11y 88 · BP 96 |
| Lighthouse móvil | Perf 96–100 · A11y 88 · BP 96 |

## Vuelta 1: notas D 7 · U 5 · C 7 · Co 6 → **ponderada 6,3**

**Añadido:**
- dirección «libro de cuentas moderno»: papel y tinta, bandas nocturnas, Fraunces + Geist;
- hero con réplica viva de «Tu patrimonio»: odómetro, curva real, inclinación 3D y foco de luz con `transform`;
- cinta de cifras;
- «La ecuación»;
- recorrido con pantalla fija;
- bento de funciones;
- banda de cifras;
- línea de tiempo;
- galería con pestañas;
- comparador claro/oscuro;
- teléfonos;
- diagrama de privacidad;
- FAQ ampliada;
- pie nuevo;
- OG nuevo;
- 31 capturas nuevas de la v1.20.0.

**Corregido durante la vuelta:**
- Performance móvil: de 71–73 a 96–99. El LCP estaba retrasado por la opacidad del hero.
- Contraste del oro sobre papel.
- `aria-label` en elementos `div`.
- Zonas desplazables sin foco con movimiento reducido.
- Botones del hero que heredaban el color de enlace.

**Checks:**
- consola limpia;
- sin scroll horizontal entre 360 y 1920;
- axe 0 / 0;
- foco visible;
- solo transform y opacity;
- Lighthouse escritorio: Perf 98 · A11y 100 · BP 96;
- Lighthouse móvil: Perf 96–99 · A11y 100 · BP 96. El BP de 96 es el 403 de cupo de la API, igual que en la base.

**Defectos del árbitro:**
- **B1 · bloqueante.** Los enlaces a `#descarga` se pasan de largo en la primera visita, por `content-visibility` y su estimación de altura.
- **M1.** E2 perdido: la animación de entrada fija el `transform` del icono.
- **M2.** El pie del carrusel tiene `aria-live` y anuncia cada 4 s.
- **M3.** El menú marca la sección equivocada.
- **M4.** Textos inexactos:
  - «Nada que instalar», que no es verdad en Mac ni en Linux;
  - «0 datos enviados», cuando los precios se piden a terceros;
  - la suma de la tarjeta parece fallar por 1 €.
- **M5.** El botón flotante duplica «Descargar» del menú y tapa contenido.
- **m1.** Móvil: pestañas y selector partidos en dos filas, el décimo punto del carrusel salta de línea, la tarjeta del hero queda fuera de la primera pantalla.
- **m2.** Las capturas no se pueden ampliar con teclado; los puntos tienen `role="tab"` sin panel.
- **m3.** CSS muerto.
- **m4.** Demasiado movimiento continuo a la vez.

**Novedades que el árbitro considera gratuitas:**
- la banda de ceros;
- la marquesina y el bento, que dicen lo mismo;
- el logo repetido en el hero;
- los rayos animados sin fin;
- las etiquetas «1.19» y «1.20».

**Inventario:**
- **Perdido:** E2.
- **Degradados:** F14, F17 y F22.
- **Se conservan:** todos los demás.

## Vuelta 2

**Correcciones de la vuelta 1:**
- **B1.** `content-visibility` se queda, porque sin él el móvil baja a Perf 72–86. Pero se desactiva (clase `sin-cv`) justo antes de seguir cualquier ancla interna, o si la URL llega con `#`. Medido: «Descargar gratis», «Descargar» del menú y «Preguntas» aterrizan a 84 px, debajo del menú, en la primera visita, a 1440 y a 390.
- **M1 / E2.** El icono va dentro de una pastilla de versión («1.20 · Nuevo diseño y un hogar de ejemplo completo»). La animación de entrada está en el enlace y el `hover` en la imagen, así que E2 vuelve a funcionar. Fuera el logo grande repetido.
- **M2.** El pie del carrusel usa `aria-live="off"` en el autoavance y `polite` solo al navegar a mano.
- **M3.** La sección activa se calcula con el scroll sobre todas las secciones de `main`. Cada sección cuenta para su enlace del menú; en el hero y en la descarga no se marca ninguno.
- **M4.**
  - «Descargar, abrir y empezar.» en lugar de «Nada que instalar»;
  - fuera la banda de cifras (y con ella «0 datos enviados» y «1 archivo sin instalar»);
  - filas de la tarjeta del hero con céntimos (153.415,40 + 159.540,17 = 312.955,57 → 312.956);
  - ecuación con cifras bien redondeadas (560.082 − 247.126 = 312.956; cartera 163.582, coche y tarjeta 10.166).
- **M5.** En escritorio el flotante es un círculo de icono que cabe en el margen. Mientras está visible, el «Descargar» del menú se retira (opacidad, sin foco y con `aria-hidden`). Así solo hay un «Descargar» a la vista. Se conserva F17: aparece pasados 600 px y se oculta sobre `#descarga`.
- **m1.** Móvil:
  - pestañas de la galería y selector de sistema en una sola línea a 360 px;
  - las flechas del carrusel bajan al pie y dejan de tapar la captura;
  - 11 indicadores en una línea;
  - hero más compacto, con la tarjeta antes de las insignias: asoma en la primera pantalla a 390×844.
- **m2.** Las capturas se amplían con teclado: `role="button"`, `aria-label` «Ampliar: …» y Enter o Espacio (la del carrusel, solo la activa es enfocable). Los indicadores pasan de `role="tab"` a `aria-current`.
- **m3.** Fuera el CSS muerto (`.punto-vivo`, `.cinta-nota`, `.nuevo`, `.feat-cifra`, cifras). Los estilos inline de los h3 pasan a `.sub-h3` y `.sub-p`.
- **m4.** Los paquetes de la bóveda solo cruzan 3 veces al entrar en pantalla, y las tarjetas flotantes van más lentas (10 s).
- **Inventario.** F14: el Panel vuelve a 11 capturas (se añade «Cartera en tema claro»).

**Novedades:**
- **La ecuación se puede tocar.** Cada partida (cartera, inmuebles, hipotecas, coche y tarjeta) es un botón con `aria-pressed`. Al quitarla o sumarla, los odómetros giran desde la cifra anterior hasta la nueva. El total se pone en rojo si sale negativo, con signo menos tipográfico, y hay un anuncio para lectores de pantalla.
- **La marquesina ya no repite el bento.** Ahora es «Lo que puedes llevar en Liberty», con 14 tipos de activo y deuda. E3 se conserva.
- Espacio duro antes de «€» en todos los odómetros (antes salía «312.956€»).
- Ritmo vertical más corto: secciones `clamp(72px,8.5vw,124px)` y pasos del recorrido al 58 vh.
- Fuera las etiquetas de versión del bento.

**Checks:**
- consola limpia;
- sin scroll horizontal de 360 a 1920 px;
- axe 0/0 en claro y en oscuro;
- 45 paradas de foco, todas visibles;
- solo transform y opacity;
- Lighthouse escritorio: Perf 98 · A11y 100 · BP 96;
- Lighthouse móvil: Perf 94–98 · A11y 100 · BP 96.

**Veredicto del árbitro, vuelta 2:** D 7,5 · U 7,5 · C 7,5 · Co 8,0 → **ponderada 7,6** (antes 6,3).
- **Correcciones de la vuelta 1:** B1, M1, M2, M3, M4, m1, m2 y m4 resueltas. M5 y m3, a medias.
- **Inventario:** 23 se conservan, 8 mejoran, 1 degradación leve (E2, el icono es más pequeño), 0 perdidos.
- **Defectos mayores:**
  - M1: el carrusel avanza con el ratón o el foco dentro;
  - M2: el flotante tapa texto en móvil;
  - M3: no hay menú por debajo de 980 px;
  - M4: movimiento infinito sin pausa (WCAG 2.2.2);
  - M5: el nodo «Nube» sale deformado.
- **Defectos menores:**
  - m1: al cargar con #ancla queda descolocado;
  - m2: la pastilla se estira en tableta;
  - m3: la palabra del pie pisa el aviso legal;
  - m4: la pista de la ecuación va detrás;
  - m5: los indicadores del recorrido tapan la captura;
  - m6: la captura de Cartera choca con el hero;
  - m7: detalles de texto;
  - m8: en oscuro se pierden las bandas.
- **Gratuito:**
  - la galería repite el recorrido;
  - la bóveda contradice el texto;
  - las tarjetas flotantes no se pueden pausar.
- **Camino a 9:** «el libro se cuadra» con un sello, el hero con el tiempo dentro, una bóveda veraz, el pie a todo el ancho y el recorrido horizontal en móvil.

El usuario decide cerrar en 3 vueltas: la vuelta 3 aplica todo lo anterior, se arbitra y se despliega.

## Vuelta 3

**Correcciones:**
- **M1.** El carrusel no arranca si el ratón está encima, si el foco está dentro o si está la pausa global. Al navegar con el teclado, el foco sigue a la imagen activa.
- **M2.** En móvil manda el «Descargar» del menú, que es fijo y siempre visible, y el flotante no se muestra; el flotante se queda solo en escritorio. Se oculta también sobre el pie, y el botón del menú solo se retira en escritorio.
- **M3.** Menú de secciones en móvil y tableta: un `<details>` con 7 enlaces. Se cierra al elegir, con Esc o al tocar fuera, y marca la sección activa.
- **M4.** Botón global «Pausar el movimiento» en el menú, con `aria-pressed`, recordado entre visitas. Para la cinta, la marquesina, las tarjetas flotantes, los paquetes de la bóveda y el autoavance de los carruseles.
- **M5.** Los iconos de los nodos ya no se deforman (`max-width:none`).
- **m1.** Si se llega con #ancla, la página se recoloca cuando aparecen el contador y las novedades, salvo que el usuario ya se haya movido. Medido: `#faq` a 84 px a 1440 y a 81 px a 390.
- **m2.** La pastilla usa `justify-self:start`.
- **m3.** La palabra «Liberty» del pie se ajusta al ancho y no toca la línea legal. Limpieza: 6 símbolos sin uso, h3 ocultos, una transición muerta, un `top` duplicado y un comentario desfasado.
- **m4.** La pista va antes del libro, y las partidas llevan ✓ o ✕ según estén sumadas o no.
- **m5.** Los indicadores del recorrido pasan a la barra del marco.
- **m6.** El paso «Cartera» del recorrido usa la captura de Rentabilidad. La galería deja de repetir Inicio y suma «Inmuebles en tema claro»; siguen siendo 11 capturas en el Panel.
- **m7.** Anuncio con «menos», `user-select:none` en los odómetros, «Sin coste. Sin cuentas. Sin letra pequeña.» y «La app estrena diseño…».
- **m8.** En oscuro el papel pasa a `#161a21`, separado de la noche `#0b0d11`.

**Novedades (camino a 9):**
- **El hero lleva el tiempo dentro.** La gráfica de la tarjeta se recorre mes a mes con la serie REAL del hogar de ejemplo: 91 meses, de mayo de 2019 a noviembre de 2026.
  - Se mueve con el ratón, arrastrando en táctil o con las flechas, gracias a un `input range` accesible con `aria-valuetext`.
  - Cambian el odómetro, la barra y la leyenda cartera/inmuebles, la variación a 12 meses y las dos filas con céntimos.
  - Un cursor vertical con su punto se desplaza con `transform`.
- **El libro se cuadra.** Los apuntes entran escalonados, el filete doble se dibuja con `scaleX` y se estampa un sello «Cuadrado».
  - Al quitar partidas, el sello se vuelve a estampar como «Simulación».
  - Si el total queda negativo, dice «En rojo» y se pinta en rojo.
- **Bóveda veraz.** Cuatro conexiones tachadas y una permitida, «Precios · solo cotizaciones». Por esa conexión va la petición (oro) y vuelve la cotización (verde). Ahora tiene `role="img"` con una descripción.
- **Recorrido horizontal en móvil y tableta.** Tarjetas con `scroll-snap` y la indicación «Desliza para ver las cinco».
- **Releases bajo demanda.** El contador, la versión y las novedades se piden al acercarse a la descarga, o al instante si la URL trae #. Gasta menos cupo de la API y saca ese trabajo de la carga.

**Checks:**
- consola limpia;
- sin scroll horizontal de 360 a 1920 px;
- axe 0/0 en claro y en oscuro;
- 45 paradas de foco, todas visibles;
- solo transform y opacity.

**Lighthouse:**
- escritorio: 98/100/100 en las tres pasadas, con el equipo tranquilo; con carga hubo pasadas de 72–75, también en la v2 y en la base;
- móvil: 89–97/100/100.

El trabajo del hilo principal es igual o menor que en la v2 (estilo y layout 1018 ms frente a 1111). La diferencia es ruido de cuándo cae la tarea larga. BP sube a 100 porque esta vez la API respondió.

**Veredicto del árbitro, vuelta 3:** D 8,0 · U 7,8 · C 8,0 · Co 8,5 → **ponderada 8,0** (6,3 → 7,6 → 8,0).
- **Correcciones y novedades:** todas las de la vuelta 2 resueltas.
- **Inventario:** 22 se conservan, 8 mejoran, 1 cambia por diseño (el flotante solo en escritorio), 1 degradación leve (E2) y 0 perdidos.
- **Veredicto:** se puede publicar si antes se corrigen B1 (en táctil la tarjeta se queda en una fecha antigua) y M1 (puntos táctiles del carrusel demasiado pequeños).
- **Listón:** no se alcanza (8,8). El usuario había decidido cerrar en 3 vueltas.

### Cierre (después del árbitro de la vuelta 3)
- **B1.**
  - En táctil, el control invisible no recibe el dedo.
  - La gráfica solo se recorre con un gesto claramente horizontal, y al soltar vuelve sola al mes actual en 1,8 s.
  - Medido con eventos táctiles reales: un scroll vertical sobre la gráfica mueve la página y la cifra sigue en 312.956 €; el gesto horizontal lleva a junio de 2021 y vuelve.
- **M1.** Por debajo de 600 px se quitan los puntos del carrusel; quedan las flechas de 38 px y el «6 / 11». axe con WCAG 2.2 a 390 px da 0.
- **M2.** Hitos REALES del ejemplo sobre la gráfica:
  - piso en alquiler, mayo de 2019;
  - casa, mayo de 2021;
  - trastero, noviembre de 2021;
  - garaje, julio de 2023;
  - empieza a registrarse la cartera, noviembre de 2023.

  El rótulo de la gráfica nombra el hito al pasar por él, así que la parte plana ya cuenta algo.
- **m1.** El menú móvil marca su propia sección, incluidas Capturas y Descarga.
- **m2.** Las cifras de la gráfica llevan punto de miles («+4.948 €»), y el primer mes dice «Punto de partida».
- **m3.** «Verificar integridad» y «Novedades» llevan +/−.
- **m4.** Por debajo de 380 px los nodos de la bóveda se acercan.
- **m5.** El botón de pausa tiene `title`.
- **Mejora gratuita aplicada:** el contador de descargas gira con el odómetro.

**Checks ampliados** (axe con WCAG 2.1 y 2.2, también a 390 px, y 80 tabulaciones):
- consola limpia;
- sin scroll horizontal de 360 a 1920 px;
- axe 0 en claro, en oscuro y a 390;
- 80 paradas de foco, todas visibles;
- solo transform y opacity.

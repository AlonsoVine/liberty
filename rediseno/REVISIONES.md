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

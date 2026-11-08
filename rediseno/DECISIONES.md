# Decisiones del rediseño (rama `mejora-epica`)

Cada ambigüedad del encargo, resuelta y anotada aquí sin preguntar.

## Alcance y método
- **Qué se rediseña.** La landing pública de Liberty (`index.html`, GitHub Pages). El método venía de un encargo de currículum; Alonso pidió ignorar esa parte final.
  - El check «lo esencial del currículum en < 10 s» lo traduzco a: en menos de 10 segundos, también en móvil, se entiende qué es Liberty, para quién es, que es gratis y local, y dónde se descarga.
  - El check de metadatos y versión imprimible también formaba parte de ese bloque. Lo mantengo igualmente (metadatos y OG nuevos, y una hoja `@media print` limpia) porque cuesta poco.
- **Despliegue.** Al acabar las vueltas, Alonso pidió desplegar. Eso supone merge a `main` y push (GitHub Pages publica desde `main`). Es la única excepción a «no tocar `main`».
- **Material del proceso.** Inventario, decisiones, revisiones y capturas viven en `rediseno/`, junto a la web. Pages también los publica, pero no se enlazan desde ningún sitio.

## Dirección de arte
- **Concepto: «libro de cuentas moderno».** Una web de economía que se lee como un periódico financiero contemporáneo:
  - papel cálido y tinta en el cuerpo;
  - bandas nocturnas tipo terminal en el hero, la descarga y el pie;
  - rejilla de fondo fina;
  - oro como acento, el oro del icono de Liberty.
- **Tipografía.** La misma de la app desde la v1.20.0: Fraunces (títulos y cifras, `opsz` 144) y Geist (texto). Se sirven en local desde `fuentes/` (licencia OFL incluida), sin CDN.
- **Momento firma del hero.** Una réplica viva de la tarjeta «Tu patrimonio» de la app:
  - odómetro de 312.956 €;
  - barra de reparto que crece;
  - curva real de «Cómo ha crecido», extraída del SVG que pinta la app, revelada con un barrido hecho solo con transform;
  - inclinación 3D con el ratón.
- **Cinta de cotizaciones.** Las cifras de la cinta son las del hogar de ejemplo y lo dice su etiqueta accesible. No hay cotizaciones inventadas.
- **«La ecuación».** Sección nueva con el patrimonio de ejemplo como asiento contable: 560.081 € − 247.125 € = 312.956 €.
  - Las cifras salen del cálculo real de la app (`/datos.js` del ejemplo).
  - Desglose: cartera 163.581 € + inmuebles 396.500 €; deudas fuera de hipotecas 10.165 € + hipotecas 236.960 €.
- **Iconos.** Los emojis pasan a iconos de línea propios en un sprite SVG, igual que la app v1.20.0.
- **Logo de Linux.** Se redibuja: el de la base tenía el trazado `d` roto y daba 5 errores en consola por carga.

## Contenido
- **Capturas.** Todas nuevas, de la v1.20.0 con el hogar de ejemplo (tema oscuro; también claro y móvil):
  - generadas desde una copia del ejemplo como cartera propia («Nuestro hogar»), porque las notas no se ven en la demo de solo lectura;
  - sin la tarjeta «¿Te está siendo útil?», con los avisos plegados y la ruta de datos sustituida por `D:/Liberty/mis_datos`, para no publicar rutas del equipo de Alonso;
  - copia íntegra en `C:\proyectos\GestorPatrimonial\Imgs_GestorPatrimonial\v1.20.0`, a petición de Alonso.
- **Secciones nuevas:**
  - navegación fija con progreso de lectura;
  - «La ecuación»;
  - «Recorrido»: pantalla fija con 5 pasos al hacer scroll;
  - banda de cifras;
  - comparador claro/oscuro;
  - «También en el móvil»;
  - diagrama de privacidad.
- **Contenido actualizado:**
  - funciones de la 1.17–1.20: inmuebles, libertad financiera, alertas de precio, deshacer, Inicio a tu gusto, ocultar importes, cuadernos y archivos, facturas;
  - hogar de ejemplo;
  - ubicación de los datos en Mac;
  - tres preguntas nuevas en la FAQ: probar sin datos, usarlo desde el móvil o varios equipos, y el «Hay que instalarlo» del Mac.
- **«Código abierto» → «Código fuente público».** La licencia de Liberty es híbrida: las aportaciones de Liberty tienen todos los derechos reservados. Llamarlo «código abierto» era inexacto. El sello sigue existiendo (F12) con el texto correcto.
- **Capturas agrupadas.** Los tres carruseles y la captura de Ajustes se agrupan en una galería con pestañas (Panel / Mis datos / Documentos / Ajustes). Cada carrusel conserva todo lo del inventario (F14):
  - autoavance de 4 s, flechas, indicadores, deslizar y teclado;
  - pausa con ratón, con foco y con la pestaña del navegador oculta.

  Además, ahora no avanza mientras está oculto en otra pestaña de la galería y tiene un pie con número y título.

## Técnica
- **Movimiento solo con transform y opacity.**
  - El foco de luz del ratón (E1) es ahora un disco que se mueve con `transform` (antes se repintaba el gradiente).
  - La elevación de las tarjetas usa una sombra en un pseudo-elemento que se funde con `opacity`.
  - La única propiedad no compuesta es el `clip-path` del comparador. No es una animación: sigue al dedo o al ratón mientras arrastras.
- **Movimiento reducido.** Todo queda quieto y legible:
  - las cifras aparecen con su valor final;
  - la cinta y la marquesina pasan a scroll manual, enfocables con teclado;
  - el carrusel no avanza solo.
- **Rendimiento.**
  - La entradilla del hero (el elemento LCP) se pinta desde el primer fotograma; el titular se anima con CSS, sin esperar al JS.
  - `content-visibility:auto` en las secciones bajo el pliegue.
  - Odómetros y clones de la marquesina se montan cuando hacen falta.
  - Con eso el Performance móvil vuelve a 96–99, como la base; la primera versión daba 71–73.
- **Caché de la API de GitHub.** Las releases se guardan 15 minutos en `localStorage` (`liberty-releases`): recargar no gasta el cupo de 60 peticiones/hora. El contador (F7) suma igual y se sigue ocultando si la API falla.
- **Checks con una copia fija de la API.** Los checks automáticos sirven a Playwright una copia fija de `releases` (obtenida con `gh api`). Así el resultado no depende del límite de GitHub, que las propias pruebas agotan.
  - Lighthouse no puede interceptarla. Su «errors-in-console» (Best Practices 96) es ese 403 de cupo agotado, igual que en la base.
- **Botón flotante.** Cuando está oculto no recibe foco (`tabindex=-1`, `aria-hidden`).
- **Lightbox.** Atrapa el foco y lo devuelve al cerrarse. Ahora también amplía las capturas del recorrido en móvil y las de los teléfonos.

# Inventario de efectos y funcionalidades (línea base, `main` @ 381783f)

Ninguno de estos puntos se puede perder ni empeorar. El árbitro los comprueba uno a uno en cada vuelta.

## Funcionalidades
| # | Qué | Dónde (base) |
|---|---|---|
| F1 | Cambio de tema claro/oscuro con botón fijo; guardado en `localStorage["liberty-tema"]`; se aplica antes de pintar, sin parpadeo | botón `#theme-toggle`, script en `<head>` |
| F2 | Selector de sistema (Windows / Mac / Linux / Docker) con autodetección del SO y paneles alternables | `.os-selector`, `.os-panel` |
| F3 | Botón de descarga Windows → `releases/latest/download/Liberty.exe` (nombre exacto) | panel `win` |
| F4 | Botón de descarga Mac → `releases/latest/download/Liberty-macOS.dmg` (nombre exacto) | panel `mac` |
| F5 | Linux: enlace al código y explicación de `python -m app` | panel `lin` |
| F6 | Docker: guía, aviso de seguridad (VPN, no exponer) y `docker-compose.yml` de ejemplo con versión | panel `docker` |
| F7 | Contador histórico de descargas: suma de `Liberty.exe`, `Liberty-macOS.dmg` y nombres históricos de Mac en todas las releases; se oculta si la API falla; formato es-ES | script «Descargas, versión y novedades» |
| F8 | Versión y fecha de la última release, desde la API; valor de reserva estático `v1.20.0` | `#ver-actual`, `#ver-fecha` |
| F9 | Novedades de la última release (markdown ligero y seguro) en un desplegable | `#novedades` |
| F10 | Verificar integridad (SHA-256) en un desplegable con el comando de PowerShell | `details.verificar` |
| F11 | Avisos de primera apertura: SmartScreen (Windows) y Gatekeeper (Mac) | `.aviso-azul` |
| F12 | Sellos de garantía: Gratis, Sin registro, 100 % local, Código abierto | `.sellos` |
| F13 | Enlace a todas las versiones | `.ver-versiones` |
| F14 | Carruseles de capturas (Panel 11, Mis datos 6, Notas 3): avance automático cada 4 s, flechas, puntos, deslizar en móvil, flechas del teclado, pausa con ratón o foco y con la pestaña oculta | `[data-carousel]` |
| F15 | Captura única de Ajustes | `.single-shot` |
| F16 | Lightbox: clic en una captura la amplía; se cierra con clic, botón o Esc | `#lightbox` |
| F17 | Botón flotante «Descargar»: aparece tras 600 px de scroll y se oculta sobre la zona de descarga | `#fab-descarga` |
| F18 | FAQ con 10 preguntas en acordeón (`details`) | `#faq` |
| F19 | Créditos a Rumbo / Dani Domínguez Quant, enlaces a Portfolio, LinkedIn y GitHub | `footer` |
| F20 | Metadatos: title, description, canonical, Open Graph, Twitter, JSON-LD `SoftwareApplication` con `softwareVersion` | `<head>` |
| F21 | Iconos SVG de Windows, Apple, Linux y Docker en `currentColor` | `<symbol>` |
| F22 | Enlaces internos: «Descargar» del hero y FAQ → `#descarga` | — |

## Efectos y animaciones
| # | Qué | Dónde (base) |
|---|---|---|
| E1 | Foco de luz que sigue al ratón en el hero y en la descarga | `header.hero::before`, `#descarga::before` + mousemove |
| E2 | Icono del hero que se eleva al pasar el ratón | `.hero-icon` |
| E3 | Marquesina de tarjetas en dos filas, en sentidos opuestos, sin costuras (clonadas) y en pausa al pasar el ratón | `.cards-marquee` |
| E4 | Tarjetas y bloques que se elevan al pasar el ratón | `.card`, `.feat` |
| E5 | Fundido entre diapositivas de los carruseles | `.slide` (opacity) |
| E6 | Botones (CTA, descarga, flechas) con elevación al pasar el ratón | `.hero-cta`, `.btn-descarga`, `.car-btn` |
| E7 | Aparición deslizada del botón flotante | `.fab-descarga` |
| E8 | Acordeón de la FAQ con el signo +/− | `.faq-item` |
| E9 | Desplazamiento suave a los anclajes | `scroll-behavior` |
| E10 | Con «reducir movimiento»: la marquesina para y pasa a scroll manual | `@media (prefers-reduced-motion)` |

## Defectos de la base (no hay que conservarlos)
- **Consola:** 5 errores por carga, por el `d` del icono de Linux, que está mal formado.
- **axe, claro (4):** color-contrast, link-in-text-block y scrollable-region-focusable.
- **axe, oscuro (7):** los mismos más 3 de contraste.
- **Transiciones** sobre background, box-shadow, border-color, color y visibility.
- **Lighthouse** (3 ejecuciones):
  - escritorio: Performance 100, Accessibility 88, Best Practices 96;
  - móvil: Performance 96–100, Accessibility 88, Best Practices 96.
- **Capturas** de la app con la estética anterior a la v1.20.0.

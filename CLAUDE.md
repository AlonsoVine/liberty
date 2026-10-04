# Liberty — guía para la IA que mantenga este repositorio

Este repo (`AlonsoVine/liberty`) es **solo la página de presentación + descargas** de Liberty,
publicada con **GitHub Pages** desde `main` / `/` (raíz). **No contiene el código de la app.**
El código fuente vive aparte (fork privado de Rumbo) y aquí solo se publica el `.exe` como
asset de cada Release.

- Web publicada: https://alonsovine.github.io/liberty/
- Propietario: Alonso Viñé (cuenta GitHub `AlonsoVine`).
- La landing es un único `index.html` con **CSS y JS inline, 100% vanilla** (sin librerías
  externas, CSP-friendly). Imágenes en `capturas/panel|misdatos|ajustes/`. Icono en `favicon.png`
  e `icono-512.png`.

## ⚠️ Contador de descargas — REGLA IMPORTANTE (no romper)

El contador bajo el botón de descarga muestra el **total histórico y acumulado** de descargas
de Liberty, **sumando todas las versiones** (da igual la versión). Cómo funciona:

- En vivo desde la API pública: `GET /repos/AlonsoVine/liberty/releases?per_page=100`.
- Suma el campo `download_count` de **cada asset llamado exactamente `Liberty.exe`** en **todas**
  las releases.
- Con `try/catch`: si la API falla o hay rate-limit, el contador se **oculta** (nunca muestra error).
- El número se formatea con separador de miles en `es-ES`.

**Para que el total NUNCA se reinicie ni baje al publicar una versión nueva:**

1. **Crea una Release NUEVA** (p. ej. `v1.1.0`) con su propio asset `Liberty.exe`.
   - El asset nuevo empieza en 0 descargas, pero los de las releases anteriores **conservan su
     `download_count`** (GitHub nunca lo reinicia). Como el contador suma todas las releases,
     el total sigue creciendo.
2. **NO borres las releases antiguas.** Borrarlas elimina sus `download_count` del total.
3. **NO re-subas el `.exe` encima del mismo asset** de una release ya publicada: al reemplazar
   el asset se pierde su contador. Si hay que corregir un binario, hazlo en una release nueva.
4. **Mantén el nombre del asset EXACTO `Liberty.exe`** en cada release. El botón de descarga
   (`releases/latest/download/Liberty.exe`) y el contador dependen de ese nombre exacto.

Resumen: **versión nueva = release nueva con `Liberty.exe`, sin tocar ni borrar las anteriores.**
Así el contador refleja siempre "cuánta gente ha descargado Liberty en total, desde siempre".

## Publicar una versión nueva (receta)

```bash
# desde una copia local del binario ya construido (NO se construye aquí)
gh release create vX.Y.Z /ruta/a/Liberty.exe -t "Liberty vX.Y.Z" -n "Novedades..."
```

El botón de la web apunta siempre a la última release automáticamente
(`releases/latest/download/Liberty.exe`), así que no hay que tocar `index.html` al sacar versión.

## Editar la landing

- Todo está en `index.html`. Tras editar: `git commit` + `git push` a `main`; Pages redespliega
  solo en ~1 min.
- Mantener: sin dependencias externas, responsive/móvil, accesible (aria), y respetar
  `prefers-reduced-motion` en las animaciones.

## No tocar

- El binario `Liberty.exe` se genera en el proyecto de la app (fork de Rumbo de Dani Domínguez
  Quant), no aquí. Este repo solo lo distribuye.

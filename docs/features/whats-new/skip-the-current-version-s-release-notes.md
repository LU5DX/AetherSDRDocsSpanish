# Omitir las notas de la versión actual

Cuando AetherSDR detecta que hay una versión más reciente disponible, el cuadro de diálogo Novedades incluye una opción para evitar que vuelva a aparecer para esa versión. Utilice esta opción si ya ha visto las notas y no desea que el cuadro de diálogo se muestre nuevamente en el próximo inicio.

## Antes de comenzar

- El botón "Omitir esta versión" solo aparece cuando hay una actualización disponible. Si no se detecta una actualización, el botón no se muestra.
- El cuadro de diálogo Novedades debe estar abierto. Se abre automáticamente después de un cambio de versión, o manualmente a través de `Help > What's New...`.

## Pasos

1. Abra el cuadro de diálogo Novedades. Si no está ya en pantalla, vaya a `Help > What's New...`.
2. Confirme que el botón "Omitir esta versión" sea visible en el pie de página. Si no está presente, no se ha detectado ninguna actualización y omitir no es aplicable.
3. Haga clic en "Omitir esta versión".

El cuadro de diálogo se cierra. AetherSDR escribe la cadena de la versión actual en `LastSeenVersion` y la guarda. El cuadro de diálogo Novedades no aparecerá automáticamente en el próximo inicio para esta versión.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Navegador de notas de la versión | Campo de texto | Vista HTML desplazable de las entradas de la versión entre la última versión vista y la versión actual. | — |
| "¡Entendido — 73!" | Botón pulsador | Descarta el cuadro de diálogo y marca la versión como vista. | `LastSeenVersion` |
| "Actualizar" | Botón pulsador | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga en `https://github.com/aethersdr/AetherSDR/releases/latest`. | — |
| "Omitir esta versión" | Botón pulsador | Se muestra solo cuando hay una actualización disponible. Guarda la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo para que el aviso no reaparezca. | `LastSeenVersion` |
| Sugerencia | Indicador | Línea corta en el pie de página con orientación. | — |

## Consejos

- Tanto "Omitir esta versión" como "¡Entendido — 73!" escriben en `LastSeenVersion`. La diferencia práctica es la intención: "¡Entendido — 73!" reconoce las notas de la versión actual, mientras que "Omitir esta versión" descarta el aviso de actualización sin más acción.
- Para volver a leer las notas de la versión en cualquier momento, use `Help > What's New...`. Esto abre el cuadro de diálogo independientemente del valor guardado en `LastSeenVersion`.

## Solución de problemas

- **"Omitir esta versión" no es visible** — El botón solo aparece cuando AetherSDR ha detectado que hay una actualización disponible. Si no se detecta ninguna actualización, solo se muestra "¡Entendido — 73!". Este comportamiento es normal.

## Relacionado

- [Volver a leer las notas de la versión más tarde a través del menú Ayuda](re-read-release-notes-later-via-help-menu.md)
- [Abrir el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)

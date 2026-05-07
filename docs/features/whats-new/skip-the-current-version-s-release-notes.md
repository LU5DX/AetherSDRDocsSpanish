# Omitir las notas de la versión actual

Cuando AetherSDR detecta que hay una versión más reciente disponible, el cuadro de diálogo Novedades incluye una opción para evitar que vuelva a aparecer para esa versión. Utilice esta opción si ya ha visto las notas y no desea que el diálogo se muestre nuevamente en el próximo inicio.

## Antes de comenzar

- El botón "Omitir esta versión" solo aparece cuando hay una actualización disponible. Si no se detecta ninguna actualización, el botón no se muestra.
- El diálogo Novedades debe estar abierto. Se abre automáticamente después de un cambio de versión, o manualmente mediante `Help > What's New...`.

## Pasos

1. Abra el diálogo Novedades. Si aún no está en pantalla, vaya a `Help > What's New...`.
2. Confirme que el botón "Omitir esta versión" sea visible en el pie de página. Si está ausente, no se ha detectado ninguna actualización y la omisión no es aplicable.
3. Haga clic en "Omitir esta versión".

El diálogo se cierra. AetherSDR escribe la cadena de la versión actual en `LastSeenVersion` y la guarda. El diálogo Novedades no aparecerá automáticamente en el próximo inicio para esta versión.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Navegador de notas de versión | Vista HTML desplazable | Muestra las entradas de publicación entre la última versión vista y la versión actual. | — |
| "Got it — 73!" | Botón | Descarta el diálogo y marca la versión como vista. | `LastSeenVersion` |
| "Upgrade" | Botón | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga. | — |
| "Omitir esta versión" | Botón | Se muestra solo cuando hay una actualización disponible. Guarda la versión actual en `LastSeenVersion` y cierra el diálogo para que el aviso no vuelva a aparecer. | `LastSeenVersion` |
| Sugerencia | Indicador | Breve línea de pie de página con orientación. | — |

## Consejos

- "Omitir esta versión" y "Got it — 73!" ambos escriben en `LastSeenVersion`. La diferencia práctica es la intención: "Got it — 73!" reconoce las notas de la versión actual, mientras que "Omitir esta versión" descarta el aviso de actualización sin más acción.
- Para volver a leer las notas de la versión en cualquier momento, use `Help > What's New...`. Esto abre el diálogo independientemente del valor guardado de `LastSeenVersion`.

## Solución de problemas

- **"Omitir esta versión" no es visible** — El botón solo aparece cuando AetherSDR ha detectado que hay una actualización disponible. Si no se detecta ninguna actualización, solo se muestra "Got it — 73!". Este comportamiento es normal.

## Relacionados

- [Re-read release notes later via Help menu](re-read-release-notes-later-via-help-menu.md)
- [Open the upgrade flow for a newer build](open-the-upgrade-flow-for-a-newer-build.md)
- [Read what changed in the new version](read-what-changed-in-the-new-version.md)

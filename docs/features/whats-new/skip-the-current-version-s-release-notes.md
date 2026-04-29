# Omitir las notas de la versión actual

Cuando AetherSDR detecta que hay una versión más reciente disponible, el diálogo What's New incluye una opción para evitar que vuelva a aparecer para esa versión. Úsela si ya ha leído las notas y no desea que el diálogo se muestre de nuevo al siguiente inicio.

## Antes de comenzar

- El botón "Skip this version" aparece únicamente cuando hay una actualización disponible. Si no se detecta ninguna actualización, el botón no se muestra.
- El diálogo What's New debe estar abierto. Se abre automáticamente tras un cambio de versión, o manualmente mediante `Help > What's New...`.

## Pasos

1. Abra el diálogo What's New. Si no está visible en pantalla, vaya a `Help > What's New...`.
2. Confirme que el botón "Skip this version" es visible en el pie del diálogo. Si no aparece, no se ha detectado ninguna actualización y la opción de omisión no está disponible.
3. Haga clic en "Skip this version".

El diálogo se cierra. AetherSDR escribe la cadena de la versión actual en `LastSeenVersion` y la guarda. El diálogo What's New no aparecerá automáticamente en el siguiente inicio para esta versión.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Visor de notas de versión | Vista HTML desplazable | Muestra las entradas de versión entre la última versión vista y la versión actual. | — |
| "Got it — 73!" | Botón | Cierra el diálogo y marca la versión como vista. | `LastSeenVersion` |
| "Upgrade" | Botón | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga. | — |
| "Skip this version" | Botón | Se muestra solo cuando hay una actualización disponible. Guarda la versión actual en `LastSeenVersion` y cierra el diálogo para que el aviso no vuelva a aparecer. | `LastSeenVersion` |
| Hint | Indicador | Línea corta en el pie del diálogo con orientación al usuario. | — |

## Consejos

- Tanto "Skip this version" como "Got it — 73!" escriben en `LastSeenVersion`. La diferencia práctica es de intención: "Got it — 73!" confirma que se han leído las notas de la versión actual, mientras que "Skip this version" descarta el aviso de actualización sin realizar ninguna acción adicional.
- Para volver a leer las notas de versión en cualquier momento, use `Help > What's New...`. Esto abre el diálogo independientemente del valor guardado en `LastSeenVersion`.

## Solución de problemas

- **"Skip this version" no es visible** — El botón aparece únicamente cuando AetherSDR ha detectado que hay una actualización disponible. Si no se detecta ninguna actualización, solo se muestra "Got it — 73!". Este es el comportamiento esperado.

## Relacionado

- [Volver a leer las notas de versión más adelante mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Abrir el flujo de actualización para una versión más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)

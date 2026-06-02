# Saltar las notas de la versión actual

Cuando AetherSDR detecta que hay una versión más reciente disponible, el diálogo "What's New" incluye una opción para evitar que vuelva a aparecer para esa versión. Use esta opción si ya ha visto las notas y no desea que el diálogo se muestre nuevamente en el siguiente inicio.

## Antes de comenzar

- El botón "Skip this version" solo aparece cuando hay una actualización disponible. Si no se detecta ninguna actualización, el botón no se muestra.
- El diálogo "What's New" debe estar abierto. Se abre automáticamente después de un cambio de versión o manualmente a través de `Help > What's New...`.

## Pasos

1. Abra el diálogo "What's New". Si no está ya en pantalla, vaya a `Help > What's New...`.
2. Confirme que el botón "Skip this version" está visible en el pie de página. Si está ausente, no se ha detectado ninguna actualización y no corresponde saltar.
3. Haga clic en "Skip this version".

El diálogo se cierra. AetherSDR escribe la cadena de la versión actual en `LastSeenVersion` y la guarda. El diálogo "What's New" no aparecerá automáticamente en el siguiente inicio para esta versión.

## Funciones de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Navegador de notas de versión | Campo de texto | Vista HTML desplazable de las entradas de la versión. Muestra las notas de versión obtenidas de los lanzamientos de GitHub para la versión actual. Muestra los cambios entre la última versión vista y la versión actual. | — |
| "Got it — 73!" | Botón pulsador | Descarta el diálogo y marca la versión como vista. | `LastSeenVersion` |
| "Upgrade" | Botón pulsador | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga en `https://github.com/aethersdr/AetherSDR/releases/latest`. | — |
| "Skip this version" | Botón pulsador | Se muestra solo cuando hay una actualización disponible. Guarda la versión actual en `LastSeenVersion` y cierra el diálogo para que el recordatorio no vuelva a aparecer. | `LastSeenVersion` |
| Sugerencia | Indicador | Línea corta en el pie de página con orientación. | — |

## Consejos

- "Skip this version" y "Got it — 73!" ambos escriben en `LastSeenVersion`. La diferencia práctica radica en la intención: "Got it — 73!" reconoce las notas de la versión actual, mientras que "Skip this version" descarta la solicitud de actualización sin realizar ninguna acción adicional.
- Para volver a leer las notas de versión en cualquier momento, use `Help > What's New...`. Esto abre el diálogo independientemente del valor guardado de `LastSeenVersion`.
- Las notas de versión se obtienen de la API de GitHub. Si su red está limitada por GitHub (HTTP 403 con un mensaje de "límite de tasa"), el diálogo muestra un mensaje amigable sugiriendo que lo intente de nuevo más tarde o que lea las notas directamente en `github.com/aethersdr/AetherSDR/releases`.
- El navegador de notas de versión renderiza Markdown del cuerpo del lanzamiento de GitHub. Las referencias a problemas de GitHub (ej. `#123`) y las menciones a `@username` se convierten automáticamente en enlaces en los que se puede hacer clic.

## Solución de problemas

- **"Skip this version" no es visible** — El botón solo aparece cuando AetherSDR ha detectado que hay una actualización disponible. Si no se detecta ninguna actualización, solo se muestra "Got it — 73!". Este comportamiento es el esperado.
- **Las notas de versión no se cargan** — El diálogo obtiene las notas de versión de `api.github.com`. Si ve un mensaje de error, puede deberse a problemas de red o a la limitación de tasa de GitHub. Intente de nuevo más tarde o visite la página de lanzamientos directamente.

## Relacionado

- [Volver a leer las notas de versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Abrir el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)

# Abrir el flujo de actualización para una versión más reciente

Cuando una nueva versión de AetherSDR está disponible, el diálogo Qué hay de nuevo muestra un botón "Upgrade" que abre la página de descarga en su navegador. Esta página explica cómo llegar a ese botón.

## Antes de comenzar

- El botón "Upgrade" aparece únicamente cuando AetherSDR ha detectado que hay una versión más reciente disponible. Si no hay actualización disponible, el botón no se muestra.
- No se requiere conexión a la radio.

## Pasos

1. Abra `Help > What's New...`.
2. Revise las notas de la versión en el navegador desplazable en la parte superior del diálogo.
3. Haga clic en `Upgrade`.

AetherSDR abre la página de versiones de AetherSDR en su navegador web predeterminado y cierra el diálogo. La página de descarga ahora se aloja en `https://github.com/aethersdr/AetherSDR/releases/latest`.

## Función de cada control

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| Navegador de notas de versión | Vista HTML desplazable | Muestra las entradas de las versiones entre la última versión vista y la versión actual. Muestra como máximo las 5 versiones recientes. | — |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre `https://github.com/aethersdr/AetherSDR/releases/latest` y cierra el diálogo. | — |
| `Got it — 73!` | Botón | Descarta el diálogo y marca la versión actual como vista. | `LastSeenVersion` |
| `Skip this version` | Botón | Suprime el recordatorio de versión para esta versión y la marca como vista. | `LastSeenVersion` |
| Sugerencia | Indicador | Breve línea de pie con orientación. | — |

## Consejos

- Si cierra el diálogo con `Got it — 73!` en lugar de `Upgrade`, AetherSDR registra la versión actual en `LastSeenVersion` y no le volverá a preguntar por esta versión. Puede regresar al diálogo mediante `Help > What's New...`.
- Si hace clic en `Skip this version`, `LastSeenVersion` se establece en la versión actual y se suprime el aviso para esta versión, pero no se abre la página de descarga.

## Relacionado

- [Volver a leer las notas de versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Leer lo que cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Saltar las notas de la versión actual](skip-the-current-version-s-release-notes.md)

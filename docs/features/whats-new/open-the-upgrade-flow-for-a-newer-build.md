# Abrir el flujo de actualización para una compilación más reciente

Cuando una compilación más reciente de AetherSDR está disponible, el diálogo What's New muestra un botón "Upgrade" que abre la página de descarga en su navegador. Esta página explica cómo llegar a ese botón.

## Antes de comenzar

- El botón "Upgrade" aparece solo cuando AetherSDR ha detectado que hay una compilación más reciente disponible. Si no hay actualización disponible, el botón no se muestra.
- No se requiere conexión con la radio.

## Pasos

1. Abra `Help > What's New...`.
2. Revise las notas de la versión en el navegador desplazable en la parte superior del diálogo.
3. Haga clic en `Upgrade`.

AetherSDR abre la página de versiones de AetherSDR en su navegador web predeterminado y cierra el diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistente |
|---|---|---|---|
| Navegador de notas de versión | Vista HTML desplazable | Muestra las entradas de versión entre la última versión vista y la versión actual. Muestra un máximo de 5 versiones recientes. | — |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre la página de descarga y cierra el diálogo. | — |
| `Got it — 73!` | Botón | Descarta el diálogo y marca la versión actual como vista. | `LastSeenVersion` |
| `Skip this version` | Botón | Suprime el recordatorio de versión para esta versión y la marca como vista. | `LastSeenVersion` |
| Sugerencia | Indicador | Línea corta al pie con orientación. | — |

## Consejos

- Si cierra el diálogo con `Got it — 73!` en lugar de `Upgrade`, AetherSDR registra la versión actual en `LastSeenVersion` y no le volverá a preguntar por esta versión. Puede regresar al diálogo mediante `Help > What's New...`.
- Si hace clic en `Skip this version`, `LastSeenVersion` se establece en la versión actual y se suprime la notificación para esta versión, pero la página de descarga no se abre.

## Relacionado

- [Volver a leer las notas de versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)

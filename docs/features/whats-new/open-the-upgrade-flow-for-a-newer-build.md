# Abrir el flujo de actualización para una versión más reciente

Cuando hay una versión más reciente de AetherSDR disponible, el cuadro de diálogo What's New muestra un botón "Upgrade" que abre la página de descarga en su navegador. Esta página explica cómo acceder a ese botón.

## Antes de comenzar

- El botón "Upgrade" aparece únicamente cuando AetherSDR ha detectado que hay una versión más reciente disponible. Si no hay ninguna actualización disponible, el botón no se muestra.
- No se requiere conexión a la radio.

## Pasos

1. Abra `Help > What's New...`.
2. Revise las notas de la versión en el visor desplazable ubicado en la parte superior del cuadro de diálogo.
3. Haga clic en `Upgrade`.

AetherSDR abre la página de versiones de AetherSDR en su navegador web predeterminado y cierra el cuadro de diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Configuración persistida |
|---|---|---|---|
| Visor de notas de versión | Vista HTML desplazable | Muestra las entradas de versión entre la última versión vista y la versión actual. Muestra como máximo 5 versiones recientes. | — |
| `Upgrade` | Botón | Visible únicamente cuando hay una actualización disponible. Abre la página de descarga y cierra el cuadro de diálogo. | — |
| `Got it — 73!` | Botón | Cierra el cuadro de diálogo y marca la versión actual como vista. | `LastSeenVersion` |
| `Skip this version` | Botón | Suprime el recordatorio de versión para esta versión y la marca como vista. | `LastSeenVersion` |
| Hint | Indicador | Línea de pie de página breve con orientación. | — |

## Consejos

- Si cierra el cuadro de diálogo con `Got it — 73!` en lugar de `Upgrade`, AetherSDR registra la versión actual en `LastSeenVersion` y no volverá a notificarle sobre esta versión. Puede regresar al cuadro de diálogo en cualquier momento mediante `Help > What's New...`.
- Si hace clic en `Skip this version`, `LastSeenVersion` se establece en la versión actual y se suprime el aviso para esta versión, pero la página de descarga no se abre.

## Relacionados

- [Volver a leer las notas de versión más tarde desde el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)

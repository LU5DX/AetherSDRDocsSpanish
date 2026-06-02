# Abrir el flujo de actualización para una versión más reciente

Cuando hay disponible una versión más reciente de AetherSDR, el cuadro de diálogo "What's New" muestra un botón "Upgrade" que abre la página de descarga en su navegador. Esta página explica cómo llegar a ese botón.

## Antes de comenzar

- El botón "Upgrade" aparece solo cuando AetherSDR ha detectado que hay una versión más reciente disponible. Si no hay actualización disponible, el botón no se muestra.
- No se requiere conexión con la radio.

## Pasos

1. Abra `Help > What's New...`.
2. Revise las notas de la versión en el navegador desplazable en la parte superior del cuadro de diálogo.
3. Haga clic en `Upgrade`.

AetherSDR abre la página de versiones de AetherSDR en su navegador web predeterminado y cierra el cuadro de diálogo. La página de descarga se encuentra en `https://github.com/aethersdr/AetherSDR/releases/latest`.

## Función de cada control

| Control | Tipo | Comportamiento | Configuración persistente |
|---|---|---|---|
| Navegador de notas de versión | Campo de texto | Vista HTML desplazable de las entradas de la versión. Muestra los cambios entre la última versión vista y la versión actual. | — |
| `Got it — 73!` | Botón pulsador | Descarta el cuadro de diálogo y marca la versión como vista. | `LastSeenVersion` |
| `Upgrade` | Botón pulsador | Visible solo cuando hay una actualización disponible. Abre la página de descarga. | — |
| `Skip this version` | Botón pulsador | Omite el aviso de esta versión. | `LastSeenVersion` |
| Sugerencia | Indicador | Línea corta en el pie de página con orientación. | — |

## Consejos

- Si cierra el cuadro de diálogo con `Got it — 73!` en lugar de `Upgrade`, AetherSDR registra la versión actual en `LastSeenVersion` y no le volverá a preguntar por esta versión. Puede volver al cuadro de diálogo mediante `Help > What's New...`.
- Si hace clic en `Skip this version`, `LastSeenVersion` se establece en la versión actual y se suprime el aviso para esta versión, pero no se abre la página de descarga.

## Relacionados

- [Volver a leer las notas de la versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omitir las notas de la versión actual](skip-the-current-version-s-release-notes.md)

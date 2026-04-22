# Abrir el flujo de actualización para una versión más reciente

Cuando hay una versión más reciente de AetherSDR disponible, el cuadro de diálogo What's New — AetherSDR muestra un botón `Upgrade` que abre directamente la página de descarga. Esta página explica cómo llegar a ese botón.

## Antes de comenzar

- El botón `Upgrade` aparece únicamente cuando AetherSDR ha detectado que hay una versión más reciente disponible. Si no hay ninguna actualización pendiente, el botón no se muestra.
- No se requiere conexión a ningún radio.

## Pasos

1. Abra `Help > What's New...`.
2. En el cuadro de diálogo What's New — AetherSDR, revise las notas de la versión en el navegador de notas de versión.
3. Haga clic en `Upgrade`.

AetherSDR abre la página de versiones de AetherSDR en su navegador predeterminado y cierra el cuadro de diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Configuración persistente |
|---|---|---|---|
| Navegador de notas de versión | Vista desplazable | Muestra las notas de versión en HTML con formato para las versiones más recientes que `LastSeenVersion` hasta la versión actual. Muestra como máximo 5 versiones. | — |
| `Got it — 73!` | Botón | Cierra el cuadro de diálogo y marca la versión actual como vista. | `LastSeenVersion` |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre la página de descarga y cierra el cuadro de diálogo. | — |
| `Skip this version` | Botón | Visible solo cuando hay una actualización disponible. Suprime el aviso de actualización para la versión actual y cierra el cuadro de diálogo. | `LastSeenVersion` |
| Hint | Indicador | Muestra una línea de pie de página breve con orientación. | — |

## Consejos

- Si hace clic en `Skip this version` en lugar de `Upgrade`, AetherSDR escribe la versión actual en `LastSeenVersion` y no volverá a avisarle sobre esta versión. Puede regresar al cuadro de diálogo posteriormente mediante `Help > What's New...`, pero el botón `Upgrade` no reaparecerá para la versión omitida.
- Hacer clic en `Got it — 73!` también marca la versión como vista sin abrir la página de descarga.

## Relacionado

- [Releer las notas de versión más tarde desde el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)

# Omitir las notas de la versión actual

Cuando AetherSDR detecta una versión más reciente disponible, el diálogo What's New ofrece una forma de evitar que vuelva a aparecer para esa versión sin necesidad de leer las notas completas.

## Antes de comenzar

- El diálogo What's New debe estar abierto y mostrar una actualización disponible. El botón `Skip this version` aparece únicamente cuando hay una actualización disponible.

## Pasos

1. Abra `Help > What's New...` si el diálogo no está ya en pantalla.
2. Haga clic en `Skip this version`.

El diálogo se cierra y `LastSeenVersion` se actualiza a la versión actual. AetherSDR no volverá a mostrar las notas de esta versión en futuros inicios.

## Qué hace cada control

| Control | Comportamiento | Ajuste persistido |
|---|---|---|
| Navegador de notas | Vista HTML desplazable con las entradas entre la última versión vista y la versión actual. | — |
| `Got it — 73!` | Cierra el diálogo y marca la versión actual como vista. | `LastSeenVersion` |
| `Upgrade` | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga. | — |
| `Skip this version` | Se muestra solo cuando hay una actualización disponible. Escribe la versión actual en `LastSeenVersion` y cierra el diálogo, suprimiendo futuros avisos para esta versión. | `LastSeenVersion` |
| Hint | Línea de pie breve con orientación. Solo lectura. | — |

## Consejos

- Si omite una versión y más adelante desea leer sus notas, abra `Help > What's New...` en cualquier momento. Esa ruta muestra todas las entradas de la versión actual independientemente del valor de `LastSeenVersion`.

## Relacionado

- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Abrir el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Releer las notas más adelante desde el menú Help](re-read-release-notes-later-via-help-menu.md)

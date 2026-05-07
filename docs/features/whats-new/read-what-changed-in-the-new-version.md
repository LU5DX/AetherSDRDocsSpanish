# Lea qué cambió en la nueva versión

El cuadro de diálogo Novedades muestra las notas de la versión que aún no ha visto. Aparece automáticamente después de una actualización y también está disponible bajo demanda desde el menú Ayuda.

## Antes de comenzar

- AetherSDR debe estar instalado y en funcionamiento. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help > What's New...`.
2. Lea las notas de la versión en el **Navegador de notas de la versión** desplazable.
3. Haga clic en `Got it — 73!` para cerrar el cuadro de diálogo. AetherSDR registra la versión actual en `LastSeenVersion` para que el cuadro de diálogo no vuelva a aparecer para esta versión.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Navegador de notas de la versión | Vista HTML desplazable de las notas de la versión para versiones más recientes que la última versión vista, limitada a las cinco versiones más recientes. |
| `Got it — 73!` | Cierra el cuadro de diálogo y marca la versión actual como vista en `LastSeenVersion`. |
| `Upgrade` | Visible solo cuando hay una compilación más reciente disponible. Abre la página de descarga y cierra el cuadro de diálogo. |
| `Skip this version` | Visible solo cuando hay una compilación más reciente disponible. Escribe la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo sin actualizar. |
| Sugerencia | Línea de pie con una breve orientación. Solo lectura. |

## Consejos

- En la primera instalación, el cuadro de diálogo muestra solo las notas de la versión actual. En actualizaciones posteriores, muestra cada versión publicada desde la última versión vista, hasta un máximo de cinco versiones.
- Si no hay cambios nuevos disponibles, el navegador muestra "No new changes to report."
- Para volver a leer las notas en cualquier momento, use `Help > What's New...`. Esta ruta siempre muestra las notas completas de la versión actual, independientemente de `LastSeenVersion`.

## Relacionados

- [Re-read release notes later via Help menu](re-read-release-notes-later-via-help-menu.md)
- [Skip the current version's release notes](skip-the-current-version-s-release-notes.md)
- [Open the upgrade flow for a newer build](open-the-upgrade-flow-for-a-newer-build.md)

# Consulte los cambios de la nueva versión

El diálogo What's New muestra las notas de versión que usted aún no ha visto. Aparece automáticamente después de una actualización y también está disponible en cualquier momento desde el menú Help.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión a un radio.

## Pasos

1. Haga clic en `Help > What's New...`.
2. Lea las notas de versión en el **Release notes browser** desplazable.
3. Haga clic en `Got it — 73!` para cerrar el diálogo. AetherSDR registra la versión actual en `LastSeenVersion` para que el diálogo no vuelva a aparecer en esta versión.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Release notes browser | Vista HTML desplazable con las entradas de versiones más recientes que la última versión vista, limitada a las cinco versiones más recientes. |
| `Got it — 73!` | Cierra el diálogo y marca la versión actual como vista en `LastSeenVersion`. |
| `Upgrade` | Visible solo cuando hay una versión más reciente disponible. Abre la página de descarga y cierra el diálogo. |
| `Skip this version` | Visible solo cuando hay una versión más reciente disponible. Escribe la versión actual en `LastSeenVersion` y cierra el diálogo sin actualizar. |
| Hint | Línea de pie de página con orientación breve. Solo lectura. |

## Consejos

- En la primera instalación, el diálogo muestra únicamente las notas de la versión actual. En actualizaciones posteriores, muestra todas las versiones publicadas desde la última versión vista, hasta un máximo de cinco.
- Si no hay cambios nuevos disponibles, el navegador muestra "No new changes to report."
- Para volver a leer las notas en cualquier momento, use `Help > What's New...`. Esta ruta siempre muestra las notas completas de la versión actual, independientemente del valor de `LastSeenVersion`.

## Temas relacionados

- [Volver a leer las notas de versión desde el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abrir el flujo de actualización para una versión más reciente](open-the-upgrade-flow-for-a-newer-build.md)

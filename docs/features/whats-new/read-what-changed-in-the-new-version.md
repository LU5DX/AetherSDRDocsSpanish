# Lea qué cambió en la nueva versión

El cuadro de diálogo Novedades muestra las notas de la versión que aún no ha visto. Aparece automáticamente tras una actualización y también está disponible a demanda desde el menú Ayuda.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help > What's New...`.
2. Lea las notas de la versión en el **Explorador de notas de la versión** desplazable.
3. Haga clic en `Got it — 73!` para cerrar el cuadro de diálogo. AetherSDR registra la versión actual en `LastSeenVersion` para que el cuadro de diálogo no vuelva a aparecer para esta versión.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Explorador de notas de la versión | Vista HTML desplazable de las entradas de la versión para versiones más recientes que la última versión vista, limitada a las cinco versiones más recientes. |
| `Got it — 73!` | Cierra el cuadro de diálogo y marca la versión actual como vista en `LastSeenVersion`. |
| `Upgrade` | Visible solo cuando hay una compilación más reciente disponible. Abre `https://github.com/aethersdr/AetherSDR/releases/latest` en el navegador del sistema y cierra el cuadro de diálogo. |
| `Skip this version` | Visible solo cuando hay una compilación más reciente disponible. Escribe la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo sin actualizar. |
| Sugerencia | Línea de pie con orientación breve. Solo lectura. |

## Consejos

- En la primera instalación, el cuadro de diálogo muestra solo las notas de la versión actual. En actualizaciones posteriores, muestra cada versión publicada desde la última versión vista, hasta cinco versiones.
- Si no hay cambios nuevos disponibles, el explorador muestra "No hay cambios nuevos que informar".
- Para volver a leer las notas en cualquier momento, use `Help > What's New...`. Esta ruta siempre muestra las notas completas de la versión actual independientemente de `LastSeenVersion`.

## Relacionados

- [Vuelva a leer las notas de la versión más tarde mediante el menú Ayuda](re-read-release-notes-later-via-help-menu.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)

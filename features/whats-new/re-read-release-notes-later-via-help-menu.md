# Volver a leer las notas de la versión desde el menú Help

El diálogo What's New — AetherSDR se abre automáticamente tras una actualización de versión, pero puede volver a abrirlo en cualquier momento desde el menú Help para revisar las notas de la versión instalada.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio.

## Pasos

1. Haga clic en `Help > What's New...` en la barra de menú.
2. Desplace el visor de notas de la versión para leer las entradas.
3. Haga clic en `Got it — 73!` para cerrar el diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Visor de notas de la versión | Vista desplazable | Muestra las entradas de la versión actual en formato HTML con estilos. |
| `Got it — 73!` | Botón | Cierra el diálogo y marca la versión actual como vista en `LastSeenVersion`. |
| `Upgrade` | Botón | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga y cierra el diálogo. |
| `Skip this version` | Botón | Se muestra solo cuando hay una actualización disponible. Registra la versión actual en `LastSeenVersion` y cierra el diálogo sin actualizar. |
| Hint | Indicador | Línea de pie breve con texto de orientación. |

## Consejos

- Cuando se abre mediante `Help > What's New...`, el diálogo muestra todas las entradas de la versión instalada actualmente, independientemente del valor configurado en `LastSeenVersion`.
- El diálogo muestra como máximo las cinco entradas de versión más recientes cuando se abre automáticamente tras una actualización.

## Relacionado

- [Leer los cambios de la nueva versión](read-what-changed-in-the-new-version.md)
- [Abrir el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Omitir las notas de la versión actual](skip-the-current-version-s-release-notes.md)

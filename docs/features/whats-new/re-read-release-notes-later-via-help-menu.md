# Volver a leer las notas de la versión desde el menú Help

El diálogo What's New — AetherSDR se abre automáticamente tras una actualización, pero puede volver a abrirlo en cualquier momento desde el menú Help para revisar las notas de la versión actual.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio.

## Pasos

1. Haga clic en `Help > What's New...` en la barra de menús.
2. Desplácese por el navegador de notas de versión para leer los cambios.
3. Haga clic en `Got it — 73!` para cerrar el diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de versión | Vista desplazable | Muestra las entradas de la versión como HTML con formato. Al abrirse mediante `Help > What's New...`, muestra todas las entradas de la versión actual. |
| `Got it — 73!` | Botón | Cierra el diálogo y marca la versión actual como vista (persistida como `LastSeenVersion`). |
| `Upgrade` | Botón | Se muestra solo cuando hay una actualización disponible. Abre la página de descarga. |
| `Skip this version` | Botón | Se muestra solo cuando hay una actualización disponible. Registra la versión actual en `LastSeenVersion` y cierra el diálogo sin actualizar. |
| Hint | Indicador | Línea de pie con orientación breve. |

## Consejos

- Al abrir el diálogo mediante `Help > What's New...` siempre se muestran las notas completas de la versión actual, independientemente del valor configurado en `LastSeenVersion`. La versión que se abre automáticamente al iniciar la aplicación muestra solo las entradas más recientes que la última versión vista, con un límite de cinco versiones.

## Relacionados

- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omitir las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abrir el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)

# Volver a Leer las Notas de la Versión Más Tarde a Través del Menú Ayuda

El cuadro de diálogo Qué hay de nuevo — AetherSDR se abre automáticamente después de una actualización, pero puede volver a abrirlo en cualquier momento desde el menú Ayuda para revisar las notas de la versión actual.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help > What's New...` en la barra de menú.
2. Desplácese por el navegador de notas de la versión para leer los cambios.
3. Haga clic en `Got it — 73!` para cerrar el cuadro de diálogo.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de la versión | Vista desplazable | Muestra las entradas de la versión como HTML con estilo de tema oscuro. Cuando se abre a través de `Help > What's New...`, muestra todas las entradas de la versión actual. |
| `Got it — 73!` | Botón | Cierra el cuadro de diálogo y marca la versión actual como vista (se guarda como `LastSeenVersion`). |
| `Upgrade` | Botón | Solo se muestra cuando hay una actualización disponible. Abre la página de descarga en `https://github.com/aethersdr/AetherSDR/releases/latest` y cierra el cuadro de diálogo. |
| `Skip this version` | Botón | Solo se muestra cuando hay una actualización disponible. Registra la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo sin actualizar. |
| Sugerencia | Indicador | Línea de pie con orientación breve. |

## Consejos

- Al abrir el cuadro de diálogo a través de `Help > What's New...`, siempre se muestran las notas completas de la versión actual, independientemente del valor configurado en `LastSeenVersion`. La apertura automática al inicio solo muestra las entradas más recientes que la última versión vista, con un máximo de cinco versiones.
- El cuadro de diálogo obtiene las notas de la versión desde la API de GitHub. Si ve un error de límite de velocidad, intente de nuevo en unos minutos o visite `github.com/aethersdr/AetherSDR/releases` directamente en su navegador.

## Relacionado

- [Lea qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)

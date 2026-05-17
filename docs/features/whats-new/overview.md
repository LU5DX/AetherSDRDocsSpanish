# Novedades — Descripción general de AetherSDR

El cuadro de diálogo "Novedades" muestra las notas de la versión para las versiones de AetherSDR que aún no ha visto. Aparece automáticamente después de una actualización y también está disponible a demanda desde el menú Ayuda (Help).

## Cómo funciona

Cuando AetherSDR se inicia, compara la versión actual con el valor almacenado en `LastSeenVersion`. Si la versión actual es más reciente, el cuadro de diálogo se abre automáticamente y muestra las notas de la versión para cada versión entre la última versión vista y la actual, limitado a las cinco versiones más recientes. En una primera instalación, donde `LastSeenVersion` no tiene ningún valor almacenado, el cuadro de diálogo muestra solo las notas de la versión actual y lo saluda con un encabezado de bienvenida en lugar de un encabezado de cambio de versión.

Cuando abre el cuadro de diálogo a través de `Help > What's New...`, muestra todas las entradas para la versión actual independientemente de lo que contenga `LastSeenVersion`.

Las entradas de las versiones se muestran como HTML con estilo en un navegador desplazable. Cada entrada puede incluir un número de versión, una fecha de publicación, un título breve y una lista de cambios individuales. Los cambios están codificados por colores según la categoría:

| Categoría | Color del indicador |
|---|---|
| Función (Feature) | Azul |
| Corrección de error (Bug Fix) | Rojo anaranjado |
| Mejora (Improvement) | Verde |
| Infraestructura (Infrastructure) | Gris |

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de la versión | Área de texto desplazable | Muestra notas de la versión con estilo HTML para versiones más recientes que `LastSeenVersion`, hasta cinco versiones. |
| `Got it — 73!` | Botón | Cierra el cuadro de diálogo y marca la versión actual como vista actualizando `LastSeenVersion`. |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre la página de descarga de versiones de AetherSDR en https://github.com/aethersdr/AetherSDR/releases/latest y cierra el cuadro de diálogo. |
| `Skip this version` | Botón | Visible solo cuando hay una actualización disponible. Escribe la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo, suprimiendo el aviso de actualización para esta versión. |
| Sugerencia (Hint) | Indicador de pie de página | Muestra una línea breve de orientación debajo del encabezado. |

Los botones `Upgrade` y `Skip this version` aparecen solo cuando AetherSDR ha detectado que hay una compilación más reciente disponible.

## Consejos

- Para volver a leer las notas de la versión en cualquier momento sin activar un aviso de actualización, use `Help > What's New...`. Esta ruta siempre muestra las notas de la versión actual.
- El pie de página de Sugerencia (Hint) apunta al botón de bombilla en la barra de título para enviar informes de errores o ideas para funciones.

## Relacionado

- [Lea qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Vuelva a leer las notas de la versión más tarde a través del menú Help](re-read-release-notes-later-via-help-menu.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)

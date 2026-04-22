# Leer los cambios de la nueva versión

El diálogo What's New muestra las notas de versión que usted aún no ha visto. Se abre automáticamente tras una actualización y también está disponible bajo demanda desde el menú Help.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión a una radio.

## Pasos

1. Haga clic en `Help > What's New...`.
2. Lea las notas de versión en el navegador desplazable. Cada entrada está agrupada por versión y lista los cambios individuales marcados con puntos de colores (funciones nuevas, correcciones de errores, mejoras y cambios de infraestructura).
3. Haga clic en `Got it — 73!` para cerrar el diálogo. AetherSDR registra la versión actual en `LastSeenVersion` para que el diálogo no vuelva a aparecer automáticamente en esta versión.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de versión | Vista desplazable | Muestra las entradas de versión en HTML con formato para las versiones más recientes que `LastSeenVersion`, hasta las cinco más recientes. |
| `Got it — 73!` | Botón | Cierra el diálogo y marca la versión actual como vista en `LastSeenVersion`. |
| `Upgrade` | Botón | Visible solo cuando hay una compilación más nueva disponible. Abre la página de descarga de versiones de AetherSDR y cierra el diálogo. |
| `Skip this version` | Botón | Visible solo cuando hay una compilación más nueva disponible. Establece `LastSeenVersion` en la versión actual, suprimiendo el aviso de actualización para esta versión. |
| Hint | Indicador de pie | Muestra un mensaje de orientación breve debajo del encabezado. |

## Consejos

- En la primera instalación, el diálogo muestra únicamente las notas de la versión actual. Tras una actualización, muestra todas las versiones publicadas desde la última versión vista, con un límite de cinco entradas.
- Si cerró el diálogo antes de leerlo, puede volver a abrirlo en cualquier momento mediante `Help > What's New...`. Al usar el menú siempre se muestran las notas completas de la versión actual, independientemente del valor de `LastSeenVersion`.

## Relacionado

- [Volver a leer las notas de versión más tarde desde el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abrir el flujo de actualización para una compilación más nueva](open-the-upgrade-flow-for-a-newer-build.md)

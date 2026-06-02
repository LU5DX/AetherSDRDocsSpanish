# Lea qué cambió en la nueva versión

El cuadro de diálogo Qué hay de nuevo muestra las notas de la versión que aún no ha visto. Aparece automáticamente después de una actualización y también está disponible bajo demanda desde el menú Ayuda. Las notas de la versión se obtienen en vivo desde GitHub, por lo que el cuadro de diálogo requiere una conexión a Internet para mostrarlas.

## Antes de comenzar

- AetherSDR debe estar instalado y ejecutándose. No se requiere conexión de radio.
- Se requiere una conexión a Internet activa para obtener las notas de la versión desde GitHub.

## Pasos

1. Haga clic en `Help > What's New...`.
2. Lea las notas de la versión en el **Navegador de notas de versión** desplazable.
3. Haga clic en `Got it — 73!` para cerrar el cuadro de diálogo. AetherSDR registra la versión actual en `LastSeenVersion` para que el cuadro de diálogo no vuelva a aparecer para esta versión.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Navegador de notas de versión | Vista HTML desplazable de las entradas de notas de versión para versiones más recientes que la última versión vista. Las notas de la versión se obtienen en vivo desde la API de GitHub y se muestran como HTML con estilo, con referencias a problemas de GitHub (`#123`) y usuarios (`@username`) enlazadas. Si la API no está disponible o está limitada por tasa, se muestra un mensaje de error amigable con un enlace directo a la página de versiones de GitHub. |
| `Got it — 73!` | Cierra el cuadro de diálogo y marca la versión actual como vista en `LastSeenVersion`. |
| `Upgrade` | Visible solo cuando hay una compilación más reciente disponible. Abre la página de la última versión en GitHub en su navegador del sistema y cierra el cuadro de diálogo. |
| `Skip this version` | Visible solo cuando hay una compilación más reciente disponible. Escribe la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo sin actualizar. |
| Sugerencia | Línea de pie con orientación breve. Solo lectura. |

## Consejos

- En la primera instalación, el cuadro de diálogo muestra solo las notas de la versión actual. En actualizaciones posteriores, muestra todas las versiones publicadas desde la última versión vista.
- Las notas de la versión se muestran como HTML con estilo, con colores de soporte para encabezados, bloques de código, citas en bloque y enlaces.
- Las referencias a problemas de GitHub (por ejemplo, `#42`) se enlazan automáticamente al problema correspondiente en GitHub.
- Los nombres de usuario de GitHub (por ejemplo, `@username`) se enlazan automáticamente al perfil de usuario correspondiente.
- Si el cuadro de diálogo no puede alcanzar la API de GitHub, muestra un mensaje de error. Una causa común es el límite de tasa no autenticado de GitHub (60 solicitudes por hora por dirección IP). En ese caso, puede leer las notas de la versión directamente en `github.com/aethersdr/AetherSDR/releases`.
- Para volver a leer las notas en cualquier momento, use `Help > What's New...`. Esta ruta siempre muestra las notas completas de la versión actual, independientemente de `LastSeenVersion`.

## Relacionado

- [Vuelva a leer las notas de la versión más tarde a través del menú Ayuda](re-read-release-notes-later-via-help-menu.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)

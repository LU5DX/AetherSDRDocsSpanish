# Exportar un volcado de configuración para diagnóstico

Exporte un volcado de texto saneado de todo el almacén de configuración de AetherSDR, con los valores con forma de credencial enmascarados, para compartirlo con el soporte técnico o revisar su propia configuración.

## Antes de comenzar

- AetherSDR no necesita estar conectado a una radio para exportar la configuración.
- La exportación es una instantánea de diagnóstico, no una copia de seguridad; no se puede volver a importar para restaurar la configuración.

## Pasos

1. Abra el menú **Settings** y seleccione **Settings Browser...**.
2. Haga clic en **Export Sanitized…**.
3. Elija una ubicación y un nombre de archivo en el cuadro de diálogo y confirme.

El archivo de texto exportado contiene el árbol completo de configuración (claves de aplicación, la sección de estación y los documentos de funciones con alcance de radio) con cualquier valor con forma de credencial (contraseñas, tokens, claves de API) enmascarado.

## Qué hace cada control

| Control | Comportamiento |
| --- | --- |
| **Filter** | Búsqueda en vivo de subcadenas sin distinción de mayúsculas y minúsculas sobre las claves y los valores mostrados en el ámbito actual. |
| **Export Sanitized…** | Escribe el volcado de diagnóstico con secretos enmascarados en un archivo de texto. Los valores con forma de credencial se enmascaran. Solo salida de diagnóstico: no es una copia de seguridad restaurable. |

## Consejos

- La exportación no es, intencionalmente, una copia de seguridad. Para guardar o restaurar su configuración real, use `Profiles > Import/Export Profiles...` en su lugar.
- Los valores con forma de credencial se enmascaran a cualquier profundidad, por lo que los secretos nunca aparecen en el volcado, ni siquiera dentro de documentos JSON anidados.

## Solución de problemas

- **El botón de exportación está deshabilitado** — Si el árbol de configuración aún se está cargando, haga clic en **Refresh** y espere a que se complete, luego intente **Export Sanitized…** de nuevo.

## Relacionado

- [Descripción general del Settings Browser](overview.md)
- [Examinar toda la configuración de AetherSDR](browse-all-aethersdr-settings.md)
- [Editar un valor de configuración desde el Settings Browser](edit-a-settings-value-from-the-settings-browser.md)

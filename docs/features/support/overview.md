# Descripción general de Soporte y Diagnósticos

El diálogo Support & Diagnostics le ofrece un único lugar para controlar qué registra AetherSDR, inspeccionar el registro en tiempo real y enviar un informe de errores. Ábralo en cualquier momento desde `Help > Support...` — no se requiere conexión con la radio.

## Cómo funciona

El diálogo está dividido en tres áreas funcionales: controles de categorías de registro, un visor de registro en tiempo real y botones de acción para gestión de archivos e informes de errores.

**Grupo Diagnostic Logging**

Cada categoría de registro aparece como una casilla de verificación. Marcar una categoría habilita la salida de registro para ese subsistema; desmarcarla la silencia. No es necesario reiniciar AetherSDR para que los cambios surtan efecto. La ruta del archivo de registro y el tamaño actual del archivo se muestran como indicadores de solo lectura directamente debajo del grupo.

**Visor de registro**

El visor de registro es un área de texto desplazable y de solo lectura que muestra las entradas de registro más recientes (hasta 2.000 líneas). Muestra el contenido del archivo de registro activo en disco.

**Botones de acción**

La fila de botones en la parte inferior del diálogo gestiona todas las acciones de archivos e informes.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Casillas de categoría | Casilla (una por categoría) | Habilita o deshabilita el registro para ese subsistema específico. |
| Enable All | Botón | Activa todas las categorías de registro a la vez. |
| Disable All | Botón | Desactiva todas las categorías de registro a la vez. |
| Log path label | Indicador | Muestra la ruta completa al archivo de registro actual. |
| Log file size | Indicador | Muestra el tamaño actual del archivo de registro activo. |
| Log viewer | Área de texto desplazable | Muestra el texto de registro más reciente del archivo de registro (hasta 2.000 líneas). |
| Refresh | Botón | Recarga el archivo de registro en el visor. |
| Clear Log | Botón | Trunca (vacía) el archivo de registro actual. |
| Open Log Folder | Botón | Abre el directorio que contiene el archivo de registro en el explorador de archivos del sistema operativo. |
| Reset Settings | Botón | Restablece la configuración local de AetherSDR y la caché de wisdom de NR2 a los valores predeterminados, previa confirmación. La configuración de la radio almacenada en el equipo no se ve afectada. |
| File an Issue | Botón | Inicia el flujo de informe de errores asistido por IA: crea un paquete de soporte, copia un prompt de diagnóstico pre-completado en el portapapeles y le guía para enviar un issue en GitHub. |
| Close | Botón | Cierra el diálogo. |

## Consejos

- Habilite solo las categorías relevantes para el problema que está reproduciendo. Un registro más pequeño es más fácil de leer y compartir.
- Haga clic en Clear Log antes de reproducir un error para que el registro contenga únicamente la secuencia de eventos relevante.
- El paquete de soporte creado por File an Issue incluye sus registros y configuración. Adjúntelo al issue de GitHub arrastrándolo desde la carpeta que se abre automáticamente.
- Reset Settings elimina las preferencias locales de AetherSDR y la caché de wisdom de NR2. No modifica ninguna configuración almacenada en el FLEX-8600.

## Relacionado

- [Habilitar registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Ver el registro en tiempo real sin salir de la aplicación](view-the-live-log-without-leaving-the-app.md)
- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Abrir la carpeta de registros para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Enviar un informe de errores asistido por IA](file-an-ai-assisted-bug-report.md)
- [Restablecer la configuración de AetherSDR a los valores de fábrica](reset-aethersdr-settings-to-factory-defaults.md)

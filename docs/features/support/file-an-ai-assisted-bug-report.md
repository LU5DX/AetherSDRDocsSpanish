# Presentar un informe de error asistido por IA

Utilice el flujo de informe de error asistido por IA para obtener ayuda al redactar una incidencia de GitHub clara y completa. AetherSDR copia un prompt de diagnóstico prellenado —incluyendo su versión, sistema operativo y radio conectada— al portapapeles y luego lo guía a través de un asistente de IA y el formulario de incidencias de GitHub.

## Antes de comenzar

- Reproduzca el problema al menos una vez para poder describir lo ocurrido. Puede habilitar primero las categorías de registro para capturar más detalles. Consulte [Habilitar registro verboso para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md).
- Si desea adjuntar registros de diagnóstico, borre el registro y reproduzca el problema primero para que el registro contenga solo la salida relevante. Consulte [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).
- No se requiere una conexión de radio, pero si está conectado, el paquete incluirá automáticamente el modelo de radio, el firmware y la información de serie.

## Pasos

1. Haga clic en `Help > File an Issue` para abrir el diálogo AI-Assisted Bug Report e iniciar el flujo.
   AetherSDR crea un paquete de soporte (registros y configuraciones) y copia un prompt de diagnóstico al portapapeles. El prompt incluye su versión de AetherSDR, versión de Qt, sistema operativo e información de la radio si está conectada.
2. En el diálogo AI-Assisted Bug Report, haga clic en el servicio de IA que desea usar: `Claude`, `ChatGPT`, `Gemini`, `Grok` o `Perplexity`.
   Su navegador predeterminado se abre en ese servicio.
3. En el chat de IA, pegue el contenido del portapapeles.
4. Al final del prompt, reemplace el texto de marcador de posición con una descripción sencilla de lo que salió mal. Por ejemplo: "El waterfall se congela después de unos 10 minutos" o "El audio se corta cuando cambio de banda".
5. Envíe el prompt y espere a que la IA produzca un informe de error formateado.
6. Copie la salida de la IA.
7. Vuelva a AetherSDR. Si el diálogo sigue abierto, haga clic en `Submit Bug Report`.
   Su navegador abre el formulario de nueva incidencia de GitHub con la etiqueta `bug` preseleccionada, y la carpeta que contiene su paquete de soporte se abre en el explorador de archivos del sistema operativo.
8. Pegue el informe de error de la IA en el formulario de incidencia de GitHub.
9. Arrastre el archivo del paquete de soporte desde la carpeta que se abrió al formulario de incidencia de GitHub para adjuntarlo.
10. Envíe la incidencia en GitHub.

## Qué hace cada control

| Control                               | Qué hace                                                                                                                                                        | Notas                                                                                                                                     |
|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `Claude`                              | Abre `https://claude.ai/new` en su navegador.                                                                                                                   |                                                                                                                                           |
| `ChatGPT`                             | Abre `https://chat.openai.com/` en su navegador.                                                                                                                |                                                                                                                                           |
| `Gemini`                              | Abre `https://gemini.google.com/` en su navegador.                                                                                                              |                                                                                                                                           |
| `Grok`                                | Abre `https://grok.x.ai/` en su navegador.                                                                                                                      |                                                                                                                                           |
| `Perplexity`                          | Abre `https://www.perplexity.ai/` en su navegador.                                                                                                              |                                                                                                                                           |
| `Submit Bug Report`                   | Abre el formulario de nueva incidencia de GitHub (preetiquetado como `bug`) y abre la carpeta del paquete de soporte para adjuntarlo arrastrándolo.              |                                                                                                                                           |
| Instructions (report-an-issue how-to) | Bloque de texto enriquecido que señala al usuario a Help > File an Issue para informar errores una vez que se hayan habilitado las categorías de registro relevantes y se haya reproducido el problema. | Nuevo en v26.8.4: los botones 'Reset Settings' y 'File an Issue' se eliminaron de este diálogo (ahora están directamente en el menú Help). |
| Close                                 | Cierra el diálogo.                                                                                                                                              |                                                                                                                                           |

## Consejos

- El prompt de diagnóstico indica a la IA que redacte el informe de error completo en una sola respuesta sin hacer preguntas de seguimiento. Solo necesita añadir su descripción al final del prompt pegado.
- El paquete de soporte se crea cuando inicia el flujo `File an Issue`, antes de interactuar con cualquier IA. Si reproduce el problema después de iniciar el flujo, cierre el diálogo, borre el registro, reproduzca el error y luego inicie el flujo nuevamente para que el paquete contenga registros recientes.
- Si cierra el diálogo AI-Assisted Bug Report y necesita informar la incidencia más tarde, inicie un nuevo flujo `File an Issue` y haga clic en `Submit Bug Report` para reabrir el formulario de GitHub y la carpeta del paquete.

## Solución de problemas

- **Aparece la advertencia "Failed to create support bundle"** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permiso de escritura en su directorio de inicio y que haya espacio disponible en disco, luego intente nuevamente.
- **El navegador no se abre al hacer clic en un botón de IA** — Verifique que haya un navegador predeterminado configurado en su sistema operativo. En Linux, compruebe que `xdg-open` esté instalado y asociado con un manejador HTTP.
- **La información de la radio muestra "not connected" en el prompt** — La radio no estaba conectada cuando inició el flujo `File an Issue`. Añada manualmente el modelo de radio y la versión de firmware en el chat de IA después de pegar el prompt.

## Relacionados

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Habilitar registro verboso para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)

---

# Referencia de Support & Diagnostics

El diálogo Support & Diagnostics (`Help > Support...`) proporciona visualización de registros, control de categorías de registro y acceso a herramientas de soporte. El diálogo recuerda su tamaño y posición entre sesiones.

## Controles de registro

| Control | Qué hace |
|---|---|
| Category checkboxes | Habilita o deshabilita el registro por categoría. Una casilla por categoría de registro. |
| Enable All | Activa todas las categorías de registro. |
| Disable All | Desactiva todas las categorías de registro. |
| Log path label | Muestra la ruta actual del archivo de registro. |
| Log viewer | Vista desplazable del texto de registro más reciente. |
| Refresh | Recarga el archivo de registro. |
| Clear Log | Trunca el archivo de registro actual. |
| Open Log Folder | Abre el directorio de registros en el explorador de archivos del sistema operativo. |

## Herramientas de soporte

| Control | Qué hace |
|---|---|
| Instructions (report-an-issue how-to) | Bloque de texto enriquecido que señala al usuario a Help > File an Issue para informar errores una vez que se hayan habilitado las categorías de registro relevantes y se haya reproducido el problema. |
| Close | Cierra el diálogo. |

## Indicadores

| Indicador | Qué muestra |
|---|---|
| Log file size | Tamaño actual del archivo de registro activo. |

## Elementos de menú relacionados

| Elemento de menú | Qué hace |
|---|---|
| `Help > File an Issue` | Inicia el flujo AI-Assisted Bug Report. |
| `Help > Reset Settings` | Elimina las configuraciones específicas de la aplicación de AetherSDR, escribe una copia de seguridad y cierra la aplicación inmediatamente. |

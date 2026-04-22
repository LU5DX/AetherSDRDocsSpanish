# Crear un informe de error asistido por IA

AetherSDR puede preparar un aviso de diagnóstico — pre-rellenado con su versión, sistema operativo e información del radio — que usted pega en un asistente de IA para generar un informe de error de GitHub con estructura clara. Utilice esta función cuando necesite ayuda para describir un problema antes de enviarlo en GitHub.

## Antes de comenzar

- Reproduzca o anote los detalles del problema que desea reportar.
- Opcionalmente, limpie y vuelva a capturar el registro justo antes de enviarlo para que contenga solo datos relevantes. Consulte [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).
- No se requiere una conexión de radio, pero si está conectado, el paquete incluirá automáticamente el modelo de su radio, la versión de firmware y su indicativo.

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo **Support & Diagnostics**.
2. Haga clic en **File an Issue**.
   AetherSDR crea un paquete de soporte (registros y configuraciones) y copia un aviso de diagnóstico en su portapapeles. El aviso viene pre-rellenado con su versión de AetherSDR, versión de Qt, sistema operativo e información del radio.
3. En el diálogo **AI-Assisted Bug Report** que aparece, haga clic en el servicio de IA que desea utilizar: **Claude**, **ChatGPT**, **Gemini**, **Grok** o **Perplexity**. Su navegador predeterminado abrirá ese servicio.
4. En la ventana de chat de la IA, pegue el contenido del portapapeles (el aviso ya está allí desde el paso 2).
5. Al final del aviso, reemplace el texto de marcador de posición con una descripción de lo que salió mal — por ejemplo, qué estaba haciendo, qué ocurrió y qué esperaba que sucediera.
6. Envíe el mensaje y espere a que la IA genere un informe de error de GitHub con formato.
7. Copie la respuesta de la IA.
8. Regrese al diálogo **AI-Assisted Bug Report** (que permanece abierto en AetherSDR) y haga clic en **Submit Bug Report**. AetherSDR abre el formulario de nuevo issue de GitHub en su navegador y abre la carpeta que contiene su paquete de soporte.
9. Pegue la respuesta de la IA en el formulario del issue de GitHub.
10. Arrastre el archivo del paquete de soporte desde la carpeta que se abrió hasta el formulario del issue de GitHub para adjuntarlo.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Claude** | Abre `https://claude.ai/new` en su navegador. |
| **ChatGPT** | Abre `https://chat.openai.com/` en su navegador. |
| **Gemini** | Abre `https://gemini.google.com/` en su navegador. |
| **Grok** | Abre `https://grok.x.ai/` en su navegador. |
| **Perplexity** | Abre `https://www.perplexity.ai/` en su navegador. |
| **Submit Bug Report** | Abre el formulario de nuevo issue de GitHub (pre-etiquetado como `bug`) y abre la carpeta del paquete de soporte para adjuntarlo mediante arrastrar y soltar. |
| **Close** | Cierra el diálogo sin enviar el informe. |

## Consejos

- El aviso de diagnóstico instruye a la IA para que redacte el informe completo en una sola respuesta sin hacer preguntas de seguimiento. Proporcione a la IA el mayor detalle posible en su descripción — cuanto más específico sea, mejor será el resultado.
- Si hizo clic en un botón de IA y luego cerró el diálogo **AI-Assisted Bug Report** antes de enviarlo, haga clic en **File an Issue** nuevamente para volver a abrirlo y use **Submit Bug Report**. Se creará un nuevo paquete de soporte.
- Si está conectado a su radio cuando hace clic en **File an Issue**, el paquete incluye automáticamente el modelo del radio, número de serie, versión de firmware y dirección IP. Si no está conectado, conéctese primero y luego haga clic en **File an Issue** para incluir esos datos.
- Active el registro detallado (verbose logging) para el subsistema correspondiente antes de reproducir el error, de modo que el paquete de soporte contenga información útil. Consulte [Activar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md).

## Solución de problemas

- **Aparece la advertencia "Failed to create support bundle."** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permiso de escritura en su directorio de datos de usuario. El aviso de diagnóstico sigue copiado en su portapapeles, por lo que puede continuar con los pasos de IA y enviar el issue manualmente sin el archivo adjunto.
- **No se abre ningún navegador al hacer clic en un botón de IA** — Verifique que su sistema operativo tenga configurado un navegador predeterminado y que pueda abrir URLs externas. En Linux, asegúrese de que `xdg-open` funcione correctamente.
- **La información del radio muestra "not connected" en el aviso** — AetherSDR no estaba conectado al radio cuando hizo clic en **File an Issue**. Conéctese mediante `Settings > Connect to Radio...` y haga clic en **File an Issue** nuevamente si los datos del radio son relevantes para su informe.

## Relacionado

- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Activar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)
- [Descripción general de Support & Diagnostics](overview.md)

# Registrar un informe de error con asistencia de IA

Use el flujo de informe de error con asistencia de IA para obtener ayuda al redactar un problema de GitHub claro y completo. AetherSDR copia un prompt de diagnóstico prellenado — que incluye su versión, sistema operativo y radio conectada — al portapapeles, y luego lo guía a través de un asistente de IA y el formulario de problemas de GitHub.

## Antes de comenzar

- Reproduzca el problema al menos una vez para poder describir lo que ocurrió.
- Si desea adjuntar registros de diagnóstico, limpie el registro y reproduzca el problema primero, de modo que el registro contenga solo la salida relevante. Consulte [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).
- No se requiere una conexión de radio, pero si está conectado, el paquete incluirá automáticamente el modelo de radio, el firmware y la información del número de serie.

## Pasos

1. Haga clic en `Help > Support...` para abrir el diálogo Support & Diagnostics.
2. Haga clic en `File an Issue`.
   AetherSDR crea un paquete de soporte (registros y configuración) y copia un prompt de diagnóstico al portapapeles. El prompt incluye su versión de AetherSDR, versión de Qt, sistema operativo e información de radio si está conectado.
3. En el diálogo AI-Assisted Bug Report que aparece, haga clic en el servicio de IA que desea usar: `Claude`, `ChatGPT`, `Gemini`, `Grok` o `Perplexity`.
   Su navegador predeterminado se abre en ese servicio.
4. En el chat de IA, pegue el contenido del portapapeles.
5. Al final del prompt, reemplace el texto de marcador de posición con una descripción sencilla de lo que salió mal. Por ejemplo: "The waterfall freezes after about 10 minutes" o "Audio cuts out when I switch bands."
6. Envíe el prompt y espere a que la IA genere un informe de error con formato.
7. Copie la respuesta de la IA.
8. Regrese a AetherSDR. Si el diálogo sigue abierto, haga clic en `Submit Bug Report`.
   Su navegador abre el formulario de nuevo problema de GitHub con la etiqueta `bug` preseleccionada, y la carpeta que contiene su paquete de soporte se abre en el explorador de archivos del sistema operativo.
9. Pegue el informe de error de la IA en el formulario de problema de GitHub.
10. Arrastre el archivo del paquete de soporte desde la carpeta que se abrió hasta el formulario de problema de GitHub para adjuntarlo.
11. Envíe el problema en GitHub.

## Qué hace cada control

| Control | Qué hace |
|---|---|
| `Claude` | Abre `https://claude.ai/new` en su navegador. |
| `ChatGPT` | Abre `https://chat.openai.com/` en su navegador. |
| `Gemini` | Abre `https://gemini.google.com/` en su navegador. |
| `Grok` | Abre `https://grok.x.ai/` en su navegador. |
| `Perplexity` | Abre `https://www.perplexity.ai/` en su navegador. |
| `Submit Bug Report` | Abre el formulario de nuevo problema de GitHub (etiquetado previamente con `bug`) y abre la carpeta del paquete de soporte para adjuntarlo mediante arrastrar y soltar. |

## Consejos

- El prompt de diagnóstico indica a la IA que redacte el informe de error completo en una sola respuesta, sin hacer preguntas de seguimiento. Solo necesita agregar su descripción al final del prompt pegado.
- El paquete de soporte se crea cuando hace clic en `File an Issue`, antes de interactuar con cualquier IA. Si reproduce el problema después de abrir el diálogo, haga clic en `Close`, limpie el registro, reproduzca el error y luego inicie el flujo nuevamente para que el paquete contenga registros actualizados.
- Si cierra el diálogo AI-Assisted Bug Report y necesita registrar el problema más tarde, haga clic en `Submit Bug Report` desde una nueva sesión de `File an Issue` para reabrir el formulario de GitHub y la carpeta del paquete.

## Solución de problemas

- **Aparece el aviso "Failed to create support bundle"** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permiso de escritura en su directorio personal y que haya espacio en disco disponible, luego inténtelo de nuevo.
- **El navegador no se abre al hacer clic en un botón de IA** — Verifique que haya un navegador predeterminado configurado en su sistema operativo. En Linux, compruebe que `xdg-open` esté instalado y asociado a un manejador HTTP.
- **La información de radio muestra "not connected" en el prompt** — La radio no estaba conectada cuando hizo clic en `File an Issue`. Agregue el modelo de radio y la versión de firmware manualmente en el chat de IA después de pegar el prompt.

## Relacionados

- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Activar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](open-the-log-folder-to-grab-multiple-files.md)

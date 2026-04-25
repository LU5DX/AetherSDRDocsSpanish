# Registrar un error con asistencia de IA

Use el flujo de registro de errores con asistencia de IA para obtener ayuda al redactar un problema de GitHub claro y completo. AetherSDR copia en el portapapeles un prompt de diagnóstico prellenado —que incluye su versión, sistema operativo y radio conectado— y lo guía a través de un asistente de IA y el formulario de problemas de GitHub.

## Antes de comenzar

- Reproduzca el problema al menos una vez para poder describir lo que ocurrió.
- Si desea adjuntar registros de diagnóstico, limpie el registro y reproduzca el problema primero, de modo que el registro contenga solo la salida relevante. Consulte [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).
- No se requiere una conexión de radio; sin embargo, si está conectado, el paquete incluirá automáticamente el modelo de radio, el firmware y la información de serie.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Haga clic en `File an Issue`.
   AetherSDR crea un paquete de soporte (registros y configuración) y copia un prompt de diagnóstico en el portapapeles. El prompt incluye su versión de AetherSDR, versión de Qt, sistema operativo e información de radio si está conectado.
3. En el cuadro de diálogo AI-Assisted Bug Report que aparece, haga clic en el servicio de IA que desea usar: `Claude`, `ChatGPT`, `Gemini`, `Grok` o `Perplexity`.
   Su navegador predeterminado se abre en ese servicio.
4. En el chat de IA, pegue el contenido del portapapeles.
5. Al final del prompt, reemplace el texto de marcador de posición con una descripción sencilla de lo que salió mal. Por ejemplo: "The waterfall freezes after about 10 minutes" o "Audio cuts out when I switch bands."
6. Envíe el prompt y espere a que la IA produzca un informe de error con formato.
7. Copie la respuesta de la IA.
8. Regrese a AetherSDR. Si el cuadro de diálogo sigue abierto, haga clic en `Submit Bug Report`.
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
| `Submit Bug Report` | Abre el formulario de nuevo problema de GitHub (etiquetado previamente como `bug`) y abre la carpeta del paquete de soporte para adjuntarla mediante arrastrar y soltar. |

## Consejos

- El prompt de diagnóstico instruye a la IA para que redacte el informe de error completo en una sola respuesta, sin hacer preguntas de seguimiento. Solo necesita agregar su descripción al final del prompt pegado.
- El paquete de soporte se crea al hacer clic en `File an Issue`, antes de interactuar con cualquier IA. Si reproduce el problema después de abrir el cuadro de diálogo, haga clic en `Close`, limpie el registro, reproduzca el error y luego inicie el flujo de nuevo para que el paquete contenga registros actualizados.
- Si cierra el cuadro de diálogo AI-Assisted Bug Report y necesita registrar el problema más tarde, haga clic en `Submit Bug Report` desde una nueva sesión de `File an Issue` para volver a abrir el formulario de GitHub y la carpeta del paquete.

## Solución de problemas

- **Aparece la advertencia "Failed to create support bundle"** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permisos de escritura en su directorio de inicio y que haya espacio disponible en disco; luego intente de nuevo.
- **El navegador no se abre al hacer clic en un botón de IA** — Verifique que haya un navegador predeterminado configurado en su sistema operativo. En Linux, compruebe que `xdg-open` esté instalado y asociado a un manejador HTTP.
- **La información de radio muestra "not connected" en el prompt** — La radio no estaba conectada cuando hizo clic en `File an Issue`. Agregue el modelo de radio y la versión de firmware manualmente en el chat de IA después de pegar el prompt.

## Relacionado

- [Limpiar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Habilitar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Abrir la carpeta de registros para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)

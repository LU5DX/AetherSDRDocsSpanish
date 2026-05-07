# Presentar un informe de error asistido por IA

Utilice el flujo de informe de errores asistido por IA para recibir ayuda al redactar un issue de GitHub claro y completo. AetherSDR copia un mensaje de diagnóstico previamente completado (que incluye su versión, sistema operativo y radio conectada) al portapapeles y luego lo guía a través de un asistente de IA y el formulario de issue de GitHub.

## Antes de comenzar

- Reproduzca el problema al menos una vez para poder describir lo que ocurrió.
- Si desea adjuntar registros de diagnóstico, borre el registro y reproduzca el problema primero para que el registro contenga solo la salida relevante. Consulte [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md).
- No es necesaria una conexión de radio, pero si está conectado, el paquete incluirá automáticamente el modelo de radio, el firmware y la información de serie.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Haga clic en `File an Issue`.
   AetherSDR crea un paquete de soporte (registros y configuración) y copia un mensaje de diagnóstico al portapapeles. El mensaje incluye su versión de AetherSDR, versión de Qt, sistema operativo e información de la radio si está conectada.
3. En el cuadro de diálogo AI-Assisted Bug Report que aparece, haga clic en el servicio de IA que desea utilizar: `Claude`, `ChatGPT`, `Gemini`, `Grok` o `Perplexity`.
   Su navegador predeterminado se abrirá en ese servicio.
4. En el chat de IA, pegue el contenido del portapapeles.
5. Al final del mensaje, reemplace el texto de marcador de posición con una descripción sencilla de lo que salió mal. Por ejemplo: "El waterfall se congela después de unos 10 minutos" o "El audio se corta cuando cambio de banda".
6. Envíe el mensaje y espere a que la IA produzca un informe de error formateado.
7. Copie la salida de la IA.
8. Vuelva a AetherSDR. Si el cuadro de diálogo aún está abierto, haga clic en `Submit Bug Report`.
   Su navegador abre el formulario de nuevo issue de GitHub con la etiqueta `bug` preseleccionada, y la carpeta que contiene su paquete de soporte se abre en el explorador de archivos del sistema operativo.
9. Pegue el informe de error de la IA en el formulario de issue de GitHub.
10. Arrastre el archivo del paquete de soporte desde la carpeta que se abrió al formulario de issue de GitHub para adjuntarlo.
11. Envíe el issue en GitHub.

## Qué hace cada control

| Control | Qué hace |
|---|---|
| `Claude` | Abre `https://claude.ai/new` en su navegador. |
| `ChatGPT` | Abre `https://chat.openai.com/` en su navegador. |
| `Gemini` | Abre `https://gemini.google.com/` en su navegador. |
| `Grok` | Abre `https://grok.x.ai/` en su navegador. |
| `Perplexity` | Abre `https://www.perplexity.ai/` en su navegador. |
| `Submit Bug Report` | Abre el formulario de nuevo issue de GitHub (preetiquetado como `bug`) y abre la carpeta del paquete de soporte para adjuntarlo arrastrando y soltando. |

## Consejos

- El mensaje de diagnóstico indica a la IA que redacte el informe de error completo en una sola respuesta sin hacer preguntas de seguimiento. Solo necesita agregar su descripción al final del mensaje pegado.
- El paquete de soporte se crea cuando hace clic en `File an Issue`, antes de interactuar con cualquier IA. Si reproduce el problema después de abrir el cuadro de diálogo, haga clic en `Close`, borre el registro, reproduzca el error y luego inicie el flujo nuevamente para que el paquete contenga registros recientes.
- Si cierra el cuadro de diálogo AI-Assisted Bug Report y necesita presentar el issue más tarde, haga clic en `Submit Bug Report` desde una nueva sesión de `File an Issue` para volver a abrir el formulario de GitHub y la carpeta del paquete.

## Solución de problemas

- **Aparece la advertencia "Failed to create support bundle"** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permiso de escritura en su directorio de inicio y que haya espacio disponible en el disco, luego intente nuevamente.
- **El navegador no se abre al hacer clic en un botón de IA** — Verifique que haya un navegador predeterminado configurado en su sistema operativo. En Linux, compruebe que `xdg-open` esté instalado y asociado con un manejador HTTP.
- **La información de la radio muestra "not connected" en el mensaje** — La radio no estaba conectada cuando hizo clic en `File an Issue`. Agregue el modelo de radio y la versión de firmware manualmente en el chat de IA después de pegar el mensaje.

## Relacionado

- [Clear the log before reproducing a bug](clear-the-log-before-reproducing-a-bug.md)
- [Enable verbose logging for a specific subsystem](enable-verbose-logging-for-a-specific-subsystem.md)
- [Open the log folder to grab multiple files](open-the-log-folder-to-grab-multiple-files.md)

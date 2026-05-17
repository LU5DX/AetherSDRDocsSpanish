# Presentar un informe de error asistido por IA

Utilice el flujo de informe de error asistido por IA para obtener ayuda al redactar un issue claro y completo en GitHub. AetherSDR copia un mensaje de diagnóstico precargado (que incluye su versión, sistema operativo y radio conectada) al portapapeles, luego lo guía a través de un asistente de IA y el formulario de issue de GitHub.

## Antes de comenzar

- Reproduzca el problema al menos una vez para poder describir lo que ocurrió.
- Si desea adjuntar registros de diagnóstico, borre el registro y reproduzca el problema primero para que el registro contenga solo la información relevante. Consulte [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md).
- No es necesaria una conexión de radio, pero si está conectado, el paquete incluirá automáticamente el modelo de radio, firmware e información de serie.

## Pasos

1. Haga clic en `Help > Support...` para abrir el cuadro de diálogo Support & Diagnostics.
2. Haga clic en `File an Issue`.
   AetherSDR crea un paquete de soporte (registros y configuración) y copia un mensaje de diagnóstico al portapapeles. El mensaje incluye su versión de AetherSDR, versión de Qt, sistema operativo e información de la radio si está conectada.
3. En el cuadro de diálogo AI-Assisted Bug Report que aparece, haga clic en el servicio de IA que desea usar: `Claude`, `ChatGPT`, `Gemini`, `Grok` o `Perplexity`.
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
| `Submit Bug Report` | Abre el formulario de nuevo issue de GitHub (con la etiqueta `bug` preasignada) y abre la carpeta del paquete de soporte para adjuntarlo mediante arrastrar y soltar. |

## Consejos

- El mensaje de diagnóstico instruye a la IA para que redacte el informe de error completo en una sola respuesta sin hacer preguntas de seguimiento. Solo necesita agregar su descripción al final del mensaje pegado.
- El paquete de soporte se crea cuando hace clic en `File an Issue`, antes de interactuar con cualquier IA. Si reproduce el problema después de abrir el cuadro de diálogo, haga clic en `Close`, borre el registro, reproduzca el error y luego inicie el flujo nuevamente para que el paquete contenga registros recientes.
- Si cierra el cuadro de diálogo AI-Assisted Bug Report y necesita presentar el issue más tarde, haga clic en `Submit Bug Report` desde una nueva sesión de `File an Issue` para reabrir el formulario de GitHub y la carpeta del paquete.

## Solución de problemas

- **Aparece la advertencia "Failed to create support bundle"** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permiso de escritura en su directorio de inicio y que haya espacio disponible en el disco, luego intente nuevamente.
- **El navegador no se abre al hacer clic en un botón de IA** — Verifique que haya un navegador predeterminado configurado en su sistema operativo. En Linux, compruebe que `xdg-open` esté instalado y asociado con un controlador HTTP.
- **La información de la radio muestra "not connected" en el mensaje** — La radio no estaba conectada cuando hizo clic en `File an Issue`. Agregue el modelo de radio y la versión de firmware manualmente en el chat de IA después de pegar el mensaje.

## Relacionado

- [Borrar el registro antes de reproducir un error](clear-the-log-before-reproducing-a-bug.md)
- [Habilitar el registro detallado para un subsistema específico](enable-verbose-logging-for-a-specific-subsystem.md)
- [Abrir la carpeta de registros para obtener varios archivos](open-the-log-folder-to-grab-multiple-files.md)

---

# Referencia de Support & Diagnostics

El cuadro de diálogo Support & Diagnostics (`Help > Support...`) proporciona visualización de registros, control de categorías de registro y acceso a herramientas de soporte.

## Controles de registro

| Control | Qué hace |
|---|---|
| Casillas de verificación de categoría | Activa o desactiva el registro por categoría. Una casilla por categoría de registro. |
| Enable All | Activa todas las categorías de registro. |
| Disable All | Desactiva todas las categorías de registro. |
| Etiqueta de ruta de registro | Muestra la ruta actual del archivo de registro. |
| Visor de registro | Vista desplazable del texto de registro más reciente. |
| Refresh | Vuelve a cargar el archivo de registro. |
| Clear Log | Trunca el archivo de registro actual. |
| Open Log Folder | Abre el directorio de registro en el explorador de archivos del sistema operativo. |

## Herramientas de soporte

| Control | Qué hace |
|---|---|
| Reset Settings | Restablece la configuración de AetherSDR a los valores predeterminados (con confirmación). |
| File an Issue | Inicia el flujo de AI-Assisted Bug Report. |
| Close | Cierra el cuadro de diálogo. |

## Indicadores

| Indicador | Qué muestra |
|---|---|
| Log file size | Tamaño actual del archivo de registro activo. |

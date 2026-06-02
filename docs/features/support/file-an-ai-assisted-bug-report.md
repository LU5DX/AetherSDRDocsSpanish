# Presentar un informe de error asistido por IA

Utilice el flujo de informe de errores asistido por IA para obtener ayuda al redactar un issue claro y completo en GitHub. AetherSDR copia un mensaje de diagnóstico previamente completado —que incluye su versión, sistema operativo y radio conectada— al portapapeles y luego lo guía a través de un asistente de IA y el formulario de issue de GitHub.

## Antes de comenzar

- Reproduzca el problema al menos una vez para poder describir lo que ocurrió.
- Si desea adjuntar registros de diagnóstico, limpie el registro y reproduzca el problema primero para que el registro contenga únicamente la información relevante. Consulte [Limpiar el registro antes de reproducir un error](limpiar-el-registro-antes-de-reproducir-un-error.md).
- No es necesaria una conexión de radio, pero si está conectado, el paquete incluirá automáticamente el modelo de radio, el firmware y la información de serie.

## Pasos

1. Haga clic en `Ayuda > Soporte...` para abrir el cuadro de diálogo de Soporte y Diagnóstico.
2. Haga clic en `Informar un problema`.
   AetherSDR crea un paquete de soporte (registros y configuraciones) y copia un mensaje de diagnóstico al portapapeles. El mensaje incluye su versión de AetherSDR, versión de Qt, sistema operativo e información de la radio si está conectada.
3. En el cuadro de diálogo de Informe de Errores Asistido por IA que aparece, haga clic en el servicio de IA que desea utilizar: `Claude`, `ChatGPT`, `Gemini`, `Grok` o `Perplexity`.
   Su navegador predeterminado se abrirá con ese servicio.
4. En el chat de IA, pegue el contenido del portapapeles.
5. Al final del mensaje, reemplace el texto de marcador de posición con una descripción sencilla de lo que salió mal. Por ejemplo: "El waterfall se congela después de unos 10 minutos" o "El audio se corta cuando cambio de banda".
6. Envíe el mensaje y espere a que la IA genere un informe de error formateado.
7. Copie la salida de la IA.
8. Regrese a AetherSDR. Si el cuadro de diálogo sigue abierto, haga clic en `Enviar Informe de Error`.
   Su navegador abre el formulario de nuevo issue de GitHub con la etiqueta `bug` preseleccionada y la carpeta que contiene su paquete de soporte se abre en el explorador de archivos del sistema operativo.
9. Pegue el informe de error de la IA en el formulario de issue de GitHub.
10. Arrastre el archivo del paquete de soporte desde la carpeta que se abrió al formulario de issue de GitHub para adjuntarlo.
11. Envíe el issue en GitHub.

## Funcionalidad de cada control

| Control | Qué hace |
|---|---|
| `Claude` | Abre `https://claude.ai/new` en su navegador. |
| `ChatGPT` | Abre `https://chat.openai.com/` en su navegador. |
| `Gemini` | Abre `https://gemini.google.com/` en su navegador. |
| `Grok` | Abre `https://grok.x.ai/` en su navegador. |
| `Perplexity` | Abre `https://www.perplexity.ai/` en su navegador. |
| `Enviar Informe de Error` | Abre el formulario de nuevo issue de GitHub (previamente etiquetado como `bug`) y abre la carpeta del paquete de soporte para adjuntarlo mediante arrastrar y soltar. |

## Consejos

- El mensaje de diagnóstico indica a la IA que redacte el informe de error completo en una sola respuesta sin hacer preguntas de seguimiento. Solo necesita agregar su descripción al final del mensaje pegado.
- El paquete de soporte se crea cuando hace clic en `Informar un problema`, antes de interactuar con cualquier IA. Si reproduce el problema después de abrir el cuadro de diálogo, haga clic en `Cerrar`, limpie el registro, reproduzca el error y luego inicie el flujo nuevamente para que el paquete contenga registros actualizados.
- Si cierra el cuadro de diálogo de Informe de Errores Asistido por IA y necesita reportar el problema más tarde, haga clic en `Enviar Informe de Error` desde una nueva sesión de `Informar un problema` para reabrir el formulario de GitHub y la carpeta del paquete.

## Solución de problemas

- **Aparece la advertencia "No se pudo crear el paquete de soporte"** — AetherSDR no pudo escribir el paquete en el disco. Verifique que tenga permisos de escritura en su directorio de inicio y que haya suficiente espacio en disco, luego intente nuevamente.
- **El navegador no se abre al hacer clic en un botón de IA** — Verifique que haya un navegador predeterminado configurado en su sistema operativo. En Linux, compruebe que `xdg-open` esté instalado y asociado con un controlador HTTP.
- **La información de la radio muestra "no conectado" en el mensaje** — La radio no estaba conectada cuando hizo clic en `Informar un problema`. Agregue el modelo de radio y la versión del firmware manualmente en el chat de IA después de pegar el mensaje.

## Relacionados

- [Limpiar el registro antes de reproducir un error](limpiar-el-registro-antes-de-reproducir-un-error.md)
- [Habilitar el registro detallado para un subsistema específico](habilitar-el-registro-detallado-para-un-subsistema-especifico.md)
- [Abrir la carpeta de registros para obtener múltiples archivos](abrir-la-carpeta-de-registros-para-obtener-multiples-archivos.md)

---

# Referencia de Soporte y Diagnóstico

El cuadro de diálogo de Soporte y Diagnóstico (`Ayuda > Soporte...`) proporciona visualización de registros, control de categorías de registro y acceso a herramientas de soporte.

## Controles de registro

| Control | Qué hace |
|---|---|
| Casillas de verificación de categoría | Activa o desactiva el registro por categoría. Una casilla por categoría de registro. |
| Habilitar Todo | Activa todas las categorías de registro. |
| Deshabilitar Todo | Desactiva todas las categorías de registro. |
| Etiqueta de ruta de registro | Muestra la ruta actual del archivo de registro. |
| Visor de registros | Vista desplazable del texto de registro más reciente. |
| Actualizar | Vuelve a cargar el archivo de registro. |
| Limpiar Registro | Trunca el archivo de registro actual. |
| Abrir Carpeta de Registros | Abre el directorio de registros en el explorador de archivos del sistema operativo. |

## Herramientas de soporte

| Control | Qué hace |
|---|---|
| Restablecer Configuración | Restablece la configuración de AetherSDR a los valores predeterminados (con confirmación). |
| Informar un Problema | Inicia el flujo de Informe de Errores Asistido por IA. |
| Cerrar | Cierra el cuadro de diálogo. |

## Indicadores

| Indicador | Qué muestra |
|---|---|
| Tamaño del archivo de registro | Tamaño actual del archivo de registro activo. |

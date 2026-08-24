# Consultar los atajos de caracteres para prosignos

El panel CWX incluye una leyenda de prosignos integrada que muestra qué caracteres de teclado debe escribir para enviar prosignos CW comunes. Utilice esta referencia al componer un búfer de texto o al escribir una macro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El panel CWX debe estar abierto. Aparece automáticamente cuando el slice TX está en modo CW, CWL o CWU.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior.
2. Localice la leyenda de prosignos mostrada en la vista Setup. Es un indicador de solo lectura — no se requiere interacción.
3. Anote los atajos de caracteres mostrados (=, +, (, &, $) y utilícelos al escribir en el área de texto de envío o al editar una macro.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Leyenda de prosignos | Indicador (solo lectura) | Muestra los atajos de teclado para prosignos CW comunes: `=`, `+`, `(`, `&`, `$`. | — |
| Área de texto de envío | Campo de texto | Escriba aquí su mensaje CW, usando atajos de prosignos cuando sea necesario. Presione Enter para enviar. | — |
| Editores de macro F1 … F12 | Campos de texto | Ingrese atajos de prosignos directamente en el texto de la macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |
| Speed: | Spinbox | Velocidad de CW en WPM. | `CwxSpeedWpm` |
| Delay: | Spinbox | Retardo entre macros. | `CwxDelay` |
| QSK | Botón de alternancia | Habilita QSK (break-in completo). | `CwxQsk` |
| Send (vista) | Botón pulsador | Muestra el área de envío en vivo con historial y campo de texto. | — |
| Live (vista) | Botón pulsador | Muestra la vista de envío en vivo. | — |
| Setup (vista) | Botón pulsador | Muestra el editor de macros y la configuración de QSK. | — |
| Desplazamiento del historial de envío | Indicador | Muestra los búferes de envío anteriores con resaltado de caracteres. | — |
| F1 … F12 (macros) | Botones pulsadores | Envía la macro preescrita para esa tecla de función. | `CwxMacro_F1` – `CwxMacro_F12` |

## Cómo interactúan Send y Live

En la versión 0.9.2.1, el comportamiento del botón **Send** cambió. Su acción ahora depende de si **Live** está activado:

- **Live apagado:** Al hacer clic en **Send**, el búfer actual se envía de inmediato, exactamente como en versiones anteriores.
- **Live activado:** Al hacer clic en **Send**, primero se desactiva el modo Live y el panel vuelve a la vista de envío normal. El búfer *no* se vuelve a transmitir. Esto evita que los caracteres que ya se enviaron uno por uno en modo Live se envíen nuevamente.

El botón **Live** ahora es de alternancia. Al hacer clic en él por segunda vez, el modo Live se desactiva sin salir de la vista de envío. El estado del botón permanece sincronizado con el modelo — si algo fuera del panel cambia el estado de Live, el botón se actualiza para coincidir.

Al hacer clic en **Setup**, el modo Live siempre se desactiva antes de mostrar la vista del editor de macros.

## Acciones con los globos del historial de envío

El área de desplazamiento del historial de envío muestra cada búfer enviado como un globo con una marca de tiempo. Puede interactuar con estos globos con el botón derecho:

- **Haga clic derecho en un globo del historial** para abrir un menú contextual con dos opciones:
  - **Resend:** Envía el mismo texto nuevamente como si lo hubiera escrito de nuevo. El texto aparece como un nuevo globo en el historial.
  - **Clear History:** Elimina todos los globos del historial del área de desplazamiento. Esta acción no se puede deshacer.

## Abortar una transmisión con Escape

Al presionar **Escape** durante una transmisión CW se aborta el proceso de envío. Cuando aborta una transmisión:

- Todos los caracteres no enviados del búfer actual se muestran con formato tachado en el globo del historial.
- Los caracteres ya enviados aparecen normalmente, sin tachado.
- La marca de tiempo del globo muestra cuándo se inició la transmisión.

Esta distinción visual le ayuda a identificar qué partes de un mensaje se transmitieron realmente frente a las que se cancelaron a mitad del envío.

## Atajos de teclado en el panel CWX

El panel CWX registra las teclas F1 a F12 y la tecla Escape como atajos de toda la aplicación. Los atajos F1–F12 se habilitan o deshabilitan según el modo del slice TX, administrados por MainWindow. Se activan independientemente de si el panel CWX está visible, siempre que el slice TX esté en modo CW, CWL o CWU. Cuando el slice TX cambia a un modo diferente (como SSB), los atajos se deshabilitan automáticamente para evitar conflictos con otros paneles como el panel DVK.

En la versión 26.8.4, la detección del modo CW se consolidó en un único asistente compartido (`isCwMode()`). Esto garantiza que todos los paneles, incluido el panel CWX, utilicen exactamente la misma lista de modos CW. Las comprobaciones específicas del sitio anteriores para `"CW"` y `"CWL"` se han reemplazado, de modo que si el conjunto de modos CW de su radio incluye variantes adicionales, el panel CWX ahora las reconoce de manera consistente.

- **F1 – F12:** Envía la cadena de macro correspondiente.
- **Escape:** Aborta la transmisión CW actual. Los caracteres no enviados aparecen con tachado en el globo del historial.

## Consejos

- Los atajos de prosignos funcionan tanto en el área de texto de envío en vivo como en los editores de macros de teclas F. Escríbalos como cualquier otro carácter.
- Para enviar una macro que contenga un prosigno, edite la cadena de la macro en la vista Setup usando los mismos caracteres de atajo y luego actívela con la tecla F correspondiente desde la vista de envío.
- Si cambia del modo Live al modo Send y desea transmitir el contenido del búfer, desactive Live primero (haga clic en **Live** para alternarlo), y luego haga clic en **Send**.
- Los atajos de teclado F1–F12 están activos siempre que el slice TX esté en un modo CW, independientemente de si el panel CWX está visible. Si no puede activar una macro con una tecla F, verifique que el slice TX esté en modo CW, CWL o CWU.
- Para reenviar un búfer anterior, haga clic derecho en el globo del historial y seleccione **Resend**. El texto original se conserva y se envía nuevamente como una nueva entrada en el historial.
- Para borrar el historial de envío, haga clic derecho en cualquier globo y seleccione **Clear History**, o haga clic derecho en el fondo del área de historial si no hay globos presentes.
- Si aborta una transmisión con Escape, el globo del historial muestra la parte no enviada con formato tachado para obtener una retroalimentación visual clara.

## Relacionado

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

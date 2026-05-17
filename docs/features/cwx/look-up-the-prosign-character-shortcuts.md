# Consultar los atajos de caracteres de prosignos

El panel CWX incluye una leyenda integrada de prosignos que muestra qué caracteres del teclado debe escribir para enviar prosignos CW comunes. Utilice esta referencia al redactar un búfer escrito o al escribir una macro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El panel CWX debe estar abierto. Aparece automáticamente cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior.
2. Localice la leyenda de prosignos que se muestra en la vista Setup. Es un indicador de solo lectura; no requiere interacción.
3. Observe los atajos de caracteres mostrados (=, +, (, &, $) y utilícelos al escribir en el área de texto de envío o al editar una macro.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Leyenda de prosignos | Indicador (solo lectura) | Muestra los atajos de teclado para prosignos CW comunes: `=`, `+`, `(`, `&`, `$`. | — |
| Área de texto de envío | Campo de texto | Escriba aquí su mensaje CW, utilizando atajos de prosignos cuando sea necesario. Pulse Enter para enviar. | — |
| Editores de macro F1 … F12 | Campos de texto | Introduzca atajos de prosignos directamente en el texto de la macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |
| Velocidad: | Spinbox | Velocidad CW en WPM. | `CwxSpeedWpm` |
| Retardo: | Spinbox | Retardo entre macros. | `CwxDelay` |
| QSK | Botón de alternancia | Activa QSK (interrupción completa). | `CwxQsk` |
| Send (vista) | Botón pulsador | Muestra el área de envío en vivo con historial y campo de texto. | — |
| Live (vista) | Botón pulsador | Muestra la vista de envío en vivo. | — |
| Setup (vista) | Botón pulsador | Muestra el editor de macros y la configuración de QSK. | — |
| Desplazamiento del historial de envío | Indicador | Muestra búferes de envío anteriores con resaltado de caracteres. | — |
| F1 … F12 (macros) | Botones pulsadores | Envía la macro preescrita para esa tecla de función. | `CwxMacro_F1` – `CwxMacro_F12` |

## Cómo interactúan Send y Live

En la versión v0.9.2.1, el comportamiento del botón **Send** cambió. Ahora su acción depende de si **Live** está activado o no:

- **Live está desactivado:** Al hacer clic en **Send** se envía el búfer actual inmediatamente, exactamente como en versiones anteriores.
- **Live está activado:** Al hacer clic en **Send**, primero se desactiva el modo Live y el panel vuelve a la vista de envío normal. El búfer *no* se retransmite. Esto evita que los caracteres que ya se enviaron uno por uno en modo Live se envíen nuevamente.

El botón **Live** ahora es de alternancia. Hacer clic en él por segunda vez desactiva el modo Live sin salir de la vista de envío. El estado del botón se sincroniza con el modelo; si algo fuera del panel cambia el estado Live, el botón se actualiza para coincidir.

Hacer clic en **Setup** siempre desactiva el modo Live antes de mostrar la vista del editor de macros.

## Acciones de las burbujas del historial de envío

El área de desplazamiento del historial de envío muestra cada búfer enviado como una burbuja con una marca de tiempo. Puede interactuar con estas burbujas usando el clic derecho:

- **Haga clic derecho en una burbuja del historial** para abrir un menú contextual con dos opciones:
  - **Resend:** Envía el mismo texto nuevamente como si lo hubiera escrito de nuevo. El texto aparece como una nueva burbuja en el historial.
  - **Clear History:** Elimina todas las burbujas del historial del área de desplazamiento. Esta acción no se puede deshacer.

## Atajos de teclado en el panel CWX

El panel CWX registra las teclas F1 a F12 y la tecla Escape como atajos de toda la aplicación. Los atajos F1–F12 se habilitan o deshabilitan según el modo del slice activo, gestionados por MainWindow. Se activan independientemente de si el panel CWX está visible, siempre que el slice activo esté en modo CW, CWL o CWU. Cuando el slice activo cambia a un modo diferente (como SSB), los atajos se deshabilitan automáticamente para evitar conflictos con otros paneles como el panel DVK.

- **F1 – F12:** Envía la cadena de macro correspondiente.
- **Escape:** Borra el búfer de envío actual.

## Consejos

- Los atajos de prosignos funcionan tanto en el área de texto de envío en vivo como en los editores de macros de las teclas F. Escríbalos como lo haría con cualquier otro carácter.
- Para enviar una macro que contenga un prosigno, edite la cadena de la macro en la vista Setup utilizando los mismos atajos de caracteres y luego actívala con la tecla F correspondiente desde la vista Send.
- Si cambia del modo Live al modo Send y desea transmitir el contenido del búfer, desactive Live primero (haga clic en **Live** para desactivarlo) y luego haga clic en **Send**.
- Los atajos de teclado F1–F12 están activos siempre que el slice activo esté en modo CW, independientemente de si el panel CWX está visible. Si no puede activar una macro con una tecla F, verifique que el slice activo esté en modo CW, CWL o CWU.
- Para reenviar un búfer anterior, haga clic derecho en la burbuja del historial y seleccione **Resend**. El texto original se conserva y se envía nuevamente como una nueva entrada en el historial.
- Para borrar el historial de envío, haga clic derecho en cualquier burbuja y seleccione **Clear History**, o haga clic derecho en el fondo del área del historial si no hay burbujas presentes.

## Relacionado

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

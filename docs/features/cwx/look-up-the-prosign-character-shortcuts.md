# Consultar los atajos de caracteres para prosignos

El panel CWX incluye una leyenda integrada de prosignos que muestra qué caracteres del teclado debe escribir para enviar prosignos CW comunes. Use esta referencia al redactar un búfer de texto o escribir una macro.

## Antes de empezar

- AetherSDR debe estar conectado a la radio.
- El panel CWX debe estar abierto. Aparece automáticamente cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior.
2. Localice la leyenda de prosignos que se muestra en la vista Setup. Es un indicador de solo lectura: no se requiere ninguna interacción.
3. Observe los atajos de caracteres mostrados (=, +, (, &, $) y úselos al escribir en el área de texto de envío o al editar una macro.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Prosigns legend | Indicador (solo lectura) | Muestra los atajos de teclado para prosignos CW comunes: `=`, `+`, `(`, `&`, `$`. | — |
| Send text area | Campo de texto | Escriba aquí su mensaje CW, usando atajos de prosignos cuando sea necesario. Pulse Enter para enviar. | — |
| F1 … F12 macro editors | Campos de texto | Ingrese atajos de prosignos directamente en el texto de la macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |
| Speed: | Spinbox | Velocidad CW en WPM. | `CwxSpeedWpm` |
| Delay: | Spinbox | Retardo entre macros. | `CwxDelay` |
| QSK | Botón de alternancia | Activa QSK (full break-in). | `CwxQsk` |
| Send (view) | Botón pulsador | Muestra el área de envío en vivo con historial y campo de texto. | — |
| Live (view) | Botón pulsador | Muestra la vista de envío en vivo. | — |
| Setup (view) | Botón pulsador | Muestra el editor de macros y la configuración de QSK. | — |
| Send history scroll | Indicador | Muestra búferes de envío anteriores con resaltado de caracteres. | — |
| F1 … F12 (macros) | Botones pulsadores | Envía la macro predefinida para esa tecla de función. | `CwxMacro_F1` – `CwxMacro_F12` |

## Cómo interactúan Send y Live

En la versión v0.9.2.1, el comportamiento del botón **Send** cambió. Su acción ahora depende de si **Live** está activado:

- **Live está desactivado:** Al hacer clic en **Send** se envía el búfer actual inmediatamente, igual que en versiones anteriores.
- **Live está activado:** Al hacer clic en **Send**, primero se desactiva el modo Live y se devuelve el panel a la vista de envío normal. El búfer *no* se retransmite. Esto evita que los caracteres que ya se enviaron uno por uno en modo Live se vuelvan a enviar.

El botón **Live** ahora es de alternancia. Al hacer clic en él una segunda vez, el modo Live se desactiva sin salir de la vista de envío. El estado del botón se mantiene sincronizado con el modelo; si algo externo al panel cambia el estado de Live, el botón se actualiza para reflejarlo.

Al hacer clic en **Setup**, el modo Live siempre se desactiva antes de mostrar la vista del editor de macros.

## Atajos de teclado en el panel CWX

El panel CWX registra las teclas F1 a F12 y la tecla Escape como atajos de toda la aplicación. Estos atajos **solo están activos mientras el panel CWX está visible**. Cuando oculta el panel o cambia a otro panel (como el panel DVK), los atajos se desactivan automáticamente para evitar conflictos con otros paneles que puedan usar las mismas teclas.

- **F1 – F12:** Envían la cadena de macro correspondiente.
- **Escape:** Borra el búfer de envío actual.

## Consejos

- Los atajos de prosignos funcionan tanto en el área de texto de envío en vivo como en los editores de macros de teclas F. Escríbalos como cualquier otro carácter.
- Para enviar una macro que contenga un prosigno, edite la cadena de macro en la vista Setup usando los mismos caracteres de atajo, luego actíVela con la tecla F correspondiente desde la vista Send.
- Si cambia del modo Live al modo Send y desea transmitir el contenido del búfer, desactive Live primero (haga clic en **Live** para desactivarlo) y luego haga clic en **Send**.
- Los atajos de teclado F1–F12 y Escape solo están activos cuando el panel CWX está visible. Si no puede activar una macro con una tecla F, asegúrese de que el panel CWX sea el panel activo.

## Relacionados

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

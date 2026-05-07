# Consultar los atajos de caracteres para prosignos

El panel CWX incluye una leyenda integrada de prosignos que muestra qué caracteres del teclado debe escribir para enviar prosignos CW comunes. Utilice esta referencia al redactar un búfer escrito o al escribir una macro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El panel CWX debe estar abierto. Aparece automáticamente cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior.
2. Localice la leyenda de prosignos que se muestra en la vista Setup. Es un indicador de solo lectura — no requiere interacción.
3. Anote los atajos de caracteres mostrados (=, +, (, &, $) y utilícelos al escribir en el área de texto de envío o al editar una macro.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Leyenda de prosignos | Indicador (solo lectura) | Muestra los atajos de teclado para prosignos CW comunes: `=`, `+`, `(`, `&`, `$`. | — |
| Área de texto de envío | Campo de texto | Escriba aquí su mensaje CW, usando atajos de prosignos cuando sea necesario. Presione Enter para enviar. | — |
| Editores de macros F1 … F12 | Campos de texto | Ingrese atajos de prosignos directamente en el texto de la macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |

## Cómo interactúan Send y Live

En v0.9.2.1, el comportamiento del botón **Send** cambió. Su acción ahora depende de si **Live** está activado:

- **Live está desactivado:** Al hacer clic en **Send** se envía el búfer actual inmediatamente, exactamente como en versiones anteriores.
- **Live está activado:** Al hacer clic en **Send** primero se desactiva el modo Live y se devuelve el panel a la vista de envío normal. El búfer *no* se re-transmite. Esto evita que los caracteres que ya fueron enviados uno por uno en modo Live se envíen nuevamente.

El botón **Live** ahora es un conmutador. Al hacer clic en él por segunda vez se desactiva el modo Live sin salir de la vista de envío. El estado del botón se mantiene sincronizado con el modelo — si algo fuera del panel cambia el estado de Live, el botón se actualiza para coincidir.

Al hacer clic en **Setup** siempre se desactiva el modo Live antes de mostrar la vista del editor de macros.

## Consejos

- Los atajos de prosignos funcionan tanto en el área de texto de envío en vivo como en los editores de macros de teclas F. Escríbalos como lo haría con cualquier otro carácter.
- Para enviar una macro que contenga un prosigno, edite la cadena de la macro en la vista Setup usando los mismos caracteres de atajo, luego actívela con la tecla F correspondiente desde la vista Send.
- Si cambia del modo Live al modo Send y desea transmitir el contenido del búfer, desactive Live primero (haga clic en **Live** para desactivarlo) y luego haga clic en **Send**.

## Relacionado

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

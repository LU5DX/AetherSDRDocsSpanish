# Consultar los atajos de caracteres para prosigns

El panel CWX incluye una leyenda de prosigns integrada que muestra qué caracteres del teclado se deben escribir para enviar los prosigns de CW más comunes. Use esta referencia al componer un búfer de texto o escribir una macro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El panel CWX debe estar abierto. Aparece automáticamente cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior.
2. Localice la leyenda de prosigns que se muestra en la vista Setup. Es un indicador de solo lectura; no se requiere ninguna interacción.
3. Tome nota de los atajos de caracteres mostrados (=, +, (, &, $) y utilícelos al escribir en el área de texto de envío o al editar una macro.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Leyenda de prosigns | Indicador (solo lectura) | Muestra los atajos de teclado para los prosigns de CW más comunes: `=`, `+`, `(`, `&`, `$`. | — |
| Área de texto de envío | Campo de texto | Escriba aquí su mensaje CW, usando los atajos de prosigns donde sea necesario. Presione Enter para enviar. | — |
| Editores de macros F1 … F12 | Campos de texto | Ingrese los atajos de prosigns directamente en el texto de la macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |

## Cómo interactúan Send y Live

En la versión 0.9.2.1 el comportamiento del botón **Send** cambió. Su acción ahora depende de si **Live** está activo en ese momento:

- **Live está desactivado:** Al hacer clic en **Send** se envía el búfer actual de inmediato, exactamente como en versiones anteriores.
- **Live está activado:** Al hacer clic en **Send** primero se desactiva el modo Live y el panel regresa a la vista de envío normal. El búfer *no* se retransmite. Esto evita que los caracteres que ya fueron enviados uno a uno en modo Live se transmitan de nuevo.

El botón **Live** es ahora un conmutador (toggle). Hacer clic en él una segunda vez desactiva el modo Live sin salir de la vista de envío. El estado del botón se mantiene sincronizado con el modelo: si algo externo al panel cambia el estado de Live, el botón se actualiza en consecuencia.

Hacer clic en **Setup** siempre desactiva el modo Live antes de mostrar la vista del editor de macros.

## Consejos

- Los atajos de prosigns funcionan tanto en el área de texto de envío en vivo como en los editores de macros de teclas F. Escríbalos como cualquier otro carácter.
- Para enviar una macro que contenga un prosign, edite la cadena de la macro en la vista Setup usando los mismos caracteres de atajo y, luego, actívela con la tecla F correspondiente desde la vista Send.
- Si cambia del modo Live al modo Send y desea transmitir el contenido del búfer, primero desactive Live (haga clic en **Live** para desactivarlo) y luego haga clic en **Send**.

## Relacionados

- [Enviar un búfer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

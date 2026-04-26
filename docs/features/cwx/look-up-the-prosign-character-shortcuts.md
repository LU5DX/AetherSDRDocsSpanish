# Consultar los atajos de caracteres para prosignos

El panel CWX incluye una leyenda integrada de prosignos que muestra qué caracteres del teclado se deben escribir para enviar los prosignos de CW más comunes. Use esta referencia al componer un búfer de texto o al escribir una macro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El panel CWX debe estar abierto. Aparece automáticamente cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior.
2. Localice la leyenda de prosignos que se muestra en la vista Setup. Es un indicador de solo lectura — no se requiere ninguna interacción.
3. Tome nota de los atajos de caracteres que se muestran (=, +, (, &, $) y utilícelos al escribir en el área de texto de envío o al editar una macro.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Leyenda de prosignos | Indicador (solo lectura) | Muestra los atajos de teclado para los prosignos de CW más comunes: `=`, `+`, `(`, `&`, `$`. | — |
| Área de texto de envío | Campo de texto | Escriba aquí su mensaje de CW, utilizando los atajos de prosignos donde sea necesario. Presione Enter para enviar. | — |
| Editores de macros F1 … F12 | Campos de texto | Ingrese los atajos de prosignos directamente en el texto de la macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |

## Consejos

- Los atajos de prosignos funcionan tanto en el área de texto de envío en vivo como en los editores de macros de teclas F. Escríbalos como cualquier otro carácter.
- Para enviar una macro que contenga un prosigno, edite la cadena de texto de la macro en la vista Setup usando los mismos caracteres de atajo y, luego, actívela con la tecla F correspondiente desde la vista Send.

## Relacionado

- [Enviar un búfer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro de CW](edit-a-cw-macro-string.md)
- [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

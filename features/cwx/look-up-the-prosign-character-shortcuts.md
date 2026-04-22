# Consultar los atajos de caracteres de prosignos

El panel CWX incluye una leyenda de prosignos integrada para encontrar los caracteres de atajo correctos al componer mensajes CW o macros.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en modo CW, CWL o CWU para que el panel CWX sea visible.

## Pasos

1. Localice el panel CWX en el área central de la ventana principal.
2. Haga clic en "Setup" en la parte inferior del panel CWX.
3. Lea la leyenda de prosignos que se muestra en la vista Setup. Indica los caracteres de atajo para los prosignos CW más comunes: `=`, `+`, `(`, `&` y `$`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| "Send" | Muestra el área de envío en vivo con el historial y el campo de entrada de texto. | — |
| "Live" | Muestra la vista de envío en vivo. | — |
| "Setup" | Muestra el editor de macros, la configuración QSK y la leyenda de prosignos. | — |
| Leyenda de prosignos | Visualización de solo lectura de los caracteres de atajo para los prosignos CW más comunes (`=`, `+`, `(`, `&`, `$`). | — |
| Speed: | Velocidad de envío CW en WPM. Rango válido: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Delay: | Retardo entre macros en ms. Rango válido: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Habilita el QSK de ruptura total. | `CwxQsk` |
| Editores de macros F1 … F12 | Campos de texto para cada macro en la vista Setup. | `CwxMacro_F1` – `CwxMacro_F12` |

## Consejos

- Use los caracteres de atajo de prosignos directamente al escribir en el área de texto de envío o al editar cadenas de macros. Por ejemplo, escriba `=` en el texto de su macro donde desee que se envíe el prosigno BT.
- La leyenda de prosignos siempre es accesible en la vista Setup sin afectar ninguna transmisión en curso.

## Relacionado

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)

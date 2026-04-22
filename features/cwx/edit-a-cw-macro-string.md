# Editar una cadena de macro CW

El panel CWX almacena hasta 12 cadenas de macro, una por cada tecla de función F1–F12. Esta página explica cómo abrir el editor de macros y escribir o modificar una cadena de macro para que transmita el texto CW correcto al activarse.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El panel CWX requiere una conexión de radio.
- El slice activo debe estar en modo CW, CWL o CWU para que aparezca el panel CWX.

## Pasos

1. Abra el panel CWX. Aparece en el área central de la ventana principal cuando el slice activo está en un modo CW.
2. Haga clic en **Setup** en la barra inferior del panel CWX. La vista cambia al editor de macros.
3. Localice el espacio de macro que desea editar. Cada espacio está etiquetado con **F1** a **F12** en el lado izquierdo.
4. Haga clic dentro del campo de texto a la derecha de la etiqueta de la tecla de función para ese espacio.
5. Borre el texto existente si es necesario y escriba la nueva cadena de macro.
6. Presione Tab o haga clic en otro lugar. El nuevo texto se guarda inmediatamente en la clave de configuración correspondiente (`CwxMacro_F1` a `CwxMacro_F12`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| Editores de macro **F1** … **F12** | Campos de texto en la vista Setup. Cada uno contiene la cadena que se envía al presionar esa tecla de función o al hacer clic en su botón de macro. | `CwxMacro_F1` … `CwxMacro_F12` | — | Cualquier texto CW válido o atajo de prosigno |
| **Delay:** | Retardo entre macros en milisegundos. | `CwxDelay` | 5 ms | 0–2000 ms |
| **QSK** | Habilita QSK (ruptura total) cuando está marcado. | `CwxQsk` | — | On / Off |
| **Speed:** | Velocidad de envío CW en palabras por minuto; se aplica a todas las macros. | `CwxSpeedWpm` | 20 WPM | 5–100 WPM |

## Consejos

- La leyenda de prosignos que se muestra en el panel indica los caracteres de atajo para los prosignos CW más comunes (como `=`, `+`, `(`, `&`, `$`). Use estos caracteres en sus cadenas de macro para enviar los prosignos correspondientes.
- Presionar Escape interrumpe una transmisión CW en curso. Esto funciona incluso durante el envío de una macro.
- Para probar una macro después de editarla, haga clic en **Send** o **Live** en la barra inferior para salir de la vista Setup y luego presione la tecla de función correspondiente.

## Temas relacionados

- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar la ruptura total QSK](enable-qsk-full-break-in.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)

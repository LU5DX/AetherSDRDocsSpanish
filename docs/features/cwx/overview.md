# Descripción general de CWX

CWX es la interfaz de manipulador CW integrada en AetherSDR. Permite enviar texto escrito o macros predefinidas a través del manipulador del FLEX-8600, controlar la velocidad de envío, establecer el retardo entre macros y activar el QSK de ruptura total, todo sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión de radio activa.
- Establezca el slice activo en modo CW, CWL o CWU. El panel CWX aparece en el área central de la ventana principal cuando hay un slice en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionadas mediante los botones en la parte inferior del panel: Send, Live y Setup. El control de velocidad Speed: y los botones de selección de vista están siempre visibles, independientemente de la vista activa.

**Vista Send** — Muestra un historial desplazable de los búferes enviados anteriormente, presentados como burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten.

**Vista Live** — Muestra el área de envío en tiempo real. Úsela cuando desee monitorear la transmisión mientras ocurre.

**Vista Setup** — Muestra los 12 editores de macros de teclas F, el control Delay: y el interruptor QSK. Edite el texto de las macros aquí y configure las opciones de temporización del manipulador.

**Atajos F1–F12** — Cuando el slice activo está en modo CW o CWL, presionar F1 a F12 en el teclado envía la macro correspondiente de inmediato, independientemente de la vista que se muestre en ese momento.

**Escape** — Presionar Escape interrumpe la transmisión CW actual y vacía el búfer de envío. Esto funciona en toda la aplicación siempre que CWX esté activo.

## Función de cada control

| Control | Descripción | Ajuste persistido |
|---|---|---|
| Send | Cambia a la vista de historial de envío y entrada de texto. | — |
| Live | Cambia a la vista de envío en tiempo real. | — |
| Setup | Cambia a la vista del editor de macros y configuración de QSK. | — |
| Speed: | Velocidad de envío CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envío | Pantalla desplazable de los búferes de envío anteriores con resaltado por carácter. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el búfer escrito. | — |
| F1 … F12 (botones de macro) | Envía la macro almacenada para esa tecla de función. Activable mediante atajo de teclado cuando el slice está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Campos de texto en la vista Setup para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa el QSK de ruptura total cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para los prosignos CW más comunes (=, +, (, &, $). | — |

## Consejos

- Presionar Escape durante la transmisión de una macro vacía el búfer de inmediato. Dado que el estado del manipulador alterna rápidamente entre puntos y rayas, Escape se ejecuta de forma incondicional en lugar de esperar un estado de transmisión específico, por lo que detiene el envío de manera fiable.
- Los atajos de teclado F1–F12 solo se activan cuando el slice activo está en modo CW o CWL. Cambiar el slice a un modo que no sea CW los desactiva automáticamente.

## Temas relacionados

- [Enviar un búfer CW escrito en tiempo real](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar el QSK de ruptura total](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)

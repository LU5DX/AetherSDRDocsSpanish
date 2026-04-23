# Descripción general de CWX

CWX es el panel de manipulación CW de AetherSDR. Permite escribir y enviar texto CW en tiempo real, activar cadenas de macros predefinidas con las teclas de función, y configurar QSK y el retardo entre macros — todo enrutado a través del radio Flex conectado.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. CWX requiere una conexión de radio activa.
- El slice activo debe estar en modo CW, CWL o CWU para que CWX aparezca automáticamente en el área de la ventana principal.

## Cómo funciona

CWX es un panel de 250 píxeles de ancho fijo que aparece en el área central de MainWindow. Tiene tres vistas, seleccionadas mediante botones en la barra inferior: Send, Live y Setup. La barra inferior también contiene el control Speed, que siempre es visible independientemente de la vista activa.

**La vista Send** muestra un historial desplazable de los buffers enviados anteriormente, presentados como burbujas de chat que se acumulan de abajo hacia arriba. Cada burbuja muestra el texto y una marca de tiempo. Debajo del historial hay un área de entrada de texto donde se escribe el siguiente mensaje. Al presionar Enter se envía el buffer escrito a la radio.

**La vista Live** muestra el área de envío en tiempo real. Para acceder a ella, haga clic en Live en la barra inferior.

**La vista Setup** muestra los 12 editores de macros para las teclas F, el control Delay y el botón QSK. Edite el texto de una macro en su campo; el valor se guarda inmediatamente y se utiliza la próxima vez que se active esa macro.

**Las teclas F1–F12** activan macros en toda la aplicación siempre que el slice activo esté en modo CW o CWL. Presionar Escape limpia el buffer de envío actual y cancela la transmisión.

## Qué hace cada control

| Control | Vista | Comportamiento | Clave de configuración |
|---|---|---|---|
| Send | Barra inferior | Cambia a la vista Send. Muestra la entrada del buffer escrito y el historial de envíos. | — |
| Live | Barra inferior | Cambia a la vista Live. | — |
| Setup | Barra inferior | Cambia al editor de macros y la configuración QSK. | — |
| Speed: | Barra inferior | Velocidad de envío CW en PPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envíos | Vista Send | Visualización desplazable de los buffers de envío anteriores con resaltado por carácter y marcas de tiempo. Solo lectura. | — |
| Área de texto de envío | Vista Send | Escriba aquí el texto CW. Presione Enter para enviar el buffer a la radio. | — |
| F1 … F12 (macros) | Vista Send/Live | Envía la cadena de macro almacenada para esa tecla de función. También se activa con la tecla de teclado correspondiente cuando el slice activo está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Vista Setup | Campos de texto para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Vista Setup | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Vista Setup | Interruptor. Habilita la operación CW con QSK (ruptura total). | `CwxQsk` |
| Leyenda de prosignos | Vista Setup | Referencia de solo lectura que muestra los atajos de caracteres para los prosignos CW más comunes (=, +, (, &, $). | — |

## Consejos

- Presionar Escape cancela una transmisión CW en curso al limpiar el buffer de envío. Esto funciona en toda la aplicación durante la operación en CW o CWL y no interfiere con el comportamiento normal de Escape en la interfaz, como cerrar diálogos.
- Los atajos de macros F1–F12 solo están activos cuando el modo del slice actual es CW o CWL. No tienen efecto en otros modos.

## Temas relacionados

- [Enviar un buffer CW escrito en tiempo real](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar QSK de ruptura total](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres para prosignos](look-up-the-prosign-character-shortcuts.md)

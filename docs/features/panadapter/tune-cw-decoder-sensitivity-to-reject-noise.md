# Ajustar la sensibilidad del decodificador CW para rechazar ruido

El control deslizante **Sens** controla con qué rigor filtra el decodificador CW las decodificaciones de caracteres inciertas. Subirlo suprime la salida distorsionada causada por ruido o señales débiles; bajarlo muestra más caracteres a costa de la precisión.

## Antes de comenzar

- El panel de decodificación CW debe estar abierto en el applet Panadapter. Si no está visible, ábralo primero.
- El audio de la PC debe estar enrutado a AetherSDR. El panel muestra "(requires PC Audio)" como recordatorio.

## Pasos

1. Localice el panel de decodificación CW en la parte inferior del applet Panadapter.
2. Encuentre la etiqueta **Sens:** y el control deslizante horizontal corto inmediatamente a su derecha.
3. Arrastre el control deslizante **Sens** hacia la izquierda para aceptar más decodificaciones (umbral más bajo) o hacia la derecha para rechazar decodificaciones de baja confianza (umbral más alto).
4. Observe el área de "texto de decodificación CW". Los caracteres en rojo o naranja indican baja confianza; redúzcalos moviendo el control deslizante hacia la derecha.
5. Suelte el control deslizante. El valor se guarda automáticamente en `CwDecoderSensitivity`.

## Qué hace cada control

| Control                        | Predeterminado | Rango              |
|--------------------------------|----------------|--------------------|
| Control deslizante **Sens**    | 30             | 0–100              |
| Texto de decodificación CW     | —              | —                  |
| Etiqueta de estadísticas CW    | —              | `<hz> Hz  <wpm> WPM` |
| Control deslizante de rango **Pitch** | 500–700 Hz | 300–1200 Hz        |
| Control deslizante de rango **WPM**   | 15–40 WPM | 5–60 WPM            |
| Botón **A-**                   | —              | —                  |
| Botón **A+**                   | —              | —                  |
| Asa de redimensionado del panel CW | —          | —                  |
| Control deslizante **Lo** (tono mín.) | 500 Hz | 300–1200 Hz         |
| Control deslizante **Hi** (tono máx.) | 700 Hz | 300–1200 Hz        |
| **🔒P** (Bloqueo de tono)       | —              | —                  |
| **🔒S** (Bloqueo de velocidad)  | —              | —                  |
| Botón **CPY ALL**              | —              | —                  |
| Botón **CPY VIS**              | —              | —                  |
| Botón **CLR**                  | —              | —                  |
| Botón **✕** (cerrar CW)        | —              | —                  |

## Coloración del texto de decodificación CW

El texto decodificado usa colores para indicar confianza:

| Color   | Umbral de costo | Significado           |
|---------|-----------------|-----------------------|
| Verde   | < 0.15          | Confianza alta        |
| Amarillo| < 0.35          | Confianza moderada    |
| Naranja | < 0.60          | Confianza baja        |
| Rojo    | >= 0.60         | Confianza muy baja    |

El texto decodificado del lado TX (su propia transmisión) aparece en cian (`#5fc8ff`) para que pueda distinguir su transmisión del CW entrante. Al cambiar de TX a RX, se inserta automáticamente un espacio separador para evitar que las dos secuencias de colores se mezclen.

## Bloquear el tono del decodificador CW

Use **🔒P** (Lock Pitch) para fijar la búsqueda de tono del decodificador a la frecuencia actualmente sintonizada. Esto es útil una vez que el decodificador se ha enganchado a una señal y desea evitar que se desvíe.

1. Haga clic en **🔒P** para activar el bloqueo de tono.
2. Haga clic nuevamente para desactivar el bloqueo y permitir que el decodificador busque libremente en todo el rango de tonos.

## Bloquear la velocidad del decodificador CW

Use **🔒S** (Lock Speed) para fijar la búsqueda de velocidad del decodificador al valor actual de WPM. Esto evita que el decodificador cambie entre diferentes velocidades de caracteres mientras decodifica una sola transmisión.

1. Haga clic en **🔒S** para activar el bloqueo de velocidad.
2. Haga clic nuevamente para desactivar el bloqueo y permitir que el decodificador se adapte a los cambios de velocidad.

## Ajustar el tamaño de fuente del texto de decodificación CW

Los botones **A+** y **A-** en la parte superior del panel de decodificación CW le permiten aumentar o disminuir el tamaño de fuente del texto decodificado.

1. Haga clic en **A+** para agrandar el texto; haga clic en **A-** para reducirlo.
2. El tamaño de fuente se conserva entre sesiones. El rango válido es de 8–32 píxeles.
3. Use texto más grande para mejor legibilidad a distancia; use texto más pequeño para ver más historial en el panel.

## Redimensionar el panel de decodificación CW

Arrastre la delgada asa horizontal en la parte superior del panel de decodificación CW (justo debajo de la barra de título) hacia arriba o hacia abajo para cambiar la altura del panel. Esto revela más o menos historial de texto decodificado.

1. Mueva el cursor sobre la barra de redimensionado de 4 píxeles de alto hasta que se convierta en un cursor de redimensionado vertical.
2. Haga clic y arrastre hacia arriba para encoger el panel, o hacia abajo para agrandarlo. El rango válido es de 60–600 píxeles.
3. La altura del panel se conserva entre sesiones.

## Copiar texto CW decodificado

- Haga clic en **CPY ALL** para copiar todo el búfer de texto decodificado al portapapeles.
- Haga clic en **CPY VIS** para copiar solo el texto actualmente visible en el área de desplazamiento.
- Hacer clic derecho en el área de texto de decodificación CW también brinda acceso a las acciones de texto estándar (Select All, Copy, etc.) junto con la opción **Clear**.

## Limpiar el búfer de decodificación CW

Haga clic en **CLR** para borrar todo el texto decodificado del búfer. Esto es útil antes de una nueva transmisión cuando desea una lectura limpia.

## Ocultar el panel de decodificación CW

Haga clic en el botón **✕** en la parte superior del panel de decodificación CW para ocultarlo. El panel reaparece cuando vuelve a activar el decodificador CW.

## Consejos

- Comience con el valor predeterminado de 30 y suba el control deslizante gradualmente hasta que los caracteres rojos y naranjas desaparezcan del texto decodificado.
- El color de los caracteres es un indicador rápido de confianza: si la mayor parte de la salida es verde, la sensibilidad actual está bien ajustada a las condiciones de la señal. Si la pantalla se queda completamente en blanco, el control deslizante está demasiado alto — muévalo hacia la izquierda hasta que vuelvan los caracteres.
- El control deslizante de rango **Pitch** (predeterminado 500–700 Hz, rango 300–1200 Hz) limita los tonos que busca el decodificador. Reducir ese rango para que coincida con el tono de la señal recibida puede reducir las falsas activaciones independientemente de **Sens**.
- El control deslizante de rango **WPM** (predeterminado 15–40 WPM, rango 5–60 WPM) limita las velocidades que busca el decodificador. Reducir ese rango para que coincida con la velocidad de transmisión de la señal recibida mejora la precisión de la decodificación.
- Hacer clic derecho en el área de texto de decodificación CW también brinda acceso a las acciones de texto estándar (Select All, Copy, etc.) junto con la opción **Clear**.
- Use **A+** y **A-** para encontrar un tamaño de lectura cómodo. El cambio se aplica de inmediato y se guarda para la próxima vez.
- Bloquee tanto **🔒P** como **🔒S** una vez que el decodificador se haya enganchado a una señal estable para producir el texto más consistente.

## Solución de problemas

- **El texto decodificado desaparece por completo después de subir Sens** — el umbral está por encima del nivel de confianza de la señal entrante. Baje el control deslizante hasta que vuelva la salida, luego súbalo más lentamente.
- **La salida sigue con ruido incluso con Sens en 100** — la señal puede estar fuera de la ventana de búsqueda de tono. Verifique la etiqueta de estadísticas CW para ver el tono informado y ajuste el control deslizante de rango **Pitch** para que lo abarque.
- **Sens se restablece a 30 después de reiniciar** — si falta `CwDecoderSensitivity` en los ajustes guardados, AetherSDR usa el valor predeterminado de 30. Mueva el control deslizante una vez para escribir el valor; a partir de entonces se guarda en cada cambio.
- **El tamaño de fuente se restablece después de reiniciar** — el tamaño de fuente se guarda automáticamente. Si se restablece, asegúrese de tener permisos de escritura en el archivo de ajustes.

## Relacionado

- [Activar el decodificador CW para leer Morse fuera del aire](turn-on-the-cw-decoder-to-read-morse-off-air.md)
- [Bloquear el tono o la velocidad del decodificador CW una vez que el seguimiento sea bueno](lock-cw-decoder-pitch-or-speed-once-tracking-is-good.md)
- [Copiar texto CW decodificado al portapapeles](copy-decoded-cw-text-to-the-clipboard.md)

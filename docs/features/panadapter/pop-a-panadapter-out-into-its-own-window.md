# Extraer un panadaptador a su propia ventana

Cuando tiene más de un panadaptador abierto, puede desacoplar cualquiera de ellos en una ventana flotante separada. Esto es útil para colocar el panadaptador en un segundo monitor o redimensionarlo independientemente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando hay una conexión de radio activa.
- Abra al menos un panadaptador adicional. En modo de un solo panadaptador, el botón de extracción está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadaptador que desea desacoplar. Muestra la etiqueta del segmento (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** en esa barra de título.

   El panadaptador se desacopla en una ventana flotante sin bordes.

3. Para mover la ventana flotante, haga clic y arrastre la tira de título en la parte superior de la ventana flotante.
4. Para redimensionar la ventana flotante, arrastre el control de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana de nuevo al diseño principal, haga clic en el botón **↩** en la barra de título de la ventana flotante.

## Funciones de cada control

| Control          | Descripción                                                                          | Predeterminado |
|------------------|--------------------------------------------------------------------------------------|---------|
| **⬈** (extraer)  | Desacopla el panadaptador en una ventana flotante.                                   | —       |
| **↩** (acoplar)  | Devuelve el panadaptador flotante al diseño principal.                               | —       |
| **□** (maximizar) | Expande este panadaptador para llenar el área principal.                             | —       |
| **×** (cerrar)   | Cierra este panadaptador.                                                           | —       |
| Título segmento  | Indicador que muestra qué segmento está vinculado a este panadaptador (Slice A a Slice H). | Slice A |

> **Nota para sesiones Multi-Flex:** Al usar múltiples clientes, el título del segmento coincide con la letra de índice proporcionada por la radio, de modo que el título corresponde a la insignia del segmento.

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y el waterfall. El panel decodifica código Morse desde el audio de PC enrutado a AetherSDR. Tanto el CW recibido (RX) como el transmitido (TX) se decodifican y muestran en el mismo panel, con diferentes colores para distinguirlos.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio de PC esté activo. Si no hay audio enrutado, el panel muestra la sugerencia **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta stats CW** | Muestra el tono y la velocidad detectados, por ejemplo `750 Hz 20 WPM`. | — | Solo lectura; se actualiza continuamente mediante el decodificador. |
| Deslizador **Sens** | Filtra decodificaciones de baja confianza. Valores más altos son más estrictos. | 30 | Asigna el rango 0–100 a un umbral de costo de 1.0–0.1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P** (Bloquear tono) | Bloquea el tono del decodificador a la frecuencia sintonizada actual. | Desactivado | Alternar. |
| **🔒S** (Bloquear velocidad) | Bloquea la velocidad del decodificador a la lectura actual de WPM. | Desactivado | Alternar. |
| Deslizador de rango **Pitch** | Establece el tono mínimo y máximo que busca el decodificador. | 500–700 Hz | Rango: 300–1200 Hz. Deslizador de doble mango que reemplaza los deslizadores **Lo** y **Hi** separados. |
| Deslizador de rango **WPM** | Establece la velocidad mínima y máxima que busca el decodificador. | 15–40 WPM | Rango: 5–60 WPM. Nuevo en v26.6.3. |
| **CPY ALL** | Copia todo el texto decodificado al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto actualmente visible en el área de desplazamiento. | — | — |
| **CLR** | Limpia el búfer de decodificación CW. | — | — |
| **✕** (cerrar CW) | Oculta el panel de decodificación CW. | — | — |
| **Texto decodificado CW** | Visualización continua de solo lectura del CW decodificado, coloreado según la confianza de decodificación. | — | Verde: costo < 0.15; Amarillo: costo < 0.35; Naranja: costo < 0.60; Rojo: costo ≥ 0.60. El texto de origen TX aparece en cian (#5fc8ff). |

### Comportamiento del texto decodificado CW

El panel de decodificación CW ahora muestra tanto la decodificación Morse recibida (RX) como la transmitida (TX) en un área de texto continuo única:

- **Texto RX** — Coloreado según la confianza como se describe arriba (verde, amarillo, naranja, rojo).
- **Texto TX** — Se muestra en cian (#5fc8ff) para que pueda distinguir su propia transmisión del CW entrante.
- **Manejo de límites** — Al cambiar entre TX y RX, se inserta un espacio automáticamente para que las ejecuciones de color no se fusionen visualmente.
- **Seguimiento de origen** — El decodificador rastrea si el último texto decodificado provino de TX o RX para aplicar la lógica de separador correcta.

### Menú contextual del texto decodificado CW

Al hacer clic derecho dentro del área de **Texto decodificado CW** se abre un menú contextual. El menú contiene las acciones estándar de edición de texto (Seleccionar todo, Copiar, etc.) seguidas de un separador y un elemento **Clear**. Al hacer clic en **Clear** en el menú contextual se produce el mismo efecto que al hacer clic en el botón **CLR**: vacía el búfer de decodificación inmediatamente.

## Congelación del waterfall durante la transmisión

Cuando cualquier cliente en una sesión Multi-Flex comienza a transmitir, el waterfall en este panadaptador se congela automáticamente. Se reanuda la actualización cuando finaliza la transmisión. Esto elimina el artefacto de estela de TX de 10 a 23 segundos que aparecía anteriormente después de desactivar la transmisión.

Al reconectarse a la radio, el panadaptador reafirma la velocidad de fotogramas deseada y la duración de la línea del waterfall para evitar caer silenciosamente al valor predeterminado de 10 Hz de la radio.

## Panel de decodificación RTTY

Cuando el modo del segmento activo es RTTY o DIGL, aparece un panel de decodificación RTTY debajo del espectro y el waterfall. Este panel decodifica señales RTTY desde el audio de PC enrutado a AetherSDR. El panel tiene una altura fija de 90 píxeles y está oculto cuando el modo del segmento no es RTTY o DIGL.

> **Nota:** La decodificación RTTY requiere que el enrutamiento de audio de PC esté activo.

## Soporte de temas

La barra de título del panadaptador, el panel de decodificación CW, el panel de decodificación RTTY y todos los controles asociados ahora utilizan tokens de color sensibles al tema (sujetos a cambios en versiones futuras). La apariencia visual se adapta al tema activo sin necesidad de anulaciones de estilo manuales.

## Consejos

- La ventana flotante no tiene bordes. Use la tira de título dentro de la aplicación para arrastrarla y el control de tamaño en la esquina inferior derecha para redimensionarla. No hay borde de ventana del sistema operativo.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotando.
- Use el deslizador de rango **Pitch** para acotar el rango de tono de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Use el deslizador de rango **WPM** para acotar el rango de velocidad de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para borrar rápidamente el texto decodificado, haga clic derecho en el área de texto decodificado y seleccione **Clear** en lugar de buscar el botón **CLR**.
- El texto decodificado del lado TX aparece en cian para ayudarle a distinguir su propia transmisión del CW entrante, sin necesidad de un prefijo textual.

## Solución de problemas

- **El botón ⬈ no está visible** — Tiene solo un panadaptador abierto. Los botones de extracción, maximizar y cerrar están ocultos en modo de un solo panadaptador. Abra un panadaptador adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la tira de título dentro de la ventana flotante, no el área del espectro. El área del espectro se utiliza para sintonizar.
- **El área de texto decodificado CW no muestra texto** — Verifique que el audio de PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionado

- [Maximize one panadapter to fill the main area](maximize-one-panadapter-to-fill-the-main-area.md)
- [Close an extra panadapter](close-an-extra-panadapter.md)
- [Click the spectrum to activate a panadapter (multi-slice mode)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Panadapter overview](overview.md)

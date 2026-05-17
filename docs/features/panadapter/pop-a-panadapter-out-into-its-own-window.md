# Extraer un panadapter a su propia ventana

Cuando tiene más de un panadapter abierto, puede desacoplar cualquiera de ellos en una ventana flotante separada. Esto es útil para colocar el panadapter en un segundo monitor o redimensionarlo independientemente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando hay una conexión de radio activa.
- Abra al menos un panadapter adicional. En el modo de un solo panadapter, el botón de extracción está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea desacoplar. Muestra la etiqueta del slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** en esa barra de título.

   El panadapter se desacopla en una ventana flotante sin marco.

3. Para mover la ventana flotante, haga clic y arrastre la barra de título en la parte superior de la ventana flotante.
4. Para redimensionar la ventana flotante, arrastre el control de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana de nuevo al diseño principal, haga clic en el botón **↩** en la barra de título de la ventana flotante.

## Qué hace cada control

| Control          | Descripción                                                                          | Predeterminado |
|------------------|--------------------------------------------------------------------------------------|---------|
| **⬈** (extraer)  | Desacopla el panadapter en una ventana flotante.                                     | —       |
| **↩** (acoplar)  | Devuelve el panadapter flotante al diseño principal.                                 | —       |
| **□** (maximizar) | Expande este panadapter para llenar el área principal.                               | —       |
| **×** (cerrar)    | Cierra este panadapter.                                                              | —       |
| Título del slice | Indicador que muestra qué slice está vinculado a este panadapter (Slice A a Slice H). | Slice A |

> **Nota para sesiones Multi-Flex:** Cuando se usan múltiples clientes, el título del slice coincide con la letra de índice proporcionada por la radio, por lo que el título corresponde a la insignia del slice.

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y el waterfall. El panel decodifica código Morse del audio de PC enrutado a AetherSDR. Tanto el CW recibido (RX) como el transmitido (TX) se decodifican y muestran en el mismo panel, con diferentes colores para distinguirlos.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio de PC esté activo. Si no hay audio enrutado, el panel muestra la sugerencia **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta de estadísticas CW** | Muestra el tono y la velocidad detectados, por ejemplo `750 Hz  20 WPM`. | — | Solo lectura; se actualiza continuamente mediante el decodificador. |
| **Control deslizante Sens** | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Asigna el rango 0–100 a un umbral de costo de 1.0–0.1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P** (Bloquear tono) | Bloquea el tono del decodificador a la frecuencia sintonizada actual. | Desactivado | Alternar. |
| **🔒S** (Bloquear velocidad) | Bloquea la velocidad del decodificador a la lectura de WPM actual. | Desactivado | Alternar. |
| **Lo** (control deslizante) | Tono mínimo que busca el decodificador. Limitado para no ser mayor que **Hi**. | 500 Hz | Rango: 300–1200 Hz. |
| **Hi** (control deslizante) | Tono máximo que busca el decodificador. Limitado para no ser menor que **Lo**. | 700 Hz | Rango: 300–1200 Hz. |
| **CPY ALL** | Copia todo el texto decodificado al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto actualmente visible en el área de desplazamiento. | — | — |
| **CLR** | Limpia el búfer de decodificación CW. | — | — |
| **✕** (cerrar CW) | Oculta el panel de decodificación CW. | — | — |
| **Texto de decodificación CW** | Visualización continua de solo lectura del CW decodificado, coloreado según la confianza de decodificación. | — | Verde: costo < 0.15; Amarillo: costo < 0.35; Naranja: costo < 0.60; Rojo: costo ≥ 0.60. El texto de origen TX aparece en cian (#5fc8ff). |

### Comportamiento del texto de decodificación CW

El panel de decodificación CW ahora muestra tanto la decodificación Morse recibida (RX) como la transmitida (TX) en un área de texto continuo único:

- **Texto RX** — Coloreado según la confianza como se describió anteriormente (verde, amarillo, naranja, rojo).
- **Texto TX** — Renderizado en cian (#5fc8ff) para que pueda distinguir su propia transmisión del CW entrante.
- **Manejo de límites** — Al cambiar entre TX y RX, se inserta un espacio automáticamente para que las ejecuciones de color no se fusionen visualmente.
- **Seguimiento de fuente** — El decodificador rastrea si el último texto decodificado provino de TX o RX para aplicar la lógica de separador correcta.

### Menú contextual del texto de decodificación CW

Al hacer clic derecho dentro del área de **texto de decodificación CW** se abre un menú contextual. El menú contiene las acciones de edición de texto estándar (Seleccionar todo, Copiar, etc.) seguidas de un separador y un elemento **Clear**. Al hacer clic en **Clear** en el menú contextual se obtiene el mismo efecto que al hacer clic en el botón **CLR**: se vacía el búfer de decodificación inmediatamente.

## Consejos

- La ventana flotante no tiene marco. Use la barra de título dentro de la aplicación para arrastrarla y el control de tamaño en la esquina inferior derecha para redimensionarla. No hay borde de ventana del sistema operativo.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotante.
- Use **Lo** y **Hi** juntos para delimitar el rango de tono de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para limpiar rápidamente el texto decodificado, haga clic derecho en el área de texto de decodificación y seleccione **Clear** en lugar de buscar el botón **CLR**.
- El texto decodificado del lado TX aparece en cian para ayudarle a distinguir su propia transmisión del CW entrante, sin necesidad de un prefijo textual.

## Solución de problemas

- **El botón ⬈ no es visible** — Solo tiene un panadapter abierto. Los botones de extracción, maximizar y cerrar están todos ocultos en el modo de un solo panadapter. Abra un panadapter adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la barra de título dentro de la ventana flotante, no el área del espectro. El área del espectro se usa para sintonizar.
- **El área de texto de decodificación CW no muestra texto** — Verifique que el audio de PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionado

- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter extra](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Resumen del panadapter](overview.md)

# Extraer un panadapter a su propia ventana

Cuando tiene más de un panadapter abierto, puede desprender cualquiera de ellos en una ventana flotante independiente. Esto resulta útil para colocar el panadapter en un segundo monitor o para cambiarle el tamaño de forma independiente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando hay una conexión de radio activa.
- Abra al menos un panadapter adicional. En el modo de panadapter único, el botón de extracción está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea desprender. Muestra la etiqueta del slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** de esa barra de título.

   El panadapter se desprende en una ventana flotante sin marco.

3. Para mover la ventana flotante, haga clic y arrastre la franja de título en la parte superior de la ventana flotante.
4. Para cambiar el tamaño de la ventana flotante, arrastre el controlador de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana de nuevo al diseño principal, haga clic en el botón **↩** de la barra de título de la ventana flotante.

## Qué hace cada control

| Control          | Descripción                                                                                         | Predeterminado |
|------------------|-----------------------------------------------------------------------------------------------------|----------------|
| **⬈** (extraer)  | Desprende el panadapter en una ventana flotante.                                                    | —              |
| **↩** (acoplar)  | Devuelve el panadapter flotante al diseño principal.                                                | —              |
| **□** (maximizar)| Expande este panadapter para ocupar el área principal.                                              | —              |
| **×** (cerrar)   | Cierra este panadapter.                                                                             | —              |
| Título del slice | Indicador que muestra qué slice está vinculado a este panadapter (Slice A hasta Slice H).           | Slice A        |

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y del waterfall. El panel decodifica código Morse a partir del audio del PC enrutado a AetherSDR.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio del PC esté activo. Si no hay audio enrutado, el panel muestra el aviso **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta CW stats** | Muestra el tono y la velocidad detectados, por ejemplo `750 Hz  20 WPM`. | — | Solo lectura; actualizado de forma continua por el decodificador. |
| Control deslizante **Sens** | Filtra las decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Asigna el rango 0–100 a un umbral de costo de 1.0–0.1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P** (Lock Pitch) | Fija el tono del decodificador a la frecuencia sintonizada actual. | Off | Conmutador. |
| **🔒S** (Lock Speed) | Fija la velocidad del decodificador a la lectura WPM actual. | Off | Conmutador. |
| Control deslizante **Lo** | Tono mínimo que busca el decodificador. Limitado para no superar **Hi**. | 500 Hz | Rango: 300–1200 Hz. |
| Control deslizante **Hi** | Tono máximo que busca el decodificador. Limitado para no ser menor que **Lo**. | 700 Hz | Rango: 300–1200 Hz. |
| **CPY ALL** | Copia el texto decodificado completo al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto visible actualmente en el área de desplazamiento. | — | — |
| **CLR** | Borra el búfer de decodificación CW. | — | — |
| **✕** (cerrar CW) | Oculta el panel de decodificación CW. | — | — |
| **Texto de decodificación CW** | Visualización continua de solo lectura del CW decodificado, con color según la confianza de la decodificación. | — | Verde: costo < 0.15; Amarillo: costo < 0.35; Naranja: costo < 0.60; Rojo: costo ≥ 0.60. |

### Menú contextual del texto de decodificación CW

Al hacer clic derecho dentro del área **CW decode text** se abre un menú contextual. El menú contiene las acciones estándar de edición de texto (Select All, Copy, entre otras), seguidas de un separador y un elemento **Clear**. Hacer clic en **Clear** en el menú contextual tiene el mismo efecto que hacer clic en el botón **CLR**: vacía el búfer de decodificación de inmediato.

## Consejos

- La ventana flotante no tiene marco. Use la franja de título de la aplicación para arrastrarla y el controlador de tamaño en la esquina inferior derecha para cambiar su tamaño. No hay borde de ventana del sistema operativo.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotante.
- Use **Lo** y **Hi** juntos para delimitar el rango de tono de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para borrar el texto decodificado rápidamente, haga clic derecho en el área de texto de decodificación y seleccione **Clear** en lugar de usar el botón **CLR**.

## Solución de problemas

- **El botón ⬈ no es visible** — Solo tiene un panadapter abierto. Los botones de extracción, maximización y cierre están todos ocultos en el modo de panadapter único. Abra un panadapter adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la franja de título dentro de la ventana flotante, no el área del espectro. El área del espectro se usa para sintonizar.
- **El área de texto de decodificación CW no muestra texto** — Verifique que el audio del PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionados

- [Maximizar un panadapter para ocupar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multi-slice)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)

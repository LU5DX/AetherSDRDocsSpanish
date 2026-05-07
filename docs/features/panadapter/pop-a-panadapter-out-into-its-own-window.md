# Extraer un panadapter a su propia ventana

Cuando tiene más de un panadapter abierto, puede desacoplar cualquiera de ellos en una ventana flotante separada. Esto es útil para colocar el panadapter en un segundo monitor o redimensionarlo independientemente del diseño principal de AetherSDR.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El botón de extracción solo está disponible cuando una conexión de radio está activa.
- Abra al menos un panadapter adicional. En modo de un solo panadapter, el botón de extracción está oculto.

## Pasos

1. Localice la barra de título en la parte superior del panadapter que desea desacoplar. Muestra la etiqueta de la slice (por ejemplo, **Slice A**) y una fila de botones pequeños a la derecha.
2. Haga clic en el botón **⬈** en esa barra de título.

   El panadapter se desacopla en una ventana flotante sin bordes.

3. Para mover la ventana flotante, haga clic y arrastre la barra de título en la parte superior de la ventana flotante.
4. Para redimensionar la ventana flotante, arrastre el control de tamaño en su esquina inferior derecha.
5. Para acoplar la ventana de nuevo al diseño principal, haga clic en el botón **↩** en la barra de título de la ventana flotante.

## Qué hace cada control

| Control          | Descripción                                                                          | Predeterminado |
|------------------|--------------------------------------------------------------------------------------|---------|
| **⬈** (extraer)  | Desacopla el panadapter en una ventana flotante.                                      | —       |
| **↩** (acoplar)  | Devuelve el panadapter flotante al diseño principal.                                 | —       |
| **□** (maximizar) | Expande este panadapter para llenar el área principal.                                | —       |
| **×** (cerrar)    | Cierra este panadapter.                                                              | —       |
| Título de slice  | Indicador que muestra qué slice está vinculada a este panadapter (Slice A a Slice H). | Slice A |

## Panel de decodificación CW

Cuando el panel de decodificación CW está abierto, aparece debajo del espectro y el waterfall. El panel decodifica código Morse desde el audio del PC enrutado a AetherSDR.

> **Nota:** La decodificación CW requiere que el enrutamiento de audio del PC esté activo. Si no se enruta audio, el panel muestra la sugerencia **(requires PC Audio)**.

### Controles del panel de decodificación CW

| Control | Descripción | Predeterminado | Notas |
|---|---|---|---|
| **Etiqueta de estadísticas CW** | Muestra el tono y la velocidad detectados, por ejemplo `750 Hz  20 WPM`. | — | Solo lectura; se actualiza continuamente mediante el decodificador. |
| Deslizador **Sens** | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | 30 | Mapea el rango 0–100 a un umbral de costo de 1.0–0.1. Se guarda como `CwDecoderSensitivity`. |
| **🔒P** (Bloquear tono) | Bloquea el tono del decodificador a la frecuencia sintonizada actual. | Apagado | Alternar. |
| **🔒S** (Bloquear velocidad) | Bloquea la velocidad del decodificador a la lectura actual de WPM. | Apagado | Alternar. |
| Deslizador **Lo** | Tono mínimo que busca el decodificador. Limitado para no ser mayor que **Hi**. | 500 Hz | Rango: 300–1200 Hz. |
| Deslizador **Hi** | Tono máximo que busca el decodificador. Limitado para no ser menor que **Lo**. | 700 Hz | Rango: 300–1200 Hz. |
| **CPY ALL** | Copia todo el texto decodificado al portapapeles. | — | — |
| **CPY VIS** | Copia solo el texto actualmente visible en el área de desplazamiento. | — | — |
| **CLR** | Limpia el búfer de decodificación CW. | — | — |
| **✕** (cerrar CW) | Oculta el panel de decodificación CW. | — | — |
| **Texto de decodificación CW** | Visualización continua de solo lectura del CW decodificado, coloreado según la confianza de decodificación. | — | Verde: costo < 0.15; Amarillo: costo < 0.35; Naranja: costo < 0.60; Rojo: costo ≥ 0.60. |

### Menú contextual del texto de decodificación CW

Al hacer clic derecho dentro del área de **texto de decodificación CW** se abre un menú contextual. El menú contiene las acciones estándar de edición de texto (Seleccionar todo, Copiar, etc.) seguidas de un separador y un elemento **Clear**. Al hacer clic en **Clear** en el menú contextual se obtiene el mismo efecto que al hacer clic en el botón **CLR**: vacía el búfer de decodificación inmediatamente.

## Consejos

- La ventana flotante no tiene bordes. Use la barra de título interna de la aplicación para arrastrarla y el control de tamaño en la esquina inferior derecha para redimensionarla. No hay borde de ventana del sistema operativo.
- Las etiquetas de los botones ⬈ y ↩ cambian para reflejar el estado actual: ⬈ cuando está acoplado, ↩ cuando está flotando.
- Use **Lo** y **Hi** juntos para acotar el rango de tono de la señal que está copiando. Reducir el rango disminuye las decodificaciones falsas cuando hay múltiples señales CW presentes.
- Para limpiar el texto decodificado rápidamente, haga clic derecho en el área de texto de decodificación y seleccione **Clear** en lugar de buscar el botón **CLR**.

## Solución de problemas

- **El botón ⬈ no es visible** — Solo tiene un panadapter abierto. Los botones de extraer, maximizar y cerrar están ocultos en modo de un solo panadapter. Abra un panadapter adicional para que aparezcan.
- **La ventana flotante no se puede mover** — Haga clic y arrastre la barra de título dentro de la ventana flotante, no el área del espectro. El área del espectro se usa para sintonizar.
- **El área de texto de decodificación CW no muestra texto** — Verifique que el audio del PC esté enrutado a AetherSDR. El panel muestra **(requires PC Audio)** cuando el audio no está disponible.

## Relacionado

- [Maximizar un panadapter para llenar el área principal](maximize-one-panadapter-to-fill-the-main-area.md)
- [Cerrar un panadapter adicional](close-an-extra-panadapter.md)
- [Hacer clic en el espectro para activar un panadapter (modo multislices)](click-the-spectrum-to-activate-a-panadapter-multi-slice-mode.md)
- [Descripción general del panadapter](overview.md)

# Applet de Panadapter

El applet de Panadapter es un contenedor para una sola pantalla de panadapter (espectro FFT + waterfall) con una barra de título que ofrece agarre de arrastre, ventana flotante, maximizar y controles de cierre. Un panel opcional de decodificación de CW puede aparecer debajo para decodificación de Morse fuera del aire. También está disponible una vista de espectro FFT 3D para visualizar el historial de señales como una superficie 3D en desplazamiento.

## Controles

| Control | Tipo | Valor predeterminado | Rango | Clave de ajuste | Comportamiento | Notas |
|---------|------|----------------------|-------|-----------------|----------------|-------|
| Título de slice | indicador | "Slice A" | Slice A..Slice H | *ninguna* | Muestra qué slice está vinculado a este panadapter. | |
| ⬈ / ↩ (ventana flotante/acoplar) | push_button | | | *ninguna* | Expulsa el panadapter a una ventana flotante o lo vuelve a acoplar. Oculto en modo de pan único. | La ventana flotante no tiene marco. Arrastre mediante la franja de título de la aplicación, cambie el tamaño mediante el agarre de la esquina inferior derecha. En macOS, cada ciclo de flotar/acoplar restablece los recursos de GPU y evita que el espectro se vuelva obsoleto. |
| □ (maximizar) | push_button | | | *ninguna* | Maximiza este panadapter en un diseño multi-pan. Oculto en modo de pan único. |
| × (cerrar) | push_button | | | *ninguna* | Cierra este panadapter. Oculto en modo de pan único. |
| Espectro / waterfall | drag_handle | | | *ninguna* | Haga clic para activar el panadapter; arrastre para sintonizar, desplácese para hacer zoom. | |
| Etiqueta de estadísticas de CW | indicador | | | *ninguna* | Muestra el tono y la velocidad de CW detectados (p. ej., "700 Hz 20 WPM"). | |
| Sens (sensibilidad del decodificador de CW) | slider | 30 | 0-100 | CwDecoderSensitivity | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | Asigna 0-100 a un umbral de costo de 1.0-0.1. |
| 🔒P (Bloquear tono) | toggle_button | | | *ninguna* | Bloquea el tono del decodificador de CW a la frecuencia sintonizada actual. | |
| 🔒S (Bloquear velocidad) | toggle_button | | | *ninguna* | Bloquea la velocidad del decodificador de CW al WPM actual. | |
| Lo (tono mínimo) | slider | 500 | 300-1200 Hz | *ninguna* | Tono mínimo que busca el decodificador de CW. Se limita automáticamente a ≤ Hi. | |
| Hi (tono máximo) | slider | 700 | 300-1200 Hz | *ninguna* | Tono máximo que busca el decodificador de CW. Se limita automáticamente a ≥ Lo. | |
| A- (reducir tamaño de fuente) | push_button | | | *ninguna* | Disminuye el tamaño de fuente del texto decodificado en 1 píxel. | Se conserva entre sesiones. Nuevo en v26.7.4. |
| A+ (aumentar tamaño de fuente) | push_button | | | *ninguna* | Aumenta el tamaño de fuente del texto decodificado en 1 píxel. | Se conserva entre sesiones. Nuevo en v26.7.4. |
| CPY ALL | push_button | | | *ninguna* | Copia todo el texto decodificado al portapapeles. | |
| CPY VIS | push_button | | | *ninguna* | Copia solo el texto actualmente visible en el área de desplazamiento. | |
| CLR | push_button | | | *ninguna* | Borra el búfer de decodificación de CW. | |
| ✕ (cerrar CW) | push_button | | | *ninguna* | Oculta el panel de decodificación de CW por completo. | |
| Texto de decodificación de CW | text_field | | | *ninguna* | Visualización continua de solo lectura del texto de CW decodificado. Coloreado por confianza: verde (<0.15), amarillo (<0.35), naranja (<0.60), rojo (≥0.60). | El tamaño de fuente es ajustable mediante los controles A+/A-. |
| Vista FFT 3D | toggle_button | Deshabilitado | | *ninguna* | Alterna la vista de espectro FFT 3D. Muestra el historial de señales como una superficie 3D con desplazamiento hacia adelante, sombras de elevación, límites de desplazamiento suave y suelo resincronizado después del zoom de ancho de banda. Los marcadores de slice proyectan sombras de elevación en caché. | Nuevo en v26.7.x (#4413-#4477). Parte de SpectrumWidget. |

## Controles del Panel de Decodificación de CW

El panel de decodificación de CW aparece en la parte inferior del panadapter cuando el modo CW está activo. Contiene:

- **Agarre de cambio de tamaño por arrastre**: Una franja delgada de 4 píxeles a lo largo del borde superior del panel. Arrastre hacia arriba o hacia abajo para cambiar la altura del panel y revelar más historial de texto decodificado. La altura del panel se conserva entre sesiones (rango: 60-600 píxeles).
- **Barra de estadísticas**: Muestra el tono de CW detectado (Hz) y la velocidad (WPM).
- **Slider de sensibilidad**: Ajusta la sensibilidad del decodificador (0-100).
- **Conmutadores de bloqueo de tono/velocidad**: Bloquean los valores de tono o velocidad actuales.
- **Sliders de rango de tono**: Establecen el rango de búsqueda de tono mínimo y máximo (300-1200 Hz).
- **Controles de tamaño de fuente**: Los botones A- y A+ ajustan el tamaño de fuente del texto decodificado (8-32 píxeles). Los cambios se conservan y se restauran en el próximo inicio.
- **Botones de copiar**: CPY ALL copia todo el texto decodificado; CPY VIS copia solo el texto visible.
- **Botón CLR**: Borra el búfer de decodificación.
- **Botón de cerrar (✕)**: Cierra el panel de decodificación de CW.

## Comportamiento de Congelación del Waterfall

El waterfall se congela automáticamente cuando la radio entra en estado TRANSMITTING según el sistema de interbloqueo de la radio. Se descongela cuando el estado TRANSMITTING se despeja. Este comportamiento sigue el estado real del interbloqueo de hardware de la radio en lugar de un borde de software local, eliminando el artefacto de estela de TX de 10-23 segundos que podía aparecer después de soltar la tecla en versiones anteriores.

- En una sesión multiFLEX, cualquier cliente conectado que transmita activa la congelación del waterfall en su panadapter.
- Al reconectar la radio, el FPS deseado del panadapter y la duración de línea del waterfall se reafirman automáticamente para evitar caer al valor predeterminado de 10 Hz de la radio.

## Inicialización del Panadapter Secundario

Los panadapters secundarios (Slices B-H) ahora tienen su rango de dBm inicializado al reconectar a la radio. Esto garantiza que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que podía causar una visualización de espectro plana después de la reconexión.

## Modo Canvas (v26.8.4)

Cuando se aloja en el canvas del espacio de trabajo, la franja de título del panadapter transmite un gesto de movimiento en vivo que refleja el modo canvas de la barra de título del contenedor. Este es un gesto real que la sesión de canvas sigue, no un fantasma de QDrag.

- La franja de título es accesible por el puente de automatización mediante su nombre accesible `panTitleBar`.
- Un umbral de arrastre de 6 px separa un clic (que activa el panadapter) de un arrastre.
- Todo lo que supere el umbral es consumido por el gesto de canvas para que el mecanismo de arrastre flotante nunca lo vea.
- Un elemento de canvas siempre puede abrirse en ventana flotante (incluso como el único pan), ya que la ocultación del botón en modo de pan único es una economía del modo de pila, no una regla sobre flotar. Cuando el elemento está fuera del canvas, el `setMultiPanMode()` de la pila reaplica su economía.
- Las señales de arrastre de canvas (`canvasDragBegan`, `canvasDragMoved`, `canvasDragEnded`) se emiten solo con posiciones globales mientras el applet está en el canvas y no está flotando.

## Indicadores

| Etiqueta | Estados posibles | Significado |
|----------|------------------|-------------|
| Estadísticas de CW | `<hz> Hz <wpm> WPM` | Tono y velocidad detectados del decodificador ggmorse |
| Sugerencia de CW | (requiere audio de PC) | Recordatorio de que el decodificador de CW necesita enrutamiento de audio de PC para funcionar |

## Detalles de Comportamiento

### Ventana flotante/Acoplar
Cuando está acoplado, al hacer clic en ⬈ se expulsa el panadapter a una ventana flotante. Cuando está flotando, al hacer clic en ↩ se vuelve a acoplar. El botón de ventana flotante está oculto en modo de pan único. Las ventanas flotantes no tienen marco y se pueden arrastrar mediante la franja de título y cambiar de tamaño mediante el agarre de la esquina inferior derecha. En macOS, cada ciclo de flotar/acoplar restablece los recursos de GPU para mantener el espectro activo. El estado guardado de la ventana flotante no se restaura cuando se agregan panadapters posteriores, evitando que aparezcan ventanas flotantes en blanco.

### Tamaño y Diseño
- Las barras de slider utilizan un `GuardedSlider` para evitar bucles de señal durante cambios programáticos.
- La altura del panel de decodificación de CW se puede ajustar entre 60 y 600 píxeles.
- El tamaño de fuente del texto decodificado varía de 8 a 32 píxeles, ajustable en incrementos de 1 píxel.

# Applet de Panadapter

El applet de Panadapter es un contenedor para una única visualización de panadapter (espectro FFT + waterfall) con una barra de título que ofrece agarre de arrastre, ventana flotante, maximizar y controles de cierre. Un panel opcional de decodificación CW puede aparecer debajo para la decodificación Morse fuera del aire.

## Controles

| Control | Tipo | Valor predeterminado | Rango | Clave de configuración | Comportamiento | Notas |
|---------|------|---------|-------|-------------|----------|-------|
| Título de slice | indicador | "Slice A" | Slice A..Slice H | *ninguno* | Muestra qué slice está vinculado a este panadapter. | |
| ⬈ / ↩ (ventana flotante/acoplar) | botón_pulsador | | | *ninguno* | Saca el panadapter a una ventana flotante o lo vuelve a acoplar. Oculto en modo de un solo pan. | La ventana flotante no tiene marco. Arrastre mediante la barra de título de la aplicación, redimensione mediante el agarre de tamaño inferior derecho. En macOS, cada ciclo de flotante/acoplado restablece los recursos de GPU y evita que el espectro se vuelva obsoleto. |
| □ (maximizar) | botón_pulsador | | | *ninguno* | Maximiza este panadapter en un diseño de varios paneles. Oculto en modo de un solo pan. |
| × (cerrar) | botón_pulsador | | | *ninguno* | Cierra este panadapter. Oculto en modo de un solo pan. |
| Espectro / waterfall | asa_arrastre | | | *ninguno* | Haga clic para activar el panadapter; arrastre para sintonizar, desplácese para hacer zoom. | |
| Etiqueta de estadísticas CW | indicador | | | *ninguno* | Muestra el tono y la velocidad de CW detectados (p. ej., "700 Hz 20 WPM"). | |
| Sens (sensibilidad del decodificador CW) | deslizador | 30 | 0-100 | CwDecoderSensitivity | Filtra decodificaciones de baja confianza. Los valores más altos son más estrictos. | Mapea 0-100 a un umbral de costo de 1.0-0.1. |
| 🔒P (Bloquear tono) | botón_de_alternancia | | | *ninguno* | Bloquea el tono del decodificador CW en la frecuencia sintonizada actual. | |
| 🔒S (Bloquear velocidad) | botón_de_alternancia | | | *ninguno* | Bloquea la velocidad del decodificador CW en las WPM actuales. | |
| Lo (tono mínimo) | deslizador | 500 | 300-1200 Hz | *ninguno* | Tono mínimo que busca el decodificador CW. Se limita automáticamente a ≤ Hi. | |
| Hi (tono máximo) | deslizador | 700 | 300-1200 Hz | *ninguno* | Tono máximo que busca el decodificador CW. Se limita automáticamente a ≥ Lo. | |
| A- (reducir tamaño de fuente) | botón_pulsador | | | *ninguno* | Disminuye el tamaño de fuente del texto decodificado en 1 píxel. | Se conserva entre sesiones. Nuevo en v26.7.4. |
| A+ (aumentar tamaño de fuente) | botón_pulsador | | | *ninguno* | Aumenta el tamaño de fuente del texto decodificado en 1 píxel. | Se conserva entre sesiones. Nuevo en v26.7.4. |
| CPY ALL | botón_pulsador | | | *ninguno* | Copia todo el texto decodificado al portapapeles. | |
| CPY VIS | botón_pulsador | | | *ninguno* | Copia solo el texto actualmente visible en el área de desplazamiento. | |
| CLR | botón_pulsador | | | *ninguno* | Borra el búfer de decodificación CW. | |
| ✕ (cerrar CW) | botón_pulsador | | | *ninguno* | Oculta el panel de decodificación CW por completo. | |
| Texto de decodificación CW | campo_de_texto | | | *ninguno* | Visualización continua de solo lectura del texto CW decodificado. Coloreado por confianza: verde (<0.15), amarillo (<0.35), naranja (<0.60), rojo (≥0.60). | El tamaño de fuente se puede ajustar mediante los controles A+/A-. |

## Controles del Panel de Decodificación CW

El panel de decodificación CW aparece en la parte inferior del panadapter cuando el modo CW está activo. Contiene:

- **Asa de redimensionamiento por arrastre**: Una tira delgada de 4 píxeles a lo largo del borde superior del panel. Arrastre hacia arriba o hacia abajo para redimensionar la altura del panel y revelar más historial de texto decodificado. La altura del panel se conserva entre sesiones (rango: 60-600 píxeles).
- **Barra de estadísticas**: Muestra el tono de CW (Hz) y la velocidad (WPM) detectados.
- **Deslizador de sensibilidad**: Ajusta la sensibilidad del decodificador (0-100).
- **Alternancias de bloqueo de tono/velocidad**: Bloquea los valores actuales de tono o velocidad.
- **Deslizadores de rango de tono**: Establecen el rango de búsqueda de tono mínimo y máximo (300-1200 Hz).
- **Controles de tamaño de fuente**: Los botones A- y A+ ajustan el tamaño de fuente del texto decodificado (8-32 píxeles). Los cambios se conservan y restauran en el próximo inicio.
- **Botones de copia**: CPY ALL copia todo el texto decodificado; CPY VIS copia solo el texto visible.
- **Botón CLR**: Borra el búfer de decodificación.
- **Botón de cierre (✕)**: Cierra el panel de decodificación CW.

## Comportamiento de Congelación del Waterfall

El waterfall se congela automáticamente cuando la radio entra en estado TRANSMITTING basado en el sistema de interbloqueo de la radio. Se descongela cuando el estado TRANSMITTING se despeja. Este comportamiento sigue el estado real del interbloqueo de hardware de la radio en lugar de un borde de software local, eliminando el artefacto de estela de TX de 10-23 segundos que podía aparecer después de desactivar la transmisión en versiones anteriores.

- En una sesión multiFLEX, cualquier cliente conectado que esté transmitiendo activa la congelación del waterfall en su panadapter.
- Al reconectar la radio, los FPS deseados del panadapter y la duración de la línea del waterfall se reafirman automáticamente para evitar que caigan al valor predeterminado de 10 Hz de la radio.

## Inicialización del Panadapter Secundario

Los panadapters secundarios (Slices B-H) ahora tienen su rango de dBm preparado al reconectar la radio. Esto asegura que el ajuste automático del piso de ruido comience desde la línea base correcta en lugar del rango predeterminado [-50, +50] que podía causar una visualización plana del espectro después de la reconexión.

## Indicadores

| Etiqueta | Estados posibles | Significado |
|-------|----------------|---------|
| Estadísticas CW | `<hz> Hz <wpm> WPM` | Tono y velocidad detectados por el decodificador ggmorse |
| Sugerencia CW | (requiere audio de PC) | Recordatorio de que el decodificador CW necesita enrutamiento de audio de PC para funcionar |

## Detalles de Comportamiento

### Ventana Flotante/Acoplar
Cuando está acoplado, al hacer clic en ⬈ se saca el panadapter a una ventana flotante. Cuando está flotando, al hacer clic en ↩ se vuelve a acoplar. El botón de ventana flotante está oculto en modo de un solo pan. Las ventanas flotantes no tienen marco y pueden arrastrarse mediante la barra de título y redimensionarse mediante el agarre de tamaño inferior derecho. En macOS, cada ciclo de flotante/acoplado restablece los recursos de GPU para mantener el espectro activo. El estado guardado de la ventana flotante no se restaura cuando se añaden panadapters posteriores, evitando que aparezcan ventanas flotantes en blanco.

### Dimensionamiento y Diseño
- Las barras deslizadoras utilizan un `GuardedSlider` para evitar bucles de señal durante cambios programáticos.
- La altura del panel de decodificación CW se puede ajustar entre 60 y 600 píxeles.
- El tamaño de fuente del texto decodificado varía de 8 a 32 píxeles, ajustable en incrementos de 1 píxel.

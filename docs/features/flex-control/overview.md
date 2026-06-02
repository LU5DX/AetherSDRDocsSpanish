# Resumen de AetherControl / FlexControl

AetherControl es un cuadro de diálogo de configuración dedicado para el controlador rotatorio de hardware FlexControl y su equivalente virtual en pantalla. Úselo para sintonizar la franja activa, asignar acciones a botones físicos o virtuales y ajustar el comportamiento de la rueda virtual.

## Antes de comenzar

- **No es necesaria** una conexión de radio para configurar el cuadro de diálogo: los ajustes se guardan y surten efecto cuando una radio está disponible.

## Cómo funciona

El cuadro de diálogo AetherControl proporciona una rueda de sintonización virtual y un panel de configuración tanto para el dispositivo físico FlexControl como para la rueda virtual en pantalla.

**Rueda virtual** — Un control circular renderizado en pantalla que se gira con el ratón o gestos táctiles. Muestra la franja activa, la frecuencia y el modo. El movimiento se traduce en pasos de sintonización según la configuración de Sensibilidad del ratón y Apriete de la rueda. Haga doble clic en la perilla para capturar la entrada del ratón y sintonizar circularmente; haga doble clic nuevamente para liberar. Presione Escape como vía de liberación secundaria.

**FlexControl físico** — Cuando un controlador de hardware FlexControl genuino está conectado a través de un puerto serie, el cuadro de diálogo muestra su estado de conexión y nombre de puerto. Use los botones Detectar y Cerrar para administrar el dispositivo físico. Cuando está conectado, la rueda física y los botones funcionan en paralelo con la rueda virtual. Si el dispositivo se reinicia (por ejemplo, al encender), AetherSDR reenvía automáticamente el estado LED almacenado en caché para que el hardware coincida con el botón de modo de rueda activo de la aplicación.

**Acciones de botón** — La propia rueda tiene una asignación de acción de pulsación (un toque) y doble toque. Cinco botones auxiliares admiten sus propias acciones de un toque y doble toque. Las acciones disponibles incluyen sintonización, cambio de modo, control de zoom, RIT/XIT, volumen, umbral AGC, APF, macros CWX, gestión de franjas y MOX.

**Modo compacto** — Oculta los botones auxiliares, mostrando solo la rueda y la lectura de frecuencia para una interfaz mínima. Se activa mediante el botón Compacto.

**Giro externo** — Habilita un gesto de giro de rueda al arrastrar en el panadapter fuera de este cuadro de diálogo. Los cambios de frecuencia de fuentes externas (por ejemplo, hacer clic en el panadapter) activan una breve animación de rotación de la rueda.

**Invertir** — Invierte la dirección en que la rotación de la rueda mueve la frecuencia: en el sentido de las agujas del reloj sintoniza hacia abajo en lugar de hacia arriba (o viceversa).

**Apriete de la rueda** — Control deslizante (0–100, predeterminado 45) que controla cuánto se desliza la rueda virtual después de soltarla. 0 = se detiene inmediatamente (apretada); 100 = continúa girando durante mucho tiempo (suelta). Se almacena en `FlexControlVirtualWheel` (JSON, campo `looseness`). Afecta principalmente a la entrada del panel táctil; no cambia el comportamiento del FlexControl físico.

**Sensibilidad del ratón** — Control deslizante (0–100, predeterminado 50) que escala cuánto movimiento del puntero se necesita para girar la rueda virtual. El punto medio (50) es escala 1,0×. 0 = se necesita menos movimiento; 100 = se necesita más movimiento. Se almacena en `FlexControlVirtualWheel` (JSON, campo `sensitivity`). Afecta principalmente a la entrada del panel táctil; no cambia el comportamiento del FlexControl físico.

**Botones auxiliares (1–5)** — Cinco botones configurables, cada uno con su propio cuadro combinado de acción de un toque y doble toque. Los botones muestran la selección activa mediante puntos auxiliares.

**Acciones configurables** — Las siguientes acciones están disponibles para cualquier asignación de botón:

| ID de acción | Etiqueta |
|-----------|-------|
| WheelFrequency | Sintonizar franja |
| BandZoom | Zoom de banda |
| SegmentZoom | Zoom de segmento |
| WheelRit | RIT (Sintonización incremental de recepción) |
| WheelXit | XIT (Sintonización incremental de transmisión) |
| WheelVolume | Volumen maestro |
| WheelHeadphoneVolume | Volumen de auriculares |
| WheelAgcT | AGCT (Umbral de control automático de ganancia) |
| WheelApf | APF (Filtro de pico de audio) |
| ClearRit | Borrar RIT |
| ClearXit | Borrar XIT |
| ToggleApf | Alternar APF |
| NextSlice | Cambiar franja activa |
| SplitActiveSlice | Dividir franja activa |
| ToggleMox | MOX |
| WheelPower | Potencia de RF |
| WheelCwSpeed | Velocidad CW |
| CwxF1–CwxF12 | Macro CWX 1–12 |
| StepUp | Subir paso |
| StepDown | Bajar paso |
| ToggleTune | Alternar sintonización |
| ToggleMute | Alternar silencio |
| ToggleLock | Alternar bloqueo |
| PrevSlice | Franja anterior |
| ToggleAgc | Alternar AGC |
| VolumeUp | AF de franja arriba |
| VolumeDown | AF de franja abajo |
| None | Ninguna |

## Consejos

- Los controles deslizantes de Apriete de la rueda y Sensibilidad del ratón están diseñados principalmente para usuarios de panel táctil. Los topes mecánicos de un FlexControl físico no se ven afectados.
- La rueda virtual utiliza una lógica antirrebote que limita los movimientos del puntero de evento único a 15° (π/12 radianes) para evitar saltos repentinos.
- Haga doble clic en la perilla virtual para capturar la entrada del ratón y vuelva a hacer doble clic para liberarla. Esto reemplaza el comportamiento anterior de captura con un solo clic que requería Escape para liberar.
- Si el FlexControl físico se reinicia, AetherSDR restaura automáticamente el estado LED correcto para el botón de modo de rueda activo.

## Relacionado

- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Set up aux buttons with single- and double-tap actions](set-up-aux-buttons-with-single-and-double-tap-actions.md)
- [Adjust wheel tightness (coasting feel)](adjust-wheel-tightness-coasting-feel.md)
- [Adjust mouse sensitivity for the virtual wheel](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Toggle compact mode for a minimal controller UI](toggle-compact-mode-for-a-minimal-controller-ui.md)
- [Toggle Auto Spin for external frequency change animation](toggle-auto-spin-for-external-frequency-change-animation.md)
- [Toggle Reverse to invert tuning direction](toggle-reverse-to-invert-tuning-direction.md)
- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)

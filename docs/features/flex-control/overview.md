# Resumen de AetherControl / FlexControl

AetherControl es un diálogo de configuración dedicado para el controlador rotatorio físico FlexControl y su equivalente virtual en pantalla. Úselo para sintonizar el slice activo, asignar acciones a botones físicos o virtuales y ajustar el comportamiento de la rueda virtual.

## Antes de comenzar

- **No es necesario** tener una conexión de radio para configurar el diálogo: los ajustes se guardan y surten efecto cuando una radio esté disponible.

## Cómo funciona

El diálogo AetherControl proporciona una rueda de sintonización virtual y un panel de configuración tanto para el dispositivo FlexControl físico como para la rueda virtual en pantalla.

**Rueda virtual** — Un control circular renderizado en pantalla que se gira con el ratón o gestos táctiles. Muestra el slice activo, la frecuencia y el modo. El movimiento se traduce en pasos de sintonización según los ajustes de sensibilidad del ratón y la rigidez de la rueda. Haga doble clic en la perilla para capturar la entrada del ratón para sintonización circular; vuelva a hacer doble clic para liberarla. Presione Escape como ruta de liberación secundaria.

**FlexControl físico** — Cuando un controlador FlexControl genuino está conectado mediante un puerto serie, el diálogo muestra su estado de conexión y el nombre del puerto. Use los botones Detectar y Cerrar para gestionar el dispositivo físico. Cuando está conectado, la rueda y los botones físicos funcionan en paralelo con la rueda virtual. Si el dispositivo se reinicia (por ejemplo, al encenderse), AetherSDR reemite automáticamente el estado LED almacenado en caché para que el hardware coincida con el botón de modo de rueda activo de la aplicación.

**Acciones de botones** — La rueda misma tiene una asignación de acción de pulsación (un solo toque) y doble toque. Cinco botones auxiliares admiten cada uno sus propias acciones de un solo toque y doble toque. Las acciones disponibles incluyen sintonización, cambio de modo, control de zoom, RIT/XIT, volumen, umbral AGC, APF, macros CWX, gestión de slices y MOX.

**Modo compacto** — Oculta los botones auxiliares, mostrando solo la rueda y la lectura de frecuencia para una interfaz mínima. Se activa mediante el botón Compacto.

**Giro externo** — Habilita un gesto de giro de rueda al arrastrar en el panadapter fuera de este diálogo. Los cambios de frecuencia desde fuentes externas (por ejemplo, al hacer clic en el panadapter) activan una breve animación de rotación de la rueda.

**Invertir** — Invierte la dirección en la que la rotación de la rueda mueve la frecuencia: en sentido horario sintoniza hacia abajo en lugar de hacia arriba (o viceversa).

**Rigidez de la rueda** — Control deslizante (0–100, predeterminado 45) que controla cuánto se desliza la rueda virtual después de soltarla. 0 = se detiene inmediatamente (rígida); 100 = continúa girando durante mucho tiempo (suelta). Se almacena en `FlexControlVirtualWheel` (JSON, campo `looseness`). Afecta principalmente la entrada del trackpad; no cambia el comportamiento del FlexControl físico.

**Sensibilidad del ratón** — Control deslizante (0–100, predeterminado 50) que escala cuánto movimiento del puntero se necesita para girar la rueda virtual. El punto medio (50) es escala 1,0×. 0 = menos movimiento necesario; 100 = más movimiento necesario. Se almacena en `FlexControlVirtualWheel` (JSON, campo `sensitivity`). Afecta principalmente la entrada del trackpad; no cambia el comportamiento del FlexControl físico.

**Botones auxiliares (1–5)** — Cinco botones configurables, cada uno con su propio cuadro combinado de acción de un solo toque y doble toque. Los botones muestran la selección activa mediante puntos auxiliares.

**Acciones configurables** — Las siguientes acciones están disponibles para cualquier asignación de botón:

| ID de acción | Etiqueta |
|-----------|-------|
| WheelFrequency | Sintonizar slice |
| BandZoom | Zoom de banda |
| SegmentZoom | Zoom de segmento |
| WheelRit | RIT (sintonización incremental de recepción) |
| WheelXit | XIT (sintonización incremental de transmisión) |
| WheelVolume | Volumen maestro |
| WheelSliceAudio | Volumen de audio del slice |
| WheelHeadphoneVolume | Volumen de auriculares |
| WheelAgcT | AGCT (umbral de control automático de ganancia) |
| WheelApf | APF (filtro de pico de audio) |
| ClearRit | Borrar RIT |
| ClearXit | Borrar XIT |
| ToggleApf | Alternar APF |
| NextSlice | Cambiar slice activo |
| SplitActiveSlice | Dividir slice activo |
| ToggleMox | MOX |
| WheelPower | Potencia de RF |
| WheelCwSpeed | Velocidad de CW |
| CwxF1–CwxF12 | Macro CWX 1–12 |
| StepUp | Paso arriba |
| StepDown | Paso abajo |
| ToggleTune | Alternar sintonización |
| ToggleMute | Alternar silencio |
| ToggleLock | Alternar bloqueo |
| PrevSlice | Slice anterior |
| ToggleAgc | Alternar AGC |
| VolumeUp | Subir AF del slice |
| VolumeDown | Bajar AF del slice |
| None | Ninguna |

## Consejos

- Los controles deslizantes de rigidez de la rueda y sensibilidad del ratón están diseñados principalmente para usuarios de trackpad. Los topes mecánicos de un FlexControl físico no se ven afectados.
- La rueda virtual utiliza lógica anti-fluctuación que limita los movimientos del puntero de un solo evento a 15° (π/12 radianes) para evitar saltos repentinos.
- Haga doble clic en la perilla virtual para capturar la entrada del ratón y vuelva a hacer doble clic para liberarla. Esto reemplaza el comportamiento anterior de captura con un solo clic que requería Escape para liberar.
- Si el FlexControl físico se reinicia, AetherSDR restaura automáticamente el estado LED correcto para el botón de modo de rueda activo.

## Relacionados

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

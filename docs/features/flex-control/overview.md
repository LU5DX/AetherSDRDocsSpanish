# Descripción general de AetherControl / FlexControl

AetherControl es un diálogo de configuración dedicado para el controlador rotativo hardware FlexControl y su equivalente virtual en pantalla. Utilícelo para sintonizar el slice activo, asignar acciones a los botones físicos o virtuales y ajustar el comportamiento de la rueda virtual.

## Antes de comenzar

- **No se requiere** una conexión de radio para configurar el diálogo: los ajustes se guardan y surten efecto cuando hay una radio disponible.

## Cómo funciona

El diálogo AetherControl proporciona una rueda de sintonización virtual y un panel de configuración tanto para el dispositivo físico FlexControl como para la rueda virtual en pantalla.

**Rueda virtual** — Un control circular renderizado en pantalla que se rota con gestos de mouse o táctiles. Muestra el slice activo, la frecuencia y el modo. El movimiento se convierte en pasos de sintonización según los ajustes de Sensibilidad del mouse y Ajuste de la rueda. Haga doble clic en la perilla para capturar la entrada del mouse para la sintonización circular; haga doble clic nuevamente para liberarla. Presione Escape como vía alternativa de liberación.

**FlexControl físico** — Cuando un controlador hardware FlexControl genuino está conectado a través de un puerto serie, el diálogo muestra su estado de conexión y el nombre del puerto. Use los botones Detect y Close para administrar el dispositivo físico. Cuando está conectado, la rueda y los botones físicos funcionan en paralelo con la rueda virtual. Si el dispositivo se reinicia (por ejemplo, al encenderse), AetherSDR re-emite automáticamente el estado de LED en caché para que el hardware coincida con el botón de modo de rueda activo de la aplicación. Si el dispositivo se desconecta o el puerto deja de estar disponible, AetherSDR reintenta automáticamente la conexión con retroceso exponencial y vuelve a detectar el puerto en caso de que el dispositivo se haya re-enumerado con un puerto COM diferente. Los primeros reintentos ocurren cada 2 segundos; si el dispositivo sigue ausente, el intervalo se amplía hasta un máximo de 30 segundos para evitar saturar el registro.

**Acciones de botones** — La rueda en sí tiene una asignación de acción de pulsación (un toque) y doble pulsación. Cinco botones auxiliares admiten cada uno sus propias acciones de un toque y doble pulsación. Las acciones disponibles incluyen sintonización, cambio de modo, control de zoom, RIT/XIT, volumen, umbral de AGC, APF, macros CWX, administración de slices y MOX.

**Modo compacto** — Oculta los botones auxiliares, mostrando solo la rueda y la lectura de frecuencia para una interfaz mínima. Se activa mediante el botón Compact.

**Giro externo** — Habilita un gesto de giro de rueda al arrastrar sobre el panadapter fuera de este diálogo. Los cambios de frecuencia de fuentes externas (por ejemplo, al hacer clic en el panadapter) activan una breve animación de rotación de la rueda.

**Invertir (Reverse)** — Invierte la dirección en que la rotación de la rueda mueve la frecuencia: en el sentido horario sintoniza hacia abajo en lugar de hacia arriba (o viceversa).

**Ajuste de la rueda (Wheel Tightness)** — Control deslizante (0–100, predeterminado 45) que controla cuánto continúa girando la rueda virtual después de soltarla. 0 = se detiene inmediatamente (apretada); 100 = continúa girando durante mucho tiempo (suelta). Se almacena en `FlexControlVirtualWheel` (JSON, campo `looseness`). Afecta principalmente la entrada del trackpad; no cambia el comportamiento del FlexControl físico. Está etiquetado con Apretada y Suelta en los extremos.

**Sensibilidad del mouse** — Control deslizante (0–100, predeterminado 50) que escala cuánto movimiento del puntero se requiere para girar la rueda virtual. El punto medio (50) es una escala de 1.0×. 0 = se necesita menos movimiento; 100 = se necesita más movimiento. Se almacena en `FlexControlVirtualWheel` (JSON, campo `sensitivity`). Afecta principalmente la entrada del trackpad; no cambia el comportamiento del FlexControl físico. Está etiquetado con Menos y Más en los extremos.

**Botones auxiliares (1–5)** — Cinco botones configurables, cada uno con su propio cuadro combinado de acción de un toque y doble pulsación. Los botones muestran la selección activa mediante los puntos auxiliares.

## Diseño del diálogo y desplazamiento

El diálogo AetherControl contiene un área de desplazamiento que se activa automáticamente cuando el contenido excede la altura de pantalla disponible. Esto permite que el controlador completo siga siendo utilizable incluso en pantallas pequeñas o de alta densidad de píxeles (high-DPI). El área de desplazamiento tiene un ancho mínimo de 430 píxeles y una altura mínima de 610 píxeles (o la altura de pantalla disponible, la que sea menor) para evitar el recorte del contenido.

**Acciones configurables** — Las siguientes acciones están disponibles para cualquier asignación de botón:

| ID de acción | Etiqueta |
|-----------|-------|
| WheelFrequency | Sintonizar Slice |
| BandZoom | Zoom de Banda |
| SegmentZoom | Zoom de Segmento |
| WheelRit | RIT (Sintonización Incremental de Recepción) |
| WheelXit | XIT (Sintonización Incremental de Transmisión) |
| WheelVolume | Volumen Maestro |
| WheelSliceAudio | Volumen de Audio del Slice |
| WheelHeadphoneVolume | Volumen de Auriculares |
| WheelAgcT | AGCT (Umbral de Control Automático de Ganancia) |
| WheelApf | APF (Filtro de Enfatización de Audio) |
| ClearRit | Borrar RIT |
| ClearXit | Borrar XIT |
| ToggleApf | Alternar APF |
| NextSlice | Cambiar Slice Activo |
| SplitActiveSlice | Dividir Slice Activo |
| ToggleMox | MOX |
| WheelPower | Potencia de RF |
| WheelCwSpeed | Velocidad CW |
| CwxF1–CwxF12 | Macro CWX 1–12 |
| StepUp | Paso Arriba |
| StepDown | Paso Abajo |
| ToggleTune | Alternar Sintonización |
| ToggleMute | Alternar Silencio |
| ToggleLock | Alternar Bloqueo |
| PrevSlice | Slice Anterior |
| ToggleAgc | Alternar AGC |
| VolumeUp | AF del Slice Arriba |
| VolumeDown | AF del Slice Abajo |
| None | Ninguna |

## Consejos

- Los controles deslizantes de Ajuste de la rueda y Sensibilidad del mouse están diseñados principalmente para usuarios de trackpad. Los retenes mecánicos de un FlexControl físico no se ven afectados.
- La rueda virtual usa lógica de eliminación de rebotes que limita los movimientos de un solo evento del puntero a 15° (π/12 radianes) para evitar saltos repentinos.
- La rueda virtual usa re-anclaje diferido: cuando el puntero cruza la zona muerta central, el ancla se suelta; el siguiente movimiento re-ancla sin calcular un delta.
- Haga doble clic en la perilla virtual para capturar la entrada del mouse, y haga doble clic nuevamente para liberarla. Esto reemplaza el comportamiento anterior de captura con un solo clic que requería Escape para liberar.
- Si el FlexControl físico se reinicia, AetherSDR restaura automáticamente el estado de LED correcto para el botón de modo de rueda activo.
- Si el FlexControl físico se desconecta o su puerto deja de estar disponible, AetherSDR reintenta automáticamente la conexión y vuelve a detectar el puerto, en caso de que el dispositivo se haya re-enumerado con un puerto COM diferente.
- El diálogo ahora incluye un área de desplazamiento que se activa cuando el contenido excede la altura de pantalla disponible, lo que lo hace más utilizable en pantallas pequeñas o de alta densidad de píxeles (#3662, #4365).

## Relacionado

- [Configure el controlador hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configure las acciones de uno y dos toques para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Configure los botones auxiliares con acciones de uno y dos toques](set-up-aux-buttons-with-single-and-double-tap-actions.md)
- [Ajuste el ajuste de la rueda (sensación de deslizamiento)](adjust-wheel-tightness-coasting-feel.md)
- [Ajuste la sensibilidad del mouse para la rueda virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Active el modo compacto para una interfaz de controlador mínima](toggle-compact-mode-for-a-minimal-controller-ui.md)
- [Active el Giro automático para la animación de cambio de frecuencia externo](toggle-auto-spin-for-external-frequency-change-animation.md)
- [Active Invertir (Reverse) para invertir la dirección de sintonización](toggle-reverse-to-invert-tuning-direction.md)
- [Asigne las acciones de pulsación y doble pulsación a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)

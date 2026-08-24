# Use el volante virtual para sintonizar la rebanada activa

Use el volante de sintonización virtual en pantalla en el diálogo AetherControl para cambiar la frecuencia de la rebanada actualmente activa con gestos de mouse o trackpad, simulando la sensación de un control rotatorio físico.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`

## Pasos

1. En el diálogo AetherControl, localice el control **Wheel** en la parte superior. Muestra la frecuencia y el modo actuales de la rebanada.
2. Haga doble clic en el volante para capturar la entrada del mouse para la sintonización circular. El volante queda activo para gestos de sintonización.
3. Arrastre en un movimiento circular alrededor del volante para sintonizar. Arrastre en el sentido de las agujas del reloj para aumentar la frecuencia, y en sentido contrario para disminuirla.
4. Para liberar la captura del mouse, haga doble clic en el volante nuevamente. Presione Escape como vía secundaria de liberación.
5. (Opcional) Para invertir la dirección de sintonización, haga clic en **Reverse**.
6. (Opcional) Para habilitar la sintonización basada en el panadapter, haga clic en **External Spin**. Cuando está habilitado, arrastrar sobre el panadapter también activa la sintonización por volante.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|
| **Wheel** | — | — | Ninguna (muestra la rebanada actual) |
| **Physical** | — | — | Ninguna (muestra el estado de conexión) |
| **Compact** | Off | On/Off | Ninguna |
| **External Spin** | Off | On/Off | `FlexControlVirtualExternalSpin` |
| **Reverse** | Off | On/Off | `FlexControlInvertDir` |
| **Push (action)** | — | — | `FlexControlButtonAction_*` |
| **Double-tap (action)** | — | — | Ninguna |
| **Wheel Tightness** | 45 | 0–100 (0 = firme, 100 = suelto) | `FlexControlVirtualWheel` (campo JSON anidado `looseness`) |
| **Mouse Sensitivity** | 50 | 0–100 (0 = menos, 100 = más) | `FlexControlVirtualWheel` (campo JSON anidado `sensitivity`) |
| **Aux buttons 1–5** | — | 5 botones | Ninguna |

## Opciones de acción del volante

Las siguientes acciones están disponibles para los controles basados en volante (Push, Double-tap y combinaciones de botones auxiliares):

| ID de acción | Descripción |
|---|---|
| `WheelRit` | RIT (Receive Incremental Tuning) |
| `WheelXit` | XIT (Transmit Incremental Tuning) |
| `WheelVolume` | Volumen maestro |
| `WheelSliceAudio` | Volumen de audio de la rebanada |
| `WheelHeadphoneVolume` | Volumen de auriculares |
| `WheelAgcT` | AGCT (umbral de control automático de ganancia) |
| `WheelApf` | APF (filtro de pico de audio) |

## Botones auxiliares

El diálogo proporciona cinco botones auxiliares configurables (etiquetados con puntos auxiliares para indicar la selección activa). Cada botón tiene:

- **Aux single-tap combo**: Asigna una acción al toque único del botón auxiliar seleccionado.
- **Aux double-tap combo**: Asigna una acción al doble toque del botón auxiliar seleccionado.

Estos ajustes se almacenan por botón auxiliar.

## Consejos

- La captura del mouse se ha simplificado a un solo conmutador de doble clic: doble clic para capturar, doble clic nuevamente para liberar. Esto reemplaza el comportamiento anterior de clic para capturar y Escape para liberar, para una experiencia de usuario más limpia.
- El volante virtual responde a arrastres circulares con el mouse o trackpad. Los deltas de puntero de un solo evento se limitan a 15° (π/12 radianes) por evento para reducir la vibración.
- Cuando el puntero cruza la zona muerta central, el ancla se restablece. El siguiente movimiento inicia un nuevo gesto de sintonización sin calcular un delta.
- **Wheel Tightness** y **Mouse Sensitivity** se almacenan juntos en un único objeto JSON bajo `FlexControlVirtualWheel`. En versiones anteriores, Wheel Tightness se almacenaba por separado como `FlexControlVirtualWheelLooseness`; esto se migra automáticamente en la primera lectura.
- El volante muestra la frecuencia de la rebanada en Hz y el modo actual (por ejemplo, USB, CW, AM).
- Haga clic en **Compact** para alternar el modo compacto, que oculta los botones auxiliares y muestra solo el volante y la frecuencia para una interfaz mínima.
- El indicador **Physical** muestra el estado de conexión y el nombre del puerto del FlexControl físico. Use los botones Detect/Close para gestionar el dispositivo físico.
- La ventana del diálogo ahora contiene un área de desplazamiento. Cuando el controlador completo excede la altura disponible de la pantalla, el contenido se desplaza verticalmente para que la ventana pueda ser más pequeña que la altura total del controlador. El ancho mínimo de la ventana se establece al ancho mínimo del contenido para evitar recortes horizontales.
- En pantallas bajas o con escala DPI, la altura de la ventana se limita a la altura disponible de la pantalla al abrir, y el contenido se vuelve desplazable en lugar de forzarse al modo compacto.

## Fiabilidad de la conexión física FlexControl

La conexión física FlexControl ahora incluye detección automática de errores y reconexión. Si el dispositivo se desconecta (por ejemplo, cuando se desconecta el cable USB), AetherControl detecta el error y reintenta automáticamente la reconexión.

- Al desconectarse, AetherControl intenta volver a detectar el dispositivo inmediatamente y luego reintenta cada 2 segundos durante los primeros intentos.
- Si el dispositivo sigue ausente, el intervalo de reintento se reduce gradualmente, duplicándose después de cada intento fallido hasta alcanzar un máximo de 30 segundos. Esto evita el escaneo rápido continuo y las advertencias de registro durante una interrupción prolongada.
- Cuando el dispositivo se reconecta, AetherControl lo detecta en su nuevo nombre de puerto (si la re-enumeración USB lo cambió) y se reconecta automáticamente. El indicador **Physical** se actualiza para mostrar el nuevo estado de conexión y nombre del puerto.
- Una conexión se considera "deseada" una vez que hace clic en **Detect**. Cerrar el puerto con **Close** limpia el estado de reintento y detiene los intentos de reconexión.

## Relacionado

- [Ajustar la sensibilidad del mouse para el volante virtual](adjust-mouse-sensitivity-for-the-virtual-wheel.md)
- [Ajustar la firmeza del volante (sensación de inercia)](adjust-wheel-tightness-coasting-feel.md)
- [Alternar Reverse para invertir la dirección de sintonización](toggle-reverse-to-invert-tuning-direction.md)
- [Alternar Auto Spin para la animación de cambio de frecuencia externo](toggle-auto-spin-for-external-frequency-change-animation.md)

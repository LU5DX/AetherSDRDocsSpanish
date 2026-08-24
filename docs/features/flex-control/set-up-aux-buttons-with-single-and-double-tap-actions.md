# AetherControl / FlexControl

Configure el controlador rotatorio físico AetherControl / FlexControl, incluida la sintonización con rueda virtual, la asignación de acciones al botón pulsador y cinco botones auxiliares con acciones de toque simple y doble.

## Antes de comenzar

- Abra el diálogo de AetherControl: `Settings > AetherControl...`
- Familiarícese con la [descripción general](overview.md) del controlador

## Qué hace cada control

| Control | Descripción | Claves de configuración |
|---|---|---|
| Wheel | Rueda virtual FlexControl: gírela con el mouse/táctil para sintonizar el slice activo. Muestra la frecuencia y el modo. Doble clic para capturar la sintonización circular; doble clic nuevamente para liberarla. Presione Escape como vía secundaria de liberación. | Ninguna |
| Physical | Muestra el estado de conexión y el nombre del puerto del FlexControl físico. Botones Detect/Close para gestionar el dispositivo físico. | Ninguna |
| Compact | Alterna el modo compacto: oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima. El área de contenido se desplaza si la altura del diálogo supera el espacio de trabajo disponible en pantalla. | Ninguna |
| External Spin | Habilita la sintonización con rueda externa: arrastrar sobre el panadapter activa gestos de sintonización con rueda. | Ninguna |
| Reverse | Invierte la dirección de sintonización de la rueda. | Ninguna |
| Push (action) | Asigna una acción al presionar la rueda (toque simple). Las opciones incluyen ciclo de modo, zoom por pasos, restablecer zoom, banda arriba/abajo y más. | `FlexControlButtonAction_*` |
| Double-tap (action) | Asigna una acción al doble toque de la rueda. | Ninguna |
| Wheel Tightness | Ajusta el arrastre de inercia de la rueda virtual; 0 = firme (detención rápida), 100 = suelto (inercia larga). Principalmente para trackpads; no afecta al FlexControl físico. Se almacena como parte de un objeto JSON anidado bajo `FlexControlVirtualWheel`. Anteriormente se almacenaba con la clave plana heredada `FlexControlVirtualWheelLooseness`; se migra automáticamente al leerla. | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Mouse Sensitivity | Ajusta cuánto movimiento capturado del mouse/trackpad hace girar la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. El supresor de rebotes limita los deltas de puntero de un solo evento a 15° (π/12). Reanclaje perezoso: cuando el puntero cruza la zona muerta central, el ancla se descarta; el siguiente movimiento reancla sin calcular un delta. | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| Aux buttons (1–5) | Seleccione un botón auxiliar para configurar. El botón activo se muestra con un punto verde. | Ninguna |
| Aux single-tap combo | Asigna una acción al toque simple del botón auxiliar seleccionado. | `FlexControlBtn1Action0` – `FlexControlBtn4Action0` |
| Aux double-tap combo | Asigna una acción al doble toque del botón auxiliar seleccionado. | `FlexControlBtn1Action1` – `FlexControlBtn4Action1` |

## Configurar acciones de botones auxiliares

1. Haga clic en uno de los cinco botones auxiliares numerados para seleccionarlo. El botón seleccionado se resalta en verde.
2. En el cuadro combinado de toque simple debajo de los botones auxiliares, seleccione una acción para el toque simple.
3. En el cuadro combinado de doble toque debajo de los botones auxiliares, seleccione una acción para el doble toque.
4. Repita para cada botón auxiliar que desee configurar.

## Acciones disponibles

Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, **Slice Audio Volume**, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macro 1–12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down, None.

## Reconexión del dispositivo físico

El diálogo se reconecta automáticamente si el dispositivo FlexControl físico se desconecta y reaparece en el sistema:

- Cuando el dispositivo se desconecta o la conexión USB se pierde, el diálogo registra el error una vez y comienza a reintentar.
- Los reintentos comienzan con intervalos de 2 segundos y aumentan exponencialmente hasta 30 segundos.
- En cada reintento, el puerto se vuelve a detectar en lugar de reutilizar el nombre anterior, por lo que una re-enumeración USB que asigne un puerto COM diferente se maneja automáticamente.
- Cuando un dispositivo FlexControl físico envía un comando de inicio/restablecimiento (por ejemplo, `F0304;`), el diálogo reemite automáticamente el estado del LED para garantizar que el hardware coincida con el botón de modo de rueda activo de la aplicación.
- Si el dispositivo sigue presente pero bloqueado (no se puede abrir), el diálogo reintenta en lugar de informar una conexión falsa.

## Consejos

- Un doble toque debe completarse dentro de los 230 ms posteriores al primer toque. Si toca demasiado lento, la acción se dispara como dos toques simples.
- Las acciones que son controles continuos (Tune Slice, Master Volume, etc.) enganchan el botón auxiliar en un modo de sintonización. Las acciones de un solo disparo (Step Up, Toggle MOX, macros) se ejecutan inmediatamente y no se enganchan.
- La rueda virtual usa doble clic para capturar y liberar el modo de sintonización circular. Un clic simple no cambia el estado de captura.
- Slice Audio Volume le permite ajustar el volumen de audio del slice activo de forma independiente con la rueda, sin afectar el volumen maestro ni otros slices.
- El diálogo usa un área de desplazamiento en modo no compacto. Si la altura de su pantalla es limitada o usa escala de alta DPI, el contenido se desplaza verticalmente para que el controlador completo siga siendo accesible. La ventana no se puede redimensionar a una altura mayor que el espacio de trabajo disponible en pantalla.

## Relacionado

- [Configure single- and double-tap actions for the PUSH button](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Map push-button and double-tap actions to the wheel](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)

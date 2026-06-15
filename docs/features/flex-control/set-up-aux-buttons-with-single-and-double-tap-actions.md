# Configurar botones auxiliares con acciones de un toque y doble toque

Configure los cinco botones auxiliares en el diálogo AetherControl / FlexControl para que cada botón pueda disparar una acción diferente con un toque simple o un doble toque.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`
- Familiarícese con la [descripción general](overview.md) del controlador

## Pasos

1. Haga clic en uno de los cinco botones auxiliares numerados para seleccionarlo. El botón seleccionado se resalta en verde.
2. En el cuadro combinado de un toque debajo de los botones auxiliares, seleccione una acción para un toque simple.
3. En el cuadro combinado de doble toque debajo de los botones auxiliares, seleccione una acción para un doble toque.
4. Repita para cada botón auxiliar que desee configurar.

## Qué hace cada control

| Control | Descripción | Claves de configuración |
|---|---|---|
| Wheel | Rueda virtual FlexControl: gírela con el mouse/táctil para sintonizar el slice activo. Muestra la frecuencia y el modo. Haga doble clic para capturar la sintonización circular; vuelva a hacer doble clic para liberarla. Presione Escape como ruta de liberación secundaria. | Ninguna |
| Physical | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Botones Detect/Close para gestionar el dispositivo físico. | Ninguna |
| Compact | Alterna el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia para una interfaz mínima. | Ninguna |
| External Spin | Habilita la sintonización con rueda externa: arrastrar en el panadapter activa gestos de sintonización con rueda. | Ninguna |
| Reverse | Invierte la dirección de sintonización de la rueda. | Ninguna |
| Push (acción) | Asigna una acción al presionar la rueda (un toque). Las opciones incluyen ciclo de modo, zoom por pasos, restablecer zoom, banda arriba/abajo y más. | `FlexControlButtonAction_*` |
| Double-tap (acción) | Asigna una acción al hacer doble toque en la rueda. | Ninguna |
| Wheel Tightness | Ajusta el arrastre de la rueda virtual; 0 = ajustado (parada rápida), 100 = suelto (arrastre largo). Principalmente para trackpads; no afecta al FlexControl físico. Se almacena como parte de un objeto JSON anidado bajo `FlexControlVirtualWheel`. | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Mouse Sensitivity | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. El anti-trepidación limita los deltas de puntero de un solo evento a 15° (π/12). Reanclaje perezoso: cuando el puntero cruza la zona muerta central, se suelta el ancla; el siguiente movimiento reancla sin calcular un delta. | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| Aux buttons (1–5) | Seleccione un botón auxiliar para configurar. El botón activo se muestra con un punto verde. | Ninguna |
| Aux single-tap combo | Asigna una acción a un toque simple del botón auxiliar seleccionado. | `FlexControlBtn1Action0` – `FlexControlBtn4Action0` |
| Aux double-tap combo | Asigna una acción a un doble toque del botón auxiliar seleccionado. | `FlexControlBtn1Action1` – `FlexControlBtn4Action1` |

Las acciones disponibles son:

Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, **Slice Audio Volume**, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macro 1–12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down, None.

## Consejos

- Un doble toque debe completarse dentro de los 230 ms del primer toque. Si toca demasiado lento, la acción se dispara como dos toques simples.
- Las acciones que son controles continuos (Tune Slice, Master Volume, etc.) enganchan el botón auxiliar en un modo de sintonización. Las acciones de un solo disparo (Step Up, Toggle MOX, macros) se ejecutan inmediatamente y no se enganchan.
- La rueda virtual ahora usa doble clic para capturar y liberar el modo de sintonización circular. Un solo clic no cambia el estado de captura. Esto reemplaza la asimetría anterior donde solo Escape podía liberar la captura.
- Cuando un dispositivo FlexControl físico envía un comando de inicio/restablecimiento (por ejemplo, `F0304;`), el diálogo re-emite automáticamente el estado del LED para garantizar que el hardware coincida con el botón de modo de rueda activo de la aplicación. Esto resuelve condiciones de carrera donde el restablecimiento de encendido del dispositivo podría borrar el estado del LED después de que la aplicación ya lo hubiera configurado.
- Slice Audio Volume permite ajustar el volumen de audio del slice activo de forma independiente usando la rueda, sin afectar el volumen maestro ni otros slices.

## Relacionado

- [Configure acciones de un toque y doble toque para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Asigne acciones de botón pulsador y doble toque a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Use la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)

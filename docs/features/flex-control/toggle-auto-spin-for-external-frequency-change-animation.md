# Alternar animación de giro automático para cambios de frecuencia externos

Active o desactive la animación automática de giro virtual de la rueda que se reproduce cuando una fuente externa cambia la frecuencia del segmento, como al hacer clic en el panadapter o usar comandos CAT.

## Antes de comenzar

- Abra el cuadro de diálogo AetherControl mediante **Settings > AetherControl...**

## Pasos

1. Haga clic en **External Spin** para activar o desactivar la animación.

Cuando está activado, arrastrar sobre el panadapter o cambiar la frecuencia desde una fuente externa activa una animación de gesto de giro de la rueda en la rueda virtual. Cuando está desactivado, los cambios de frecuencia ocurren inmediatamente sin animación.

## Funciones de cada control

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Botón de alternancia | External Spin | Activa o desactiva la animación de giro en la rueda virtual cuando los cambios de frecuencia se originan fuera de la rueda. Clave de configuración: `FlexControlVirtualExternalSpin` |
| Botón de alternancia | Reverse | Invierte la dirección de sintonización de la rueda. |
| Botón de alternancia | Compact | Activa o desactiva el modo compacto: oculta los botones auxiliares y muestra solo la rueda y la frecuencia para una interfaz mínima. |
| Control deslizante | Wheel Tightness | Ajusta la resistencia al deslizamiento de la rueda virtual; 0 = apretado (parada rápida), 100 = suelto (deslizamiento prolongado). Principalmente para trackpads; no afecta al FlexControl físico. Clave de configuración: `FlexControlVirtualWheel` (JSON anidado, campo looseness). |
| Control deslizante | Mouse Sensitivity | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1,0x. Principalmente para trackpads; no afecta al FlexControl físico. Clave de configuración: `FlexControlVirtualWheel` (JSON anidado, campo sensitivity). |
| Cuadro combinado | Push (acción) | Asigna una acción al presionar la rueda (toque simple). Las opciones incluyen ciclo de modo, zoom por pasos, reinicio de zoom, banda arriba/abajo, RIT, XIT, volumen maestro, volumen de audio del segmento, volumen de auriculares, AGCT, APF y más. Clave de configuración: `FlexControlButtonAction_*`. |
| Cuadro combinado | Double-tap (acción) | Asigna una acción al doble toque en la rueda. |
| Botón pulsador | Aux buttons (1-5) | Cinco botones auxiliares configurables; etiquetados con puntos auxiliares para indicar la selección activa. |
| Cuadro combinado | Aux single-tap combo | Asigna una acción al toque simple en el botón auxiliar seleccionado. |
| Cuadro combinado | Aux double-tap combo | Asigna una acción al doble toque en el botón auxiliar seleccionado. |

## Indicadores

| Indicador | Significado |
|-----------|-------------|
| Wheel | Rueda FlexControl virtual que muestra la frecuencia y el modo del segmento activo. Gírela con el mouse o la pantalla táctil para sintonizar. |
| Physical | Muestra el estado de conexión del FlexControl físico y el nombre del puerto. Use los botones Detect/Cerrar para administrar el dispositivo físico. |

## Opciones de acción de la rueda

Las siguientes acciones se pueden asignar al toque de la rueda, doble toque o toques de botones auxiliares:

| ID de acción | Descripción |
|-------------|-------------|
| WheelRit | RIT (sintonización incremental de recepción) |
| WheelXit | XIT (sintonización incremental de transmisión) |
| WheelVolume | Volumen maestro |
| WheelSliceAudio | Volumen de audio del segmento |
| WheelHeadphoneVolume | Volumen de auriculares |
| WheelAgcT | AGCT (umbral de control automático de ganancia) |
| WheelApf | APF (filtro de pico de audio) |

## Relacionado

- [Use la rueda virtual para sintonizar el segmento activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configure el controlador hardware AetherControl/FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)

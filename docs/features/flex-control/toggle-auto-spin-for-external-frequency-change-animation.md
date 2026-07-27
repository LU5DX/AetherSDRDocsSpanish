# Alternar animación automática de giro para cambios de frecuencia externos

Active o desactive la animación automática de giro de la rueda virtual que se reproduce cuando una fuente externa cambia la frecuencia del segmento, como al hacer clic en el panadapter o usar comandos CAT.

## Antes de comenzar

- Abra el diálogo AetherControl mediante **Settings > AetherControl...**

## Pasos

1. Haga clic en **External Spin** para activar o desactivar la animación.

Cuando está activado, arrastrar sobre el panadapter o cambiar la frecuencia desde una fuente externa desencadena una animación de gesto de giro de rueda en la rueda virtual. Cuando está desactivado, los cambios de frecuencia ocurren inmediatamente sin animación.

## Qué hace cada control

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Botón de alternancia | External Spin | Activa o desactiva la animación de giro en la rueda virtual cuando los cambios de frecuencia provienen de fuera de la rueda. Clave de configuración: `FlexControlVirtualExternalSpin` |
| Botón de alternancia | Reverse | Invierte la dirección de sintonización de la rueda. |
| Botón de alternancia | Compact | Alterna el modo compacto: oculta los botones auxiliares, muestra solo la rueda y la frecuencia para una interfaz minimalista. |
| Control deslizante | Wheel Tightness | Ajusta la resistencia al deslizamiento de la rueda virtual; 0 = ajustado (parada rápida), 100 = suelto (deslizamiento prolongado). Principalmente para trackpads; no afecta al FlexControl físico. Clave de configuración: `FlexControlVirtualWheel` (JSON anidado, campo looseness). |
| Control deslizante | Mouse Sensitivity | Ajusta cuánto movimiento capturado del mouse/trackpad gira la rueda virtual. El punto medio (50) produce una escala de 1.0x. Principalmente para trackpads; no afecta al FlexControl físico. Clave de configuración: `FlexControlVirtualWheel` (JSON anidado, campo sensitivity). |
| Cuadro combinado | Push (action) | Asigna una acción al presionar la rueda (toque simple). Las opciones incluyen ciclo de modo, zoom por pasos, restablecer zoom, banda arriba/abajo, RIT, XIT, Volumen maestro, Volumen de audio del segmento, Volumen de auriculares, AGCT, APF y más. Clave de configuración: `FlexControlButtonAction_*`. |
| Cuadro combinado | Double-tap (action) | Asigna una acción al toque doble en la rueda. |
| Botón pulsador | Aux buttons (1-5) | Cinco botones auxiliares configurables; etiquetados con puntos auxiliares para indicar la selección activa. |
| Cuadro combinado | Aux single-tap combo | Asigna una acción al toque simple en el botón auxiliar seleccionado. |
| Cuadro combinado | Aux double-tap combo | Asigna una acción al toque doble en el botón auxiliar seleccionado. |

## Indicadores

| Indicador | Significado |
|-----------|-------------|
| Wheel | Rueda virtual FlexControl que muestra la frecuencia y el modo del segmento activo. Gírela con el mouse o el tacto para sintonizar. |
| Physical | Muestra el estado de conexión y el nombre del puerto del FlexControl físico. Use los botones Detect/Close para gestionar el dispositivo físico. |

## Opciones de acción de la rueda

Las siguientes acciones se pueden asignar al toque simple, toque doble o toques de botón auxiliar de la rueda:

| ID de acción | Descripción |
|--------------|-------------|
| WheelRit | RIT (Sintonización incremental de recepción) |
| WheelXit | XIT (Sintonización incremental de transmisión) |
| WheelVolume | Volumen maestro |
| WheelSliceAudio | Volumen de audio del segmento |
| WheelHeadphoneVolume | Volumen de auriculares |
| WheelAgcT | AGCT (Umbral de control automático de ganancia) |
| WheelApf | APF (Filtro de pico de audio) |

## Notas

- **Área de desplazamiento**: El diálogo completo de AetherControl incluye un área de desplazamiento para su contenido. Cuando la altura del diálogo excede la altura disponible de la pantalla, el área de contenido se desplaza verticalmente. El tamaño mínimo de ventana no compacto es 430×610 píxeles, pero el diálogo se reducirá más en pantallas pequeñas mientras mantiene acceso por desplazamiento a todos los controles.
- **Ajuste de tamaño según la pantalla**: El diálogo se adapta a la altura disponible de la pantalla (excluyendo la barra de tareas) para evitar abrirse más alto que el espacio de trabajo. En modo compacto, el diálogo se redimensiona para ajustarse al diseño minimalista de solo rueda. En modo no compacto, el ancho mínimo sigue el ancho del contenido para evitar recortes horizontales.

## Relacionados

- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)

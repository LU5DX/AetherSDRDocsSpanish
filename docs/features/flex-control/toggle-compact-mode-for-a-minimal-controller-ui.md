# Diálogo AetherControl / FlexControl

El diálogo AetherControl configura el controlador de hardware FlexControl y proporciona una rueda de sintonización virtual para el slice activo. Incluye sintonización con rueda, asignación de acciones a pulsaciones de botón, cinco botones auxiliares con acciones de pulsación simple y doble, modo compacto y reconexión automática para el dispositivo físico.

## Abrir el diálogo

Abra el diálogo AetherControl: `Settings > AetherControl…`

## Función de cada control

| Control | Predeterminado | Rango válido | Clave de configuración |
|---------|---------|-------------|-------------|
| Wheel (indicador) | — | — | — |
| Physical (indicador) | — | — | — |
| Compact (botón de alternancia) | Off | — | `FlexControlCompactMode` |
| External Spin (botón de alternancia) | Off | — | — |
| Reverse (botón de alternancia) | Off | — | — |
| Push (action) (cuadro combinado) | — | — | `FlexControlButtonAction_*` |
| Double-tap (action) (cuadro combinado) | — | — | — |
| Wheel Tightness (control deslizante) | 45 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo looseness) |
| Mouse Sensitivity (control deslizante) | 50 | 0–100 | `FlexControlVirtualWheel` (JSON anidado, campo sensitivity) |
| Aux buttons 1–5 (botón pulsador) | — | — | — |
| Aux single-tap combo (cuadro combinado) | — | — | — |
| Aux double-tap combo (cuadro combinado) | — | — | — |

## Rueda virtual

- **Wheel** — Gírela con el mouse o el tacto para sintonizar el slice activo. Muestra la lectura de frecuencia y modo.
- **Reverse** — Haga clic para invertir la dirección de sintonización de la rueda.
- **Wheel Tightness** — Ajusta la inercia de arrastre de la rueda virtual; 0 = firme (detención rápida), 100 = suelto (inercia prolongada). Afecta principalmente a los trackpads; no afecta al FlexControl físico. El control deslizante está etiquetado con los extremos **Tight** y **Loose**.
- **Mouse Sensitivity** — Ajusta cuánto movimiento capturado del mouse o trackpad hace girar la rueda virtual. El punto medio (50) produce una escala de 1.0x. El control deslizante está etiquetado con los extremos **Less** y **More**. Los deltas del puntero se limitan a 15° (π/12) por evento para evitar vibraciones, y el ancla se recentra cuando el puntero cruza la zona muerta central de la rueda sin calcular un delta.

## FlexControl físico

- **Physical** — Muestra el estado de conexión y el nombre del puerto del FlexControl físico. Use los botones **Detect** y **Close** para gestionar el dispositivo físico.
- El dispositivo físico se reconecta automáticamente si se desconecta y se vuelve a insertar, o si el puerto deja de estar disponible. Los intervalos de reintento comienzan en 2 segundos y aumentan progresivamente hasta un máximo de 30 segundos para fallos persistentes. El puerto se vuelve a detectar en cada reintento en caso de que una re-enumeración USB haya asignado un puerto COM diferente.

## Modo compacto

1. Haga clic en **Compact** para ocultar los botones auxiliares y sus cuadros combinados de acción, dejando solo la rueda y la lectura de frecuencia/modo.
2. Haga clic en **Compact** nuevamente para restaurar la vista completa.

## Giro externo

Haga clic en **External Spin** para habilitar los gestos de sintonización con rueda desde el panadapter. Arrastrar sobre el panadapter activa entonces la sintonización con rueda.

## Asignación de acciones

- **Push (action)** — Asigna una acción a la pulsación de la rueda (pulsación simple).
- **Double-tap (action)** — Asigna una acción a la doble pulsación de la rueda.
- **Aux buttons 1–5** — Cinco botones auxiliares configurables. Cada uno tiene un cuadro combinado de acción de **single-tap** y **double-tap**. El botón activo se indica mediante una etiqueta de punto auxiliar.

## Acciones disponibles para la rueda

Las siguientes acciones pueden asignarse a las pulsaciones de la rueda y a los toques de los botones auxiliares:

| ID de acción | Nombre mostrado |
|-----------|--------------|
| ModeCycle | Mode Cycle |
| StepZoom | Step Zoom |
| ZoomReset | Zoom Reset |
| BandUp | Band Up |
| BandDown | Band Down |
| WheelRit | RIT (Receive Incremental Tuning) |
| WheelXit | XIT (Transmit Incremental Tuning) |
| WheelVolume | Master Volume |
| WheelSliceAudio | Slice Audio Volume |
| WheelHeadphoneVolume | Headphone Volume |
| WheelAgcT | AGCT (Automatic Gain Control Threshold) |
| WheelApf | APF (Audio Peaking Filter) |

**Nota:** La acción **Slice Audio Volume** (WheelSliceAudio) ajusta el volumen de audio del slice activo de forma independiente de los volúmenes maestro y de auriculares.

## Comportamiento del tamaño de la ventana (v26.7.4)

El diálogo AetherControl usa un diseño desplazable. Cuando el modo compacto está desactivado, la ventana garantiza que el controlador completo esté disponible incluso en pantallas cortas o con escala DPI. El área de contenido se desplaza verticalmente cuando su altura intrínseca supera la altura disponible de la pantalla. El ancho mínimo de la ventana sigue el ancho mínimo del contenido para evitar recortes horizontales.

## Relacionado

- [AetherControl / FlexControl overview](overview.md)
- [Configure the AetherControl / FlexControl hardware controller](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
- [Use the virtual wheel to tune the active slice](use-the-virtual-wheel-to-tune-the-active-slice.md)

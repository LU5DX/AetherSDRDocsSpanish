# Establecer la velocidad de manipulación CW en PPM

Use el control deslizante Speed en el applet Phone/CW para establecer la velocidad a la que el radio manipula CW, medida en palabras por minuto. Esta configuración se envía directamente al FLEX-8600 y tiene efecto de inmediato.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW requiere una conexión de radio activa.
- El slice activo debe estar en un modo CW. El applet muestra los controles CW automáticamente solo cuando el slice se encuentra en modo CW; en modos de voz muestra el panel Phone en su lugar.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el panel del applet sea visible. Si el panel está oculto, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Verifique que se muestre el subpanel CW. Si en cambio se muestran los controles Phone, cambie el slice activo a un modo CW.
3. Ubique el control deslizante **Speed (CW)** en el panel CW.
4. Arrastre el control deslizante hasta la velocidad de manipulación deseada. El rango válido es de **5–100 WPM**.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Speed (CW) | Establece la velocidad de manipulación CW enviada al radio. | — | 5–100 WPM | — |

## Consejos

- El panel CW también contiene el control deslizante **Delay (CW)** (0–2000 ms, paso 10) para el tiempo de break-in, y el spinbox **Pitch < / >** (100–6000 Hz, paso 10) para el tono del sidetone. Ajuste estos valores junto con la velocidad para adaptarlos a sus preferencias de operación.

## Relacionados

- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Cambiar la frecuencia de tono/sidetone CW](change-cw-pitch-sidetone-frequency.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Escuchar un monitor de sidetone en TX](listen-to-a-tx-sidetone-monitor.md)

# Cambiar la frecuencia de tono CW / sidetone

La configuración de tono CW controla la frecuencia del tono utilizada tanto para el monitor de sidetone como para el desplazamiento de decodificación CW. Ajustarla permite coincidir con el tono de escucha preferido y alinear el marcador del filtro del panadapter con la frecuencia de operación.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al panel CW cuando el modo CW está activo.

## Pasos

1. Localice el applet Phone/CW en el Applet Panel (barra lateral derecha). Si no está visible, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que el subpanel CW esté visible. Aparece automáticamente cuando el slice activo está en modo CW.
3. Busque el spinbox **Pitch** cerca de la parte inferior del panel CW. El valor de tono actual se muestra en Hz entre dos botones de flecha.
4. Haga clic en **<** para disminuir el tono 10 Hz, o haga clic en **>** para aumentarlo 10 Hz.
5. Repita hasta que el valor mostrado coincida con el tono deseado.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Pitch < / >** | Ajusta en pasos la frecuencia de tono del sidetone CW y de la decodificación. Cada clic cambia el valor 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |
| **Sidetone** | Activa o desactiva el monitor de sidetone CW. El tono no tiene efecto audible a menos que Sidetone esté habilitado. | — | On / Off | — |
| **Sidetone volume** | Establece el nivel de volumen del monitor CW. | — | 0–100 | — |

## Consejos

- El valor de tono afecta tanto al tono audible del sidetone como al desplazamiento de frecuencia utilizado para la decodificación CW. Configúrelo para que coincida con su tono de escucha preferido antes de operar.
- El tono cambia únicamente en incrementos de 10 Hz. Para alcanzar un valor como 750 Hz desde 600 Hz, haga clic en **>** quince veces.

## Relacionados

- [Escuchar el monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)

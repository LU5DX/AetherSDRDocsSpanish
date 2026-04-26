# Cambiar el tono CW / frecuencia del sidetone

El ajuste de tono CW controla la frecuencia del tono utilizada tanto para el sidetone que escucha mientras transmite como para el desplazamiento de decodificación CW. Ajústelo para que coincida con el tono de escucha preferido o para ubicar correctamente el CW decodificado dentro de la banda de paso.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al panel CW cuando se selecciona un modo CW; el control de tono no es visible en el modo Phone.

## Pasos

1. Localice el botón de bandeja P/CW en la barra lateral derecha y confirme que el panel CW está visible. Si el applet está oculto, haga clic en el botón de bandeja P/CW para mostrarlo.
2. Ubique el spinbox **Pitch < / >** en la parte inferior del panel CW.
3. Haga clic en **<** para disminuir el tono 10 Hz, o haga clic en **>** para aumentarlo 10 Hz.
4. Repita hasta que el valor mostrado coincida con la frecuencia deseada.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Pitch < / >** | Incrementa o disminuye el tono del sidetone CW y de la decodificación. Cada clic mueve el valor 10 Hz. | 600 Hz | 100–6000 Hz (paso 10) | — |

## Consejos

- El valor de tono afecta tanto lo que escucha en el sidetone como el desplazamiento de frecuencia utilizado para la decodificación CW. Si el texto decodificado aparece desplazado, verifique que el tono coincida con el centro del filtro.
- El ajuste de tono se envía directamente al radio; no existe persistencia separada del lado del cliente.

## Relacionado

- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
- [Habilitar el manipulador iambic](enable-iambic-paddle-keying.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)

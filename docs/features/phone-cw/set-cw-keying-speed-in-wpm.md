# Configurar la velocidad de manipulación CW en PPM

Use el control deslizante Speed del applet Phone/CW para controlar la velocidad a la que AetherSDR manipula el FLEX-8600 cuando opera en modo CW. La velocidad se establece en palabras por minuto (WPM) y se envía directamente al radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de CW solo están disponibles cuando hay conexión activa.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia al panel CW automáticamente cuando el modo del slice es CW.

## Pasos

1. Ubique el botón de bandeja `P/CW` en la barra lateral derecha y confirme que el applet Phone/CW esté visible. Si no lo está, haga clic en el botón de bandeja `P/CW` para mostrarlo.
2. Confirme que el subpanel CW esté visible. Si el slice activo está en modo CW, el applet cambia al panel CW automáticamente. Si aún ve el panel Phone, configure primero el modo del slice en CW.
3. Localice el control deslizante **Speed (CW)**.
4. Arrastre el control deslizante **Speed (CW)** hacia la izquierda para reducir los WPM o hacia la derecha para aumentarlos.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Speed (CW) | Establece la velocidad de manipulación CW enviada al radio | — | 5–100 WPM | — |

## Consejos

- El panel CW también contiene el control deslizante **Delay (CW)** (0–2000 ms, paso 10) para el tiempo de break-in, y el interruptor **Breakin** para QSK completo. Ajustar la velocidad no afecta esos controles.
- El applet vuelve al panel Phone automáticamente cuando el slice activo sale del modo CW, pero el radio conserva su configuración de velocidad.

## Temas relacionados

- [Configurar el retardo de break-in en CW](set-cw-break-in-delay.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone en transmisión](listen-to-a-tx-sidetone-monitor.md)

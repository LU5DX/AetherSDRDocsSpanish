# Ajustar la velocidad de manipulación CW en WPM

Use esta página para ajustar la velocidad con la que AetherSDR manipula la radio en modo CW. La velocidad se configura en palabras por minuto (WPM) y se envía directamente al FLEX-8600.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet P/CW requiere una conexión de radio activa.
- El slice activo debe estar en modo CW. El applet Phone/CW cambia automáticamente al subpanel de CW cuando el slice está en modo CW; el control deslizante Speed solo es visible en ese subpanel.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW, si aún no está visible.
2. Confirme que el subpanel de CW se está mostrando. Si el slice activo está en modo CW, el applet muestra los controles de CW, incluyendo **Speed (CW)**, **Delay (CW)** y **ALC**. Si ve los controles de micrófono en su lugar, cambie primero el slice activo a un modo CW.
3. Arrastre el control deslizante **Speed (CW)** hasta el valor de WPM deseado. El rango válido es de 5–100 WPM.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| Speed (CW) | Deslizador | — | 5–100 WPM | — |

El control deslizante **Speed (CW)** establece la velocidad de manipulación CW en la radio. Los cambios surten efecto de inmediato y se aplican a las transmisiones con paleta, manipulador recto y CWX.

## Consejos

- El control deslizante Speed no tiene una clave de configuración persistida. El valor lo conserva el firmware de la radio; AetherSDR lo lee de la radio al volver a conectarse.
- Si usa el tono lateral local (**Local STn**), este sigue automáticamente la velocidad de manipulación de la radio — no se necesita ningún ajuste adicional.

## Solución de problemas

- **El subpanel de CW no es visible** — El applet muestra los controles Phone cuando el slice activo no está en modo CW. Cambie el modo del slice a CW y el applet mostrará automáticamente los controles de CW, incluyendo **Speed (CW)**.
- **El control deslizante aparece pero no responde** — Verifique que la conexión de radio esté activa. El applet P/CW requiere una conexión de radio en vivo para enviar los cambios de velocidad.

## Relacionados

- [Ajustar el retardo de break-in CW](set-cw-break-in-delay.md)
- [Activar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Activar el tono lateral CW local de baja latencia (Local STn) para trabajar con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Escuchar un monitor de tono lateral en TX](listen-to-a-tx-sidetone-monitor.md)

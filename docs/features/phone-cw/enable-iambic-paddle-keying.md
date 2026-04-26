# Activar el manipulador de paleta iámbica

Esta página explica cómo activar el manipulador de paleta iámbica para el slice CW activo. Use esta función cuando opere con una paleta squeeze y desee que el manipulador iámbico integrado del radio se encargue de generar los dits y dahs.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW requiere una conexión activa con el radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW muestra los controles de CW únicamente cuando el slice activo está en modo CW; de lo contrario, muestra los controles de Phone.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet Phone/CW esté visible. Si no lo está, haga clic en el botón **P/CW** para mostrarlo.
2. Confirme que el applet esté mostrando el panel de CW. Si en su lugar se muestran los controles de Phone (ganancia de micrófono, PROC, MON), primero cambie el slice activo a un modo CW.
3. Haga clic en **Iambic** para activar o desactivar el manipulador de paleta iámbica. El botón se activa y el radio habilita el manipulado iámbico.

Para desactivar el manipulado iámbico, haga clic en **Iambic** nuevamente.

## Qué hace cada control

| Control | Tipo | Valor por defecto | Rango válido | Clave persistida |
|---|---|---|---|---|
| Iambic | Botón de alternancia | — | On / Off | — |

**Iambic** — Activa o desactiva el manipulador de paleta iámbica en el radio. Cuando está activo, el radio interpreta la entrada de la paleta squeeze como manipulado iámbico. Cuando está desactivado, el radio utiliza el comportamiento de llave recta o bug según el cableado de su paleta.

## Temas relacionados

- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Cambiar el tono CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)

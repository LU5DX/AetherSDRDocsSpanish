# Configurar el retardo de break-in de CW

El retardo de break-in de CW controla cuánto tiempo espera el equipo después del último elemento transmitido antes de volver a la recepción. Ajustar este valor evita que el receptor recupere la escucha de forma prematura durante intercambios rápidos.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo.
- El slice activo debe estar en un modo CW. El applet Phone/CW muestra los controles de CW automáticamente solo cuando se selecciona un modo CW.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón **P/CW** de la barra lateral derecha para mostrarlo.
2. Localice el control deslizante **Delay** en el subpanel de CW.
3. Arrastre el control deslizante **Delay** hasta el valor deseado. El rango válido es de 0 a 2000 ms en pasos de 10.
4. Para habilitar el break-in completo (QSK) sin retardo, haga clic en **Breakin** para activarlo.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de persistencia |
|---|---|---|---|---|
| **Delay** | Control deslizante | — | 0–2000 ms (paso 10) | — |
| **Breakin** | Botón de alternancia | — | On / Off | — |

- **Delay** — Establece el tiempo que el equipo espera después del último elemento transmitido antes de volver a la recepción.
- **Breakin** — Activa o desactiva el break-in completo (QSK). Cuando está activo, el equipo vuelve a la recepción inmediatamente entre elementos transmitidos, independientemente del valor de **Delay**.

## Consejos

- Un valor de **Delay** de 0 ms con **Breakin** activo proporciona un comportamiento QSK verdadero.
- Aumente el valor de **Delay** si el receptor recupera la escucha demasiado rápido y esto interrumpe su ritmo de manipulación durante pile-ups.

## Relacionado

- [Descripción general de Phone/CW](overview.md)
- [Configurar la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Habilitar la manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono de CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)

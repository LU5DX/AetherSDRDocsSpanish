# Seleccionar la fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Esta página muestra cómo seleccionar la fuente de entrada de micrófono para su FLEX-8600 en AetherSDR. La fuente correcta debe coincidir con el conector físico que está utilizando antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado a su FLEX-8600.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM o similar). El panel Phone se oculta cuando el slice activo está en modo CW.
- Abra el applet Phone/CW: haga clic en el botón de bandeja **P/CW** en la barra lateral derecha si el applet no está visible.

## Pasos

1. Localice el menú desplegable **Mic source** en el applet Phone/CW. Es un cuadro combinado estrecho (aproximadamente 55 px de ancho) en la misma fila que el control deslizante **Mic gain** y el botón **+ACC**.
2. Haga clic en el menú desplegable **Mic source**.
3. Seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`. La selección se envía al radio de inmediato.
4. Si seleccionó `PC`, ajuste el control deslizante **Mic gain** al nivel deseado (0–100; valor predeterminado 50). La fuente `PC` conserva su valor de ganancia localmente en `PcMicGain` porque el radio siempre reporta el nivel de micrófono como 0 para esta fuente.
5. Observe el indicador **Level** (−40 a +10 dBFS). Hable o alimente audio y confirme que la aguja se mueve. Procure mantener los picos por debajo de 0 dBFS (el indicador se pone rojo por encima de 0).

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Clave de configuración | Notas |
|---|---|---|---|---|---|
| Mic source | Cuadro combinado | — | MIC, BAL, LINE, ACC, PC | — | Se envía al radio al cambiar. |
| Mic gain | Control deslizante | 50 | 0–100 | `PcMicGain` (solo fuente PC) | Para fuentes que no son PC, la ganancia se almacena en el radio. Para PC, el valor se conserva en el cliente. |
| Level | Medidor | — | −40 a +10 dBFS (rojo por encima de 0) | — | Muestra el nivel de pico de entrada del micrófono. Indica −150 cuando no se está transmitiendo y la monitorización del micrófono está desactivada. |

## Consejos

- La fuente `PC` enruta el audio desde la entrada de sonido de su computadora. El radio no reporta el nivel de micrófono para esta fuente, por lo que el valor `PcMicGain` se almacena en AetherSDR y se aplica localmente.
- Si desea mezclar un micrófono de accesorio con la fuente seleccionada, active **+ACC** en la misma fila después de elegir su fuente principal.

## Solución de problemas

- **El indicador Level no muestra movimiento después de seleccionar una fuente** — Confirme que está transmitiendo o que la monitorización del micrófono está activa. El indicador se suprime a −150 dBFS cuando ninguna de las dos condiciones es verdadera.
- **Fuente PC seleccionada pero el control deslizante Mic gain no tiene efecto en el nivel reportado por el radio** — Esto es esperado. El radio siempre reporta mic_level=0 para la fuente PC. AetherSDR almacena la ganancia en `PcMicGain` y la aplica en el cliente.
- **El panel Phone no está visible** — El applet cambia a los controles CW cuando el slice activo está en modo CW. Cambie el slice activo a un modo de voz para ver los controles de fuente de micrófono.

## Relacionados

- [Ajustar la ganancia del micrófono y activar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)

# Reducir la latencia DAX RX en Linux (ruta nativa PipeWire, ~200 ms)

AetherSDR v0.9.7 en Linux enruta el audio DAX RX a través de una fuente `pw_stream` nativa de PipeWire, reduciendo la latencia de recepción de ~400 ms a ~200 ms. Esta página explica qué cambió y cómo confirmar que DAX está funcionando con la ruta de menor latencia.

## Antes de comenzar

- AetherSDR v0.9.7 o posterior instalado en Linux con PipeWire como servidor de audio del sistema.
- Una radio FLEX-8600 conectada (DAX requiere una conexión de radio activa).
- Al menos un slice (receptor virtual) asignado a un canal DAX en la radio.

## Pasos

1. Haga clic en el botón DAX de la bandeja en la barra lateral derecha para abrir el applet DAX Audio.
2. Haga clic en Enable para iniciar el puente de audio DAX. El botón se vuelve verde cuando está activo.
3. Confirme que la configuración `AutoStartDAX` esté guardada: el botón Enable permanece marcado después de volver a abrir el applet.
4. En su software de modos digitales (WSJT-X, fldigi u otro similar), seleccione la fuente PipeWire correspondiente al canal DAX que asignó. El audio llegará ahora con aproximadamente 200 ms de latencia en lugar de ~400 ms.

No se requiere configuración adicional. La ruta PipeWire se utiliza automáticamente en Linux en v0.9.7 y versiones posteriores; no existe un interruptor para cambiar entre la ruta antigua de PulseAudio y la nueva.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Descripción |
|---|---|---|---|---|
| Enable | Off | On / Off | `AutoStartDAX` | Interruptor principal. Inicia todos los flujos DAX RX y TX. Debe estar activo para que el audio fluya. |
| DAX 1 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain1` | Medidor de nivel y control de ganancia combinados para el canal DAX 1. Arrastre para ajustar la ganancia RX. |
| DAX 2 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain2` | Medidor de nivel y control de ganancia combinados para el canal DAX 2. |
| DAX 3 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain3` | Medidor de nivel y control de ganancia combinados para el canal DAX 3. |
| DAX 4 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain4` | Medidor de nivel y control de ganancia combinados para el canal DAX 4. |
| TX gain+meter | 0.5 | 0.0 – 1.0 | `DaxTxGain` | Medidor de nivel y control de ganancia combinados para el flujo DAX TX. |
| Estado de asignación de slice | — | — o Slice A–H | *(ninguna)* | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX. |

## Consejos

- Si las barras del medidor en DAX 1–4 no se mueven después de hacer clic en Enable, verifique que el indicador de estado de asignación de slice muestre una letra de slice en lugar de —. Un — significa que ningún slice está enrutado actualmente a ese canal; asigne el slice al canal DAX desde los controles de slice de la radio.
- Para que DAX se inicie automáticamente en cada arranque, marque `Settings > Autostart DAX with AetherSDR`. Esto establece `AutoStartDAX` en True sin necesidad de hacer clic en Enable manualmente en cada sesión.
- El medidor de nivel utiliza una dinámica de ataque rápido (α = 0.4) y decaimiento lento (α = 0.08). Una breve ausencia de señal no blanqueará el medidor de inmediato.

## Solución de problemas

- **El botón Enable aparece atenuado o no responde** — DAX requiere una conexión de radio activa. Conéctese primero al FLEX-8600 mediante `Settings > Connect to Radio...`, luego haga clic en Enable.
- **La latencia sigue siendo ~400 ms después de actualizar a v0.9.7** — Verifique que PipeWire sea el servidor de audio activo en su sistema. Si su sistema aún utiliza PulseAudio sin PipeWire, la ruta nativa de PipeWire no está disponible y la latencia permanecerá en el valor más alto.
- **Sin audio desde la fuente PipeWire en WSJT-X o fldigi** — Confirme que Enable esté marcado (verde) en el applet DAX y que el indicador de asignación de slice para el canal correspondiente muestre una letra de slice, no —.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Ver qué slice utiliza cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

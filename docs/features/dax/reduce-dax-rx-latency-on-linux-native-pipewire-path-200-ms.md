# Reducir la latencia de RX de DAX en Linux (ruta nativa de PipeWire, ~200 ms)

AetherSDR v0.9.7 en Linux enruta el audio de RX de DAX a través de una fuente nativa `pw_stream` de PipeWire, reduciendo la latencia de recepción de ~400 ms a ~200 ms. Esta página explica qué cambió y cómo confirmar que DAX se está ejecutando con la ruta de menor latencia.

## Antes de comenzar

- AetherSDR v0.9.7 o posterior instalado en Linux con PipeWire ejecutándose como servidor de audio del sistema.
- Una radio FLEX-8600 conectada (DAX requiere una conexión de radio activa).
- Al menos un slice asignado a un canal DAX en la radio.

## Pasos

1. Haga clic en el botón de la bandeja de DAX en la barra lateral derecha para abrir el applet de audio DAX.
2. Haga clic en Enable para iniciar el puente de audio DAX. El botón se vuelve verde cuando está activo.
3. Confirme que la configuración `AutoStartDAX` esté guardada: el botón Enable permanece marcado después de volver a abrir el applet.
4. En su software de modos digitales (WSJT-X, fldigi o similar), seleccione la fuente de PipeWire correspondiente al canal DAX que asignó. El audio ahora llega con aproximadamente 200 ms de latencia en lugar de ~400 ms.

No se requiere configuración adicional. La ruta de PipeWire se utiliza automáticamente en Linux en v0.9.7 y versiones posteriores; no hay un interruptor para cambiar entre la ruta antigua de PulseAudio y la nueva.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Descripción |
|---|---|---|---|---|
| Enable | Off | On / Off | `AutoStartDAX` | Interruptor principal. Inicia todos los flujos de RX y TX de DAX. Debe estar activado para que fluya el audio. |
| DAX 1 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain1` | Medidor de nivel combinado y deslizador de ganancia para el canal DAX 1. Arrastre para ajustar la ganancia de RX. |
| DAX 2 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain2` | Medidor de nivel combinado y deslizador de ganancia para el canal DAX 2. |
| DAX 3 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain3` | Medidor de nivel combinado y deslizador de ganancia para el canal DAX 3. |
| DAX 4 gain+meter | 0.5 | 0.0 – 1.0 | `DaxRxGain4` | Medidor de nivel combinado y deslizador de ganancia para el canal DAX 4. |
| TX gain+meter | 0.5 | 0.0 – 1.0 | `DaxTxGain` | Medidor de nivel combinado y deslizador de ganancia para el flujo TX de DAX. |
| Slice-assignment status | — | — o Slice A–H | *(ninguna)* | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX. |

## Consejos

- Si las barras del medidor en DAX 1–4 no se mueven después de hacer clic en Enable, verifique que el indicador de estado de asignación de slice muestre una letra de slice en lugar de —. Un — significa que ningún slice está enrutado actualmente a ese canal; asigne el slice al canal DAX desde los controles de slice de la radio.
- Para que DAX se inicie automáticamente en cada inicio, marque `Settings > Autostart DAX with AetherSDR`. Esto establece `AutoStartDAX` en True sin necesidad de hacer clic en Enable manualmente cada sesión.
- El medidor de nivel utiliza ataque rápido (α = 0.4) y caída lenta (α = 0.08). Una breve ausencia de señal no dejará el medidor en blanco de inmediato.

## Solución de problemas

- **El botón Enable está atenuado o no responde** — DAX requiere una conexión de radio activa. Conéctese primero a la FLEX-8600 a través de `Settings > Connect to Radio...`, luego haga clic en Enable.
- **La latencia sigue siendo de ~400 ms después de actualizar a v0.9.7** — Verifique que PipeWire sea el servidor de audio activo en su sistema. Si su sistema aún usa PulseAudio sin PipeWire, la ruta nativa de PipeWire no está disponible y la latencia permanecerá en el valor más alto.
- **Sin audio desde la fuente de PipeWire en WSJT-X o fldigi** — Confirme que Enable esté marcado (verde) en el applet DAX y que el indicador de asignación de slice para el canal relevante muestre una letra de slice, no —.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Establecer ganancia de RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

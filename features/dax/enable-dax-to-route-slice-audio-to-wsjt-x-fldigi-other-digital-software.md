# Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / Otro software digital

DAX (Digital Audio eXchange) actúa como puente de audio entre el FLEX-8600 y otro software que se ejecute en su computadora. Al habilitarlo, se crean canales de audio virtuales que programas como WSJT-X, FLDigi y aplicaciones similares de modos digitales pueden usar como dispositivo de sonido.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. DAX requiere una conexión de radio activa.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.
- En su software de modo digital, tenga abierta la configuración de dispositivos de audio para poder seleccionar el canal DAX una vez que esté activo.

## Pasos

1. Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para abrir el applet DAX Audio.
2. Haga clic en **Enable** para iniciar el puente de audio DAX. El botón se vuelve verde cuando está activo, y la configuración se guarda como `AutoStartDAX`.
3. En su radio, asigne un slice (receptor virtual) a un canal DAX. El indicador de asignación de slice junto a cada fila de canal se actualiza para mostrar el slice asignado (por ejemplo, `Slice A`). Un `—` significa que no hay ningún slice asignado a ese canal.
4. En su software de modo digital, seleccione el canal DAX RX que corresponda al canal asignado como dispositivo de entrada de audio (por ejemplo, DAX IQ 1 o DAX Audio 1, según su sistema operativo y controlador).
5. Si su software de modo digital transmite audio, seleccione el canal DAX TX correspondiente como dispositivo de salida de audio.
6. Arrastre el control deslizante de ganancia en la fila del canal para ajustar el nivel RX de ese canal. El valor predeterminado es `0.5` (punto medio). El medidor detrás del control deslizante muestra el nivel de señal en tiempo real.
7. Si transmite mediante DAX, arrastre el control deslizante de ganancia **TX** para establecer el nivel de audio de transmisión. El valor predeterminado también es `0.5`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Configuración guardada | Comportamiento |
|---|---|---|---|---|
| Enable | Desactivado | Activado / Desactivado | `AutoStartDAX` | Interruptor principal. Inicia el puente de audio DAX para todos los flujos RX y TX. |
| DAX 1 ganancia+medidor | 0.5 | 0.0 – 1.0 | `DaxRxGain1` | Arrastre para ajustar la ganancia RX en el canal DAX 1. El medidor muestra el nivel en tiempo real después del fader. |
| DAX 2 ganancia+medidor | 0.5 | 0.0 – 1.0 | `DaxRxGain2` | Arrastre para ajustar la ganancia RX en el canal DAX 2. |
| DAX 3 ganancia+medidor | 0.5 | 0.0 – 1.0 | `DaxRxGain3` | Arrastre para ajustar la ganancia RX en el canal DAX 3. |
| DAX 4 ganancia+medidor | 0.5 | 0.0 – 1.0 | `DaxRxGain4` | Arrastre para ajustar la ganancia RX en el canal DAX 4. |
| TX ganancia+medidor | 0.5 | 0.0 – 1.0 | `DaxTxGain` | Arrastre para ajustar la ganancia del flujo TX. El medidor muestra el nivel de transmisión en tiempo real después del fader. |
| Indicador de asignación de slice | — | `—` o `Slice A`–`Slice H` | _(ninguna)_ | Muestra qué slice está enrutado a cada canal DAX. Solo lectura. |

## Consejos

- Para que DAX se inicie automáticamente cada vez que se lance AetherSDR, habilite `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** manualmente en cada sesión.
- El indicador de estado TX muestra qué slice tiene actualmente los privilegios de transmisión. Solo ese slice controla el flujo DAX TX.
- Si el medidor de un canal está activo pero su software digital no recibe audio, confirme que el indicador de asignación de slice muestre un nombre de slice en lugar de `—`.

## Solución de problemas

- **El botón Enable está presente pero no hace nada visible** — DAX requiere una conexión de radio activa. Confirme que AetherSDR esté conectado al radio antes de hacer clic en **Enable**.
- **El indicador de asignación de slice muestra `—` en todos los canales** — Ningún slice ha sido asignado a un canal DAX en el radio. Use los controles de slice del radio para asignar un número de canal DAX al slice que desea decodificar.
- **El software digital no recibe audio a pesar de que hay un slice asignado** — Verifique que el dispositivo de entrada de audio de su software coincida con el número de canal DAX correcto que se muestra en el applet. Confirme también que el control deslizante de ganancia RX esté por encima de `0.0`.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Inicio automático de DAX al lanzar AetherSDR](autostart-dax-on-launch.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar cuál es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

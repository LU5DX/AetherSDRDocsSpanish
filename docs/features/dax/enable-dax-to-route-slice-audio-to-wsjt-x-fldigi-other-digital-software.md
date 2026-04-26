# Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital

DAX (Digital Audio eXchange) crea puentes de audio entre AetherSDR y otros programas que se ejecutan en su computadora. Al habilitarlo, programas como WSJT-X y fldigi pueden recibir audio de un slice (canal de recepción) y enviar audio de transmisión a través del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. DAX requiere una conexión de radio activa.
- Su software digital (WSJT-X, fldigi, etc.) debe estar configurado para usar los dispositivos de audio DAX. Consulte [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md) para esa parte de la configuración.
- Identifique qué slice desea enrutar. Cada canal DAX transporta el audio de un slice.

## Pasos

1. Haga clic en el botón `DAX` del panel lateral derecho para abrir el applet de audio DAX. Si el panel de applets no está visible, actívelo con `View > Applet Panel`.
2. Haga clic en `Enable` para iniciar el puente de audio DAX. El botón se pone verde cuando está activo. Este estado se guarda como `AutoStartDAX`.
3. Revise el indicador de asignación de slice junto a cada canal DAX (etiquetados `DAX 1:` a `DAX 4:`). Un valor de `—` significa que ningún slice está enrutado a ese canal. Un valor como `Slice A` indica que el audio de ese slice fluye por el canal.
4. En los controles de slice de su radio, asigne el slice deseado al canal DAX que su software digital está escuchando. El indicador se actualiza automáticamente cuando la asignación surte efecto.
5. En su software digital, seleccione el dispositivo de audio DAX RX correspondiente como entrada y el dispositivo de audio DAX TX como salida.
6. Arrastre el control deslizante de ganancia+medidor del canal DAX correspondiente (por ejemplo, `DAX 1:`) para ajustar el nivel de audio RX que llega a su software. El valor predeterminado es `0.5`. El rango válido es `0.0`–`1.0`, guardado como `DaxRxGain1` a `DaxRxGain4`.
7. Si su software digital transmite audio, arrastre el control deslizante de ganancia+medidor `TX:` para ajustar el nivel de transmisión. El valor predeterminado es `0.5`. El rango válido es `0.0`–`1.0`, guardado como `DaxTxGain`.

## Qué hace cada control

| Control | Función | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `Enable` | Inicia o detiene el puente de audio DAX. Interruptor principal para todos los flujos RX y TX. | Desactivado | Activado / Desactivado | `AutoStartDAX` |
| Ganancia+medidor `DAX 1:` | Establece la ganancia de audio RX para el canal DAX 1 y muestra el nivel en tiempo real. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| Ganancia+medidor `DAX 2:` | Establece la ganancia de audio RX para el canal DAX 2 y muestra el nivel en tiempo real. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| Ganancia+medidor `DAX 3:` | Establece la ganancia de audio RX para el canal DAX 3 y muestra el nivel en tiempo real. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| Ganancia+medidor `DAX 4:` | Establece la ganancia de audio RX para el canal DAX 4 y muestra el nivel en tiempo real. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| Ganancia+medidor `TX:` | Establece la ganancia de audio TX para el flujo de transmisión DAX y muestra el nivel en tiempo real. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice (por canal) | Muestra qué slice está enrutado actualmente a cada canal DAX (`—` o `Slice A`–`Slice H`). Solo lectura. | `—` | — | — |

## Consejos

- Para que DAX se inicie automáticamente cada vez que AetherSDR arranque, marque `Settings > Autostart DAX with AetherSDR`. Esto establece `AutoStartDAX` sin necesidad de abrir el applet en cada sesión.
- El medidor de nivel detrás de cada control deslizante muestra el nivel posterior al fader: la barra refleja el nivel de salida real después de aplicar la ganancia, de modo que lo que ve es lo que recibe su software digital.
- El indicador `TX:` muestra qué slice tiene en ese momento los privilegios de transmisión. Si muestra `—`, ningún slice está definido como slice TX y el audio de transmisión no fluirá.

## Solución de problemas

- **El botón `Enable` no responde o aparece desactivado** — DAX requiere una conexión de radio activa. Confirme que AetherSDR esté conectado al FLEX-8600 antes de habilitar DAX.
- **El indicador de asignación de slice muestra `—` después de habilitar DAX** — El slice no ha sido asignado a un canal DAX en la configuración de slices del radio. Asigne el slice a un canal DAX desde los controles de slice.
- **El software digital no recibe audio a pesar de que DAX está habilitado** — Confirme que el dispositivo de entrada de audio del software digital esté configurado en el canal DAX RX correcto, que coincida con el canal mostrado en el applet. Verifique también que el control deslizante de ganancia RX esté por encima de `0.0`.
- **El audio TX no se transmite** — Compruebe que el indicador `TX:` muestre el slice esperado y no `—`. Si muestra `—`, ningún slice tiene privilegios de TX; consulte [Identificar cuál es el slice TX](identify-which-slice-is-the-tx-slice.md).

## Temas relacionados

- [Descripción general del audio DAX](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Establecer la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer la ganancia DAX TX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar cuál es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

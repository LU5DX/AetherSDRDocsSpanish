# Descripción general de audio DAX

El applet DAX (Digital Audio eXchange) actúa como puente de audio entre su FLEX-8600 y otros programas de su computadora. Úselo para enrutar el audio de recepción de un slice (canal de recepción) hacia programas de modos digitales como WSJT-X o fldigi, y para enviar el audio de esos programas de vuelta a la radio para transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- El applet DAX está oculto de forma predeterminada. Haga clic en el botón **DAX** de la barra lateral derecha para mostrarlo.

## Cómo funciona

DAX proporciona cuatro canales de audio RX independientes y un canal de audio TX. Cada canal RX puede asignarse a un slice de la radio; el applet muestra qué slice (si alguno) está enrutado actualmente a cada canal. El canal TX transporta audio desde su computadora hacia la radio y es controlado por el slice que tenga los privilegios de TX en ese momento.

Cada canal cuenta con un medidor y un control deslizante de ganancia combinados. El medidor muestra el nivel post-fader — el valor RMS suavizado multiplicado por la ganancia actual — de modo que la barra refleja el nivel de salida real. Arrastre el control deslizante para establecer la ganancia de ese canal; el valor se guarda de inmediato.

El botón principal **Enable** inicia o detiene todo el puente de audio DAX. Al activarlo o desactivarlo también se actualiza el ajuste `AutoStartDAX`, que controla si DAX se inicia automáticamente cuando se lanza AetherSDR. También puede configurar el inicio automático desde `Settings > Autostart DAX with AetherSDR`.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Enable** | Inicia o detiene el puente de audio DAX. Interruptor principal para todos los flujos RX y TX. | Off | On / Off | `AutoStartDAX` |
| Ganancia+medidor **DAX 1** | Establece la ganancia RX del canal DAX 1 y muestra su nivel post-fader. | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Ganancia+medidor **DAX 2** | Establece la ganancia RX del canal DAX 2 y muestra su nivel post-fader. | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Ganancia+medidor **DAX 3** | Establece la ganancia RX del canal DAX 3 y muestra su nivel post-fader. | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Ganancia+medidor **DAX 4** | Establece la ganancia RX del canal DAX 4 y muestra su nivel post-fader. | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Ganancia+medidor **TX** | Establece la ganancia del flujo DAX TX y muestra su nivel post-fader. | 0.5 | 0.0 – 1.0 | `DaxTxGain` |
| Indicador de asignación de slice (por canal RX) | Muestra qué slice está enrutado a este canal DAX. Muestra `—` cuando no hay asignación, o `Slice A` a `Slice H` cuando hay una. | — | `—` o `Slice A–H` | — |
| Indicador de slice TX | Muestra qué slice tiene actualmente los privilegios de TX y controla el flujo DAX TX. Muestra `—` cuando no hay slice TX activo. | — | `—` o `Slice A–H` | — |

## Consejos

- Los cambios de ganancia se guardan de inmediato en los ajustes persistentes. No es necesario hacer clic en un botón separado de guardar o aplicar.
- El medidor utiliza suavizado asimétrico: la barra de nivel sube rápidamente ante una nueva señal (ataque rápido) y baja lentamente cuando la señal cae (decaimiento lento), de forma coherente con las demás superficies de medición en AetherSDR.

## Temas relacionados

- [Habilitar DAX para enrutar audio de slice hacia WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Inicio automático de DAX al lanzar la aplicación](autostart-dax-on-launch.md)
- [Establecer la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer la ganancia DAX TX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar cuál es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

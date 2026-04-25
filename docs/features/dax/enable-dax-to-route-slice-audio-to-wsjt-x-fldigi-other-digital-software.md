# Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software de modos digitales

DAX (Digital Audio eXchange) crea flujos de audio entre AetherSDR y otras aplicaciones en su computadora. Habilítelo para que software como WSJT-X o FLDigi pueda recibir audio de un slice de radio y transmitir audio de vuelta a través de él.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. DAX requiere una conexión de radio activa.
- Debe existir al menos un slice y estar asignado a un canal DAX en la configuración de la radio antes de que fluya el audio.
- Su software de modo digital debe estar configurado para usar el dispositivo de audio virtual DAX. Consulte [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md) para esa parte de la configuración.

## Pasos

1. Haga clic en el botón `DAX` de la bandeja en la barra lateral derecha para abrir el applet de audio DAX. El applet está oculto por defecto.
2. Haga clic en `Enable`. El botón se vuelve verde cuando DAX está activo. AetherSDR guarda este estado como `AutoStartDAX`.
3. Verifique el indicador de asignación de slice junto a cada canal DAX (por ejemplo, `Slice A`). Un guión (`—`) significa que ningún slice está enrutado a ese canal. Si es necesario, asigne un slice a un canal DAX desde la configuración de slices de la radio.
4. Arrastre el control deslizante de ganancia+medidor del canal DAX que usará su software digital para establecer el nivel de audio RX. El valor predeterminado es `0.5` (escala media). Ajuste hasta que el medidor de nivel muestre señal sin saturación.
5. Si su software digital va a transmitir a través de DAX, arrastre el control deslizante de ganancia+medidor `TX` para establecer el nivel de audio de transmisión. El valor predeterminado también es `0.5`.
6. En su software de modo digital (WSJT-X, FLDigi, etc.), seleccione el dispositivo de audio virtual DAX como la tarjeta de sonido de entrada (RX) y de salida (TX).

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| `Enable` | Inicia el puente de audio DAX. Todos los flujos RX y TX dependen de que esté activo. | Desactivado | Activado / Desactivado | `AutoStartDAX` |
| Ganancia+medidor `DAX 1` | Establece la ganancia de audio RX para el canal DAX 1. Arrastre para ajustar; el medidor muestra el nivel en tiempo real. | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Ganancia+medidor `DAX 2` | Establece la ganancia de audio RX para el canal DAX 2. | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Ganancia+medidor `DAX 3` | Establece la ganancia de audio RX para el canal DAX 3. | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Ganancia+medidor `DAX 4` | Establece la ganancia de audio RX para el canal DAX 4. | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Ganancia+medidor `TX` | Establece el nivel de audio de transmisión para el flujo TX de DAX. | 0.5 | 0.0 – 1.0 | `DaxTxGain` |
| Indicador de asignación de slice (por canal) | Muestra qué slice está enrutado a este canal DAX (`—` si ninguno, o `Slice A` hasta `Slice H`). | `—` | — | — |

## Consejos

- Para que DAX se inicie automáticamente cada vez que AetherSDR se lanza, habilite `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en `Enable` en cada sesión.
- El medidor de nivel en cada widget de ganancia+medidor muestra el nivel post-fader; refleja el nivel de salida real después de aplicar el control deslizante de ganancia. Úselo para determinar si su software digital está recibiendo una señal adecuada.
- El indicador `TX` muestra qué slice tiene actualmente los privilegios de TX. Si muestra `—`, ningún slice está designado como slice TX y el audio TX de DAX no será enrutado.

## Solución de problemas

- **El botón `Enable` está presente pero el applet DAX no muestra actividad en el medidor** — Confirme que hay un slice asignado al canal DAX que está utilizando. El indicador de asignación de slice debe mostrar una letra de slice, no `—`.
- **El software digital no recibe audio** — Verifique que el dispositivo de audio virtual DAX esté seleccionado como dispositivo de entrada en su software digital. DAX debe estar habilitado en AetherSDR antes de que el dispositivo virtual se active.
- **El audio TX no está llegando a la radio** — Compruebe que el indicador `TX` muestre una letra de slice. Si muestra `—`, no hay ningún slice TX asignado. Confirme también que su software digital esté usando el dispositivo de audio virtual DAX como salida.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Inicio automático de DAX al lanzar](autostart-dax-on-launch.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

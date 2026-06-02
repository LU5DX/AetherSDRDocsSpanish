# Inicio automático de DAX al lanzar

Active la opción `AutoStartDAX` para que el puente de audio DAX se inicie automáticamente cada vez que AetherSDR se abra, sin necesidad de hacer clic manualmente en **Enable** cada sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión activa con la radio.
- El applet DAX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet DAX haciendo clic en el botón **DAX** de la bandeja en la barra lateral derecha si aún no está visible.
2. Haga clic en **Settings > Autostart DAX with AetherSDR** para marcar el elemento. Esto fija `AutoStartDAX` como `True`.
3. Confirme que el botón **Enable** en el applet DAX está marcado (iluminado en verde). Si no lo está, haga clic en **Enable** para iniciar el puente en la sesión actual.

En el próximo lanzamiento, AetherSDR leerá `AutoStartDAX` y activará el puente automáticamente, reflejando el estado marcado en el botón **Enable**.

Para desactivar el inicio automático, haga clic en **Settings > Autostart DAX with AetherSDR** nuevamente para desmarcar la opción.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** (en el applet DAX) | Interruptor principal. Inicia o detiene el puente de audio DAX para la sesión actual y persiste el estado. | Off | On / Off | `AutoStartDAX` |
| **Settings > Autostart DAX with AetherSDR** | Elemento de menú marcable. Cuando está marcado, AetherSDR inicia el puente DAX en cada lanzamiento. | Off (sin marcar) | Marcado / Sin marcar | `AutoStartDAX` |
| Ganancia+medidor DAX 1 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 1. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 2. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 3. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 4. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Ganancia+medidor TX | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Significado de los indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Asignación DAX 1..4 | — o Slice A..H | La slice (si existe) asignada actualmente a este canal DAX. Muestra la letra de la slice en el color del modelo de radio activo. |
| Asignación TX | — o Slice A..H | La slice que actualmente tiene privilegios de TX (controla DAX TX). Muestra la letra de la slice en el color del modelo de radio activo. |

## Consejos

- El botón **Enable** y **Settings > Autostart DAX with AetherSDR** escriben la misma clave `AutoStartDAX`. Al hacer clic en cualquiera de ellos se actualiza la configuración compartida.
- Los valores de ganancia de los cuatro canales RX y del canal TX se guardan de forma independiente. Ajustarlos antes de activar el inicio automático asegura que se restaurarán en los mismos niveles en el próximo lanzamiento.
- Los indicadores de asignación de slice ahora muestran la letra de la slice en el color del modelo de radio activo (formato de texto enriquecido) para mejorar la visibilidad. Esto afecta tanto a las asignaciones de los canales RX de DAX como a los indicadores de asignación TX.
- En Linux, el audio DAX utiliza flujos nativos de PipeWire (`pw_stream`) para menor latencia, reduciendo la latencia de RX de aproximadamente 400 ms a aproximadamente 200 ms. Esto se aplica a todos los canales DAX RX.

## Solución de problemas

- **El applet DAX no es visible** — Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.
- **Enable está marcado pero el puente no se inicia en el próximo lanzamiento** — Verifique que **Settings > Autostart DAX with AetherSDR** tenga una marca de verificación. Al hacer clic en **Enable** en el applet solo se establece el estado del puente para la sesión actual y se persiste `AutoStartDAX`, pero confirmar que el elemento del menú está marcado asegura que la ruta de inicio automático se ejecute al lanzar.
- **El botón Enable aparece sin marcar después del lanzamiento a pesar de que el inicio automático está activado** — Esto puede ocurrir si AetherSDR se lanza antes de que se establezca una conexión con la radio. El applet DAX requiere una radio conectada. Conéctese a la radio y haga clic en **Enable** manualmente, o permita que AetherSDR se conecte antes de verificar el estado del puente.

## Relacionado

- [Descripción general del audio DAX](overview.md)
- [Activar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Establecer ganancia de RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)

# Inicio automático de DAX al arrancar

Active el ajuste `AutoStartDAX` para que el puente de audio DAX se inicie automáticamente cada vez que AetherSDR se abra, sin necesidad de hacer clic en Enable manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Si no lo está, haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet DAX haciendo clic en el botón **DAX** de la bandeja en la barra lateral derecha si aún no está visible.
2. Haga clic en **Settings > Autostart DAX with AetherSDR** para colocar una marca de verificación junto al elemento. Esto guarda `AutoStartDAX` como `True`.
3. Confirme que el botón **Enable** en el applet DAX esté marcado (iluminado en verde). Si no lo está, haga clic en **Enable** para iniciar el puente en la sesión actual.

En el próximo inicio, AetherSDR leerá `AutoStartDAX` y activará el puente automáticamente, reflejando el estado marcado en el botón **Enable**.

Para desactivar el inicio automático, haga clic nuevamente en **Settings > Autostart DAX with AetherSDR** para quitar la marca de verificación.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Enable** (en el applet DAX) | Interruptor principal. Inicia o detiene el puente de audio DAX en la sesión actual y guarda el estado. | Desactivado | Activado / Desactivado | `AutoStartDAX` |
| **Settings > Autostart DAX with AetherSDR** | Elemento de menú con marca de verificación. Cuando está marcado, AetherSDR inicia el puente DAX en cada arranque. | Desactivado (sin marcar) | Marcado / Sin marcar | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 1 de DAX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 2 de DAX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 3 de DAX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 4 de DAX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el flujo TX de DAX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Consejos

- El botón **Enable** y **Settings > Autostart DAX with AetherSDR** escriben la misma clave `AutoStartDAX`. Al hacer clic en cualquiera de los dos se actualiza el ajuste compartido.
- Los valores de ganancia de los cuatro canales RX y del canal TX se guardan de forma independiente. Ajustarlos antes de activar el inicio automático garantiza que se restauren con los mismos niveles en el próximo arranque.

## Solución de problemas

- **El applet DAX no está visible** — Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.
- **Enable está marcado pero el puente no se inicia en el siguiente arranque** — Verifique que **Settings > Autostart DAX with AetherSDR** tenga una marca de verificación. Hacer clic en **Enable** en el applet por sí solo establece el estado del puente para la sesión actual y guarda `AutoStartDAX`, pero confirmar que el elemento de menú está marcado garantiza que la ruta de inicio automático se ejecute al arrancar.
- **El botón Enable aparece sin marcar tras el arranque a pesar de tener el inicio automático activado** — Esto puede ocurrir si AetherSDR se inicia antes de que se establezca una conexión de radio. El applet DAX requiere una radio conectada. Conéctese a la radio y haga clic en **Enable** manualmente, o permita que AetherSDR se conecte antes de verificar el estado del puente.

## Relacionados

- [Descripción general del audio DAX](overview.md)
- [Activar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX en este momento](see-which-slice-is-currently-using-each-dax-channel.md)

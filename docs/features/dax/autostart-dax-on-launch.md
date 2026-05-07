# Autoiniciar DAX al Inicio

Active el ajuste `AutoStartDAX` para que el puente de audio DAX se inicie automáticamente cada vez que se abra AetherSDR, sin necesidad de hacer clic manualmente en **Enable** cada sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet DAX haciendo clic en el botón de la bandeja **DAX** en la barra lateral derecha si aún no está visible.
2. Haga clic en **Settings > Autostart DAX with AetherSDR** para marcar el elemento. Esto persiste `AutoStartDAX` como `True`.
3. Confirme que el botón **Enable** en el applet DAX esté marcado (iluminado en verde). Si no lo está, haga clic en **Enable** para iniciar el puente para la sesión actual.

En el siguiente inicio, AetherSDR leerá `AutoStartDAX` y activará el puente automáticamente, reflejando el estado marcado en el botón **Enable**.

Para desactivar el inicio automático, haga clic nuevamente en **Settings > Autostart DAX with AetherSDR** para desmarcar el elemento.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Enable** (en el applet DAX) | Interruptor principal. Inicia o detiene el puente de audio DAX para la sesión actual y persiste el estado. | Apagado | Encendido / Apagado | `AutoStartDAX` |
| **Settings > Autostart DAX with AetherSDR** | Elemento de menú marcable. Cuando está marcado, AetherSDR inicia el puente DAX en cada inicio. | Apagado (sin marcar) | Marcado / Sin marcar | `AutoStartDAX` |
| Control de ganancia+medidor DAX 1 | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 1. Arrastre para ajustar. | 0,5 | 0,0 – 1,0 | `DaxRxGain1` |
| Control de ganancia+medidor DAX 2 | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 2. Arrastre para ajustar. | 0,5 | 0,0 – 1,0 | `DaxRxGain2` |
| Control de ganancia+medidor DAX 3 | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 3. Arrastre para ajustar. | 0,5 | 0,0 – 1,0 | `DaxRxGain3` |
| Control de ganancia+medidor DAX 4 | Medidor de nivel y control deslizante de ganancia combinados para el canal de RX DAX 4. Arrastre para ajustar. | 0,5 | 0,0 – 1,0 | `DaxRxGain4` |
| Control de ganancia+medidor TX | Medidor de nivel y control deslizante de ganancia combinados para el flujo de TX DAX. Arrastre para ajustar. | 0,5 | 0,0 – 1,0 | `DaxTxGain` |

## Consejos

- El botón **Enable** y **Settings > Autostart DAX with AetherSDR** escriben la misma clave `AutoStartDAX`. Al hacer clic en cualquiera de ellos, se actualiza el ajuste compartido.
- Los valores de ganancia para los cuatro canales de RX y el canal de TX se guardan de forma independiente. Ajustarlos antes de activar el inicio automático significa que se restaurarán en los mismos niveles en el siguiente inicio.

## Solución de problemas

- **El applet DAX no es visible** — Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarlo.
- **Enable está marcado pero el puente no se inicia en el siguiente inicio** — Verifique que **Settings > Autostart DAX with AetherSDR** tenga una marca de verificación. Hacer clic en **Enable** en el applet por sí solo establece el estado del puente para la sesión actual y persiste `AutoStartDAX`, pero confirmar que el elemento del menú está marcado asegura que la ruta de inicio automático se ejecute al inicio.
- **El botón Enable está desmarcado después del inicio a pesar de que el inicio automático está activado** — Esto puede ocurrir si AetherSDR se inicia antes de que se establezca una conexión con la radio. El applet DAX requiere una radio conectada. Conéctese a la radio y haga clic en **Enable** manualmente, o permita que AetherSDR se conecte antes de verificar el estado del puente.

## Relacionado

- [Descripción general de audio DAX](overview.md)
- [Activar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia de RX DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia de TX DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)

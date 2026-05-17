# Inicio automático de DAX al iniciar

Active el ajuste `AutoStartDAX` para que el puente de audio DAX se inicie automáticamente cada vez que AetherSDR se abra, sin necesidad de hacer clic manualmente en "Enable" cada sesión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet DAX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Si no lo está, haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet DAX haciendo clic en el botón de bandeja **DAX** en la barra lateral derecha si aún no está visible.
2. Haga clic en **Settings > Autostart DAX with AetherSDR** para marcar el elemento. Esto establece `AutoStartDAX` como `True`.
3. Confirme que el botón **Enable** en el applet DAX esté marcado (iluminado en verde). Si no lo está, haga clic en **Enable** para iniciar el puente en la sesión actual.

En el próximo inicio, AetherSDR leerá `AutoStartDAX` y activará el puente automáticamente, reflejando el estado marcado en el botón **Enable**.

Para desactivar el inicio automático, haga clic en **Settings > Autostart DAX with AetherSDR** nuevamente para desmarcar el elemento.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| **Enable** (en el applet DAX) | Conmutador principal. Inicia o detiene el puente de audio DAX para la sesión actual y persiste el estado. | Apagado | Encendido / Apagado | `AutoStartDAX` |
| **Settings > Autostart DAX with AetherSDR** | Elemento de menú marcable. Cuando está marcado, AetherSDR inicia el puente DAX en cada inicio. | Apagado (sin marcar) | Marcado / Sin marcar | `AutoStartDAX` |
| Ganancia+medidor DAX 1 | Medidor de nivel y control deslizante de ganancia combinados para el canal de recepción DAX 1. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | Medidor de nivel y control deslizante de ganancia combinados para el canal de recepción DAX 2. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | Medidor de nivel y control deslizante de ganancia combinados para el canal de recepción DAX 3. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | Medidor de nivel y control deslizante de ganancia combinados para el canal de recepción DAX 4. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Ganancia+medidor TX | Medidor de nivel y control deslizante de ganancia combinados para el flujo de transmisión DAX. Arrastre para ajustar. | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Significado de los indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Asignación DAX 1..4 | — o Slice A..H | El slice (si existe) actualmente asignado a este canal DAX. Muestra la letra del slice en el color del modelo de radio activo. |
| Asignación TX | — o Slice A..H | El slice que actualmente tiene privilegios de transmisión (controla la TX de DAX). Muestra la letra del slice en el color del modelo de radio activo. |

## Consejos

- El botón **Enable** y **Settings > Autostart DAX with AetherSDR** escriben ambos la misma clave `AutoStartDAX`. Al hacer clic en cualquiera de ellos, se actualiza el ajuste compartido.
- Los valores de ganancia para los cuatro canales de recepción y el canal de transmisión se guardan de forma independiente. Ajustarlos antes de activar el inicio automático significa que se restaurarán en los mismos niveles en el próximo inicio.
- Los indicadores de asignación de slice ahora muestran la letra del slice en el color del modelo de radio activo (formato de texto enriquecido) para mejorar la visibilidad. Esto afecta tanto a las asignaciones de canales de recepción DAX como a los indicadores de asignación de transmisión.

## Solución de problemas

- **El applet DAX no está visible** — Haga clic en el botón de bandeja **DAX** en la barra lateral derecha para mostrarlo.
- **Enable está marcado pero el puente no se inicia en el próximo inicio** — Verifique que **Settings > Autostart DAX with AetherSDR** tenga una marca de verificación. Hacer clic en **Enable** en el applet por sí solo establece el estado del puente para la sesión actual y persiste `AutoStartDAX`, pero confirmar que el elemento del menú está marcado asegura que la ruta de inicio automático se ejecute al iniciar.
- **El botón Enable está desmarcado después del inicio a pesar de que el inicio automático está activado** — Esto puede ocurrir si AetherSDR se inicia antes de que se establezca una conexión con la radio. El applet DAX requiere una radio conectada. Conéctese a la radio y haga clic en **Enable** manualmente, o permita que AetherSDR se conecte antes de verificar el estado del puente.

## Relacionado

- [DAX Audio overview](overview.md)
- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Set DAX RX gain per channel](set-dax-rx-gain-per-channel.md)
- [Set DAX TX gain](set-dax-tx-gain.md)
- [See which slice is currently using each DAX channel](see-which-slice-is-currently-using-each-dax-channel.md)

# Inicio automático de DAX al lanzar la aplicación

Configure AetherSDR para que inicie el puente de audio DAX automáticamente cada vez que se abra la aplicación, de modo que no sea necesario activar DAX manualmente tras cada reinicio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 antes de que los flujos DAX se activen, incluso si el inicio automático está habilitado.
- El inicio automático de DAX está disponible en macOS y en sistemas Linux con PipeWire habilitado.

## Pasos

1. Abra el applet de audio DAX haciendo clic en el botón **DAX** de la bandeja en la barra lateral derecha. Si el panel del applet no está visible, actívelo con `View > Applet Panel`.
2. Para habilitar el inicio automático mediante el menú, haga clic en `Settings > Autostart DAX with AetherSDR`. Aparece una marca de verificación junto al elemento cuando el inicio automático está activado. Esto guarda la configuración `AutoStartDAX`.
3. Alternativamente, haga clic en **Enable** dentro del applet de audio DAX. Al hacer clic en **Enable** se inicia el puente DAX de inmediato y se guarda `AutoStartDAX` para que el puente se inicie automáticamente en el siguiente lanzamiento.
4. Verifique que la configuración surtió efecto reiniciando AetherSDR y confirmando que **Enable** aparece activo (resaltado en verde) cuando se abre el applet de audio DAX.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** | Interruptor principal del puente de audio DAX. Inicia o detiene todos los flujos DAX RX y TX. El estado se guarda y se restaura al lanzar la aplicación. | Off | On / Off | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal 1 de DAX RX. Arrastre para ajustar la ganancia. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal 2 de DAX RX. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal 3 de DAX RX. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal 4 de DAX RX. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. | 0.5 | 0.0–1.0 | `DaxTxGain` |

## Consejos

- El elemento de menú `Settings > Autostart DAX with AetherSDR` y el botón **Enable** dentro del applet escriben en la misma configuración `AutoStartDAX`. Cualquiera de los dos métodos produce el mismo resultado.
- Los valores de ganancia de todos los canales (`DaxRxGain1` hasta `DaxRxGain4` y `DaxTxGain`) se guardan de forma independiente cada vez que arrastra un control deslizante, y se restauran al lanzar la aplicación independientemente de si el inicio automático está activado.

## Solución de problemas

- **Enable aparece activo tras el lanzamiento pero no pasa audio** — Los flujos DAX requieren una conexión de radio activa. Confirme que AetherSDR está conectado al FLEX-8600 antes de esperar audio. El indicador de asignación de slice junto a cada canal mostrará `—` si ningún slice está enrutado a ese canal.
- **`Settings > Autostart DAX with AetherSDR` no aparece** — Este elemento de menú solo está presente en plataformas compatibles (macOS y Linux con PipeWire habilitado). En sistemas no compatibles, use el botón **Enable** en el applet en cada sesión.

## Relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia DAX RX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)

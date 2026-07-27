# Miniaplicación de audio DAX

## Nota sobre Windows

En Windows, AetherSDR no incluye un controlador de audio DAX integrado. La miniaplicación DAX muestra únicamente el siguiente mensaje informativo y no hay controles disponibles:

> No hay controlador DAX integrado en Windows. Use TCI o SmartSDR DAX.

El enrutamiento de audio DAX en Windows es compatible a través de los controladores SmartSDR DAX de FlexRadio o mediante TCI. Consulte **Help > Configuring Data Modes** para obtener instrucciones de configuración.

En macOS y Linux, la miniaplicación DAX completa está disponible como se describe a continuación.

## Inicio automático de DAX al iniciar

Active la opción `AutoStartDAX` para que el puente de audio DAX se inicie automáticamente cada vez que se abra AetherSDR, sin necesidad de hacer clic manualmente en Enable en cada sesión.

### Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. La miniaplicación DAX requiere una conexión activa con la radio.
- La miniaplicación DAX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarla.

### Pasos

1. Abra la miniaplicación DAX haciendo clic en el botón de la bandeja **DAX** en la barra lateral derecha si aún no está visible.
2. Haga clic en **Settings > Autostart DAX with AetherSDR** para marcar la opción. Esto establece `AutoStartDAX` como `True`.
3. Confirme que el botón **Enable** en la miniaplicación DAX muestra **Enabled** (iluminado en verde). Si muestra **Disabled**, haga clic en él para iniciar el puente en la sesión actual.

En el próximo inicio, AetherSDR leerá `AutoStartDAX` y activará el puente automáticamente, reflejando el estado habilitado en el botón **Enable** (mostrando **Enabled**).

Para desactivar el inicio automático, haga clic nuevamente en **Settings > Autostart DAX with AetherSDR** para desmarcar la opción.

## Función de cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Botón **Enable** en la miniaplicación DAX | Interruptor principal. Inicia o detiene el puente de audio DAX para la sesión actual y conserva el estado. Muestra **Enabled** cuando está activo, **Disabled** cuando está inactivo. | Disabled | Enabled / Disabled | `AutoStartDAX` |
| **Settings > Autostart DAX with AetherSDR** | Elemento de menú seleccionable. Cuando está marcado, AetherSDR inicia el puente DAX en cada inicio. | Off (sin marcar) | Checked / Unchecked | `AutoStartDAX` |
| Indicador+ganancia DAX 1 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 1. Arrastre para ajustar. Nombre accesible: "DAX RX 1 gain". | 0.5 | 0.0 – 1.0 | `DaxRxGain1` |
| Indicador+ganancia DAX 2 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 2. Arrastre para ajustar. Nombre accesible: "DAX RX 2 gain". | 0.5 | 0.0 – 1.0 | `DaxRxGain2` |
| Indicador+ganancia DAX 3 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 3. Arrastre para ajustar. Nombre accesible: "DAX RX 3 gain". | 0.5 | 0.0 – 1.0 | `DaxRxGain3` |
| Indicador+ganancia DAX 4 | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX RX 4. Arrastre para ajustar. Nombre accesible: "DAX RX 4 gain". | 0.5 | 0.0 – 1.0 | `DaxRxGain4` |
| Indicador+ganancia TX | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. Arrastre para ajustar. Nombre accesible: "DAX TX gain". | 0.5 | 0.0 – 1.0 | `DaxTxGain` |

## Significado de los indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Asignación DAX 1..4 | — o Slice A..H | La slice (si existe) asignada actualmente a este canal DAX. Muestra la letra de la slice en el color del modelo de radio activo. |
| Asignación TX | — o Slice A..H | La slice que actualmente tiene privilegios de TX (controla DAX TX). Muestra la letra de la slice en el color del modelo de radio activo. |

## Consejos

- El botón **Enable** y **Settings > Autostart DAX with AetherSDR** escriben la misma clave `AutoStartDAX`. Al hacer clic en cualquiera de ellos, se actualiza la configuración compartida.
- Los valores de ganancia para los cuatro canales RX y el canal TX se guardan de forma independiente. Ajustarlos antes de activar el inicio automático significa que se restaurarán en los mismos niveles en el próximo inicio.
- Los indicadores de asignación de slice muestran la letra de la slice en el color del modelo de radio activo (formato de texto enriquecido) para una mejor visibilidad. Esto afecta tanto a las asignaciones de canales DAX RX como a los indicadores de asignación TX.
- En Linux, el audio DAX utiliza flujos nativos de PipeWire (`pw_stream`) para una menor latencia, reduciendo la latencia RX de aproximadamente 400 ms a aproximadamente 200 ms. Esto se aplica a todos los canales DAX RX.
- Cada control deslizante de ganancia tiene un nombre accesible configurado para compatibilidad con lectores de pantalla: "DAX RX N gain" para los canales 1-4 y "DAX TX gain" para el canal de transmisión.
- El botón **Enable** ahora actualiza dinámicamente su texto para mostrar **Enabled** o **Disabled** según el estado actual, proporcionando una retroalimentación visual más clara.

## Solución de problemas

- **La miniaplicación DAX no es visible** — Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarla.
- **Enable está marcado pero el puente no se inicia en el próximo inicio** — Verifique que **Settings > Autostart DAX with AetherSDR** tenga una marca de verificación. Hacer clic en **Enable** en la miniaplicación solo establece el estado del puente para la sesión actual y conserva `AutoStartDAX`, pero confirmar que el elemento del menú está marcado asegura que la ruta de inicio automático se ejecute al iniciar.
- **El botón Enable muestra Disabled después del inicio a pesar de que el inicio automático está activado** — Esto puede ocurrir si AetherSDR se inicia antes de que se establezca una conexión con la radio. La miniaplicación DAX requiere una radio conectada. Conéctese a la radio y haga clic en **Enable** manualmente, o permita que AetherSDR se conecte antes de verificar el estado del puente.
- **En Windows, la miniaplicación DAX muestra solo una nota** — Esto es normal. AetherSDR no incluye un controlador de audio DAX integrado en Windows. Use los controladores SmartSDR DAX de FlexRadio o TCI en su lugar. Consulte **Help > Configuring Data Modes** para más detalles.

## Relacionados

- [Descripción general de audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Configurar ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Configurar ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)

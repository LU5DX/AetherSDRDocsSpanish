# Inicio automático de DAX al arrancar

Configure AetherSDR para que inicie el puente de audio DAX automáticamente cada vez que la aplicación se conecte a la radio, de modo que no sea necesario hacer clic en **Enable** manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar instalado y poder comunicarse con su FLEX-8600 en la red.
- DAX está disponible en sistemas macOS y Linux con PipeWire.

## Pasos

1. Abra el applet DAX Audio haciendo clic en el botón **DAX** de la bandeja en la barra lateral derecha. Si el panel del applet no está visible, actívelo con `View > Applet Panel`.
2. Para habilitar el inicio automático mediante el menú: haga clic en `Settings > Autostart DAX with AetherSDR`. Aparece una marca de verificación junto al elemento cuando el inicio automático está activo. AetherSDR guarda esto como `AutoStartDAX`.
3. De manera alternativa, habilite DAX para la sesión actual haciendo clic en **Enable** en el applet DAX Audio. Esto también guarda `AutoStartDAX` de forma permanente, por lo que DAX se iniciará automáticamente en el próximo arranque.
4. Para deshabilitar el inicio automático, haga clic de nuevo en `Settings > Autostart DAX with AetherSDR` para quitar la marca de verificación, o haga clic en **Enable** en el applet para desactivarlo.

## Función de cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** (botón de alternancia) | Inicia o detiene el puente de audio DAX. Al activarlo también se establece el inicio automático. | Off | On / Off | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 1 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 2 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 3 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal RX 4 de DAX. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el flujo TX de DAX. | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Slice-assignment status | Indicador de solo lectura que muestra qué slice está enrutado a cada canal DAX. Muestra `—` cuando no hay asignación, o `Slice A`–`Slice H` cuando está asignado. | `—` | — | — |

## Consejos

- El elemento del menú y el botón **Enable** escriben en la misma configuración `AutoStartDAX`. Cualquiera de los dos métodos conserva la elección entre reinicios.
- Las configuraciones de ganancia (`DaxRxGain1`–`DaxRxGain4`, `DaxTxGain`) se guardan de forma independiente cada vez que se arrastra un control deslizante. Se restauran en el próximo arranque independientemente de si el inicio automático está activado.

## Solución de problemas

- **DAX no inicia automáticamente a pesar de que la marca de verificación está establecida** — Confirme que su sistema cumple el requisito de plataforma (macOS o PipeWire en Linux). En otras configuraciones, la opción no tiene efecto.
- **El botón Enable no responde** — El applet DAX requiere una conexión activa con la radio. Conéctese primero al FLEX-8600 mediante `Settings > Connect to Radio...` y vuelva a intentarlo.

## Temas relacionados

- [Descripción general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Ajustar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando cada canal DAX en este momento](see-which-slice-is-currently-using-each-dax-channel.md)

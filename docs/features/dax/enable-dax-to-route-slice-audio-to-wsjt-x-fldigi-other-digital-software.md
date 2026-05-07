# Habilitar DAX para enrutar el audio de un slice a WSJT-X / FLDigi / otro software digital

DAX (Digital Audio eXchange) crea flujos de audio virtuales entre AetherSDR y otro software que se ejecuta en la misma máquina. Actívelo cuando desee que WSJT-X, FLDigi o cualquier otro programa de modo digital reciba audio de un slice de radio o envíe audio de vuelta a la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. DAX requiere una conexión activa con la radio.
- Cada slice que desee enrutar debe tener un canal DAX asignado en la configuración de slices de la radio. El applet de DAX muestra qué slices ya están asignados.
- En Linux, PipeWire debe estar en ejecución. En macOS, el subsistema de audio del sistema maneja el enrutamiento automáticamente.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de audio DAX. El applet está oculto por defecto.
2. Haga clic en **Enable**. El botón se vuelve verde cuando DAX está activo. AetherSDR guarda este estado como `AutoStartDAX`.
3. Verifique los indicadores de asignación de slice junto a cada etiqueta de canal DAX (por ejemplo, **DAX 1:**, **DAX 2:**). Cada indicador muestra `—` (sin slice asignado) o `Slice A` a `Slice H`. Confirme que el canal que desea muestra el slice correcto.
4. En su software de modo digital (WSJT-X, FLDigi, etc.), seleccione el dispositivo de audio virtual DAX correspondiente como dispositivo de audio de entrada (y salida para TX). Consulte [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md) para ver los pasos específicos por aplicación.
5. Transmita un tono de audio de prueba desde su software digital y observe el medidor **TX** en el applet. Ajuste el control deslizante **TX gain+meter** para que el nivel se mantenga por debajo de la saturación.
6. Reciba una señal y observe el control deslizante **DAX 1–4 gain+meter** para el canal que asignó. Ajuste el control deslizante para establecer un nivel cómodo para la entrada de audio de su software.

## Descripción de cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Enable | Conmutador maestro. Inicia o detiene todos los flujos de audio de DAX. | Apagado | Encendido / Apagado | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal DAX 1. Arrastre para ajustar la ganancia de RX enviada al software en ese canal. | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Igual que DAX 1, para el canal 2. | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Igual que DAX 1, para el canal 3. | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Igual que DAX 1, para el canal 4. | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el flujo TX de DAX (audio desde su software digital hacia la radio). | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice | Solo lectura. Muestra qué slice (A–H) está enrutado a cada canal DAX, o `—` si no hay ninguno. | `—` | `—` o `Slice A`–`Slice H` | — |

## Consejos

- Para iniciar DAX automáticamente cada vez que se lance AetherSDR, marque `Settings > Autostart DAX with AetherSDR` en el menú. Esto escribe la misma configuración `AutoStartDAX` que controla el botón **Enable**.
- El indicador de TX junto a la etiqueta **TX** muestra qué slice tiene actualmente los privilegios de TX. Si muestra `—`, ningún slice está configurado como slice de TX y el audio TX de DAX no llegará a la radio.
- Los controles deslizantes de ganancia son posteriores al fader: la barra del medidor refleja el nivel después de su ajuste de ganancia, por lo que lo que ve es lo que recibe la aplicación receptora.

## Solución de problemas

- **Los canales DAX muestran `—` y no pasa audio** — Ningún slice tiene un canal DAX asignado. Asigne un canal DAX al slice usando los controles de slice en el panadapter, luego confirme que el indicador en el applet se actualice a `Slice A` (o la letra correspondiente).
- **El botón Enable no permanece marcado después de reiniciar AetherSDR** — `AutoStartDAX` no se guardó. Active la configuración a través de `Settings > Autostart DAX with AetherSDR` para que se aplique al iniciar.
- **El software digital no recibe audio a pesar de que DAX está habilitado** — Confirme que el dispositivo virtual DAX correcto está seleccionado como entrada de audio en su software de modo digital. El nombre del dispositivo depende de su sistema operativo y subsistema de audio.
- **El medidor TX está activo pero la radio no transmite** — Confirme que el indicador de slice TX muestra un slice válido. Si muestra `—`, ningún slice tiene privilegios de TX. Consulte [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md).

## Relacionados

- [Descripción general de Audio DAX](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Establecer ganancia de RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice de TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

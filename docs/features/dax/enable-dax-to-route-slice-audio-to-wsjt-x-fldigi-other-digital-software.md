# Habilite DAX para enrutar el audio de un slice a WSJT-X, FLDigi u otro software digital

DAX (Digital Audio eXchange) crea flujos de audio virtuales entre AetherSDR y otro software que se ejecute en la misma máquina. Actívelo cuando desee que WSJT-X, FLDigi o cualquier otro programa de modo digital reciba audio de un slice de la radio o envíe audio de vuelta a la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. DAX requiere una conexión de radio activa.
- Cada slice que desee enrutar debe tener un canal DAX asignado en la configuración de slices de la radio. El applet de DAX muestra qué slices ya están asignados.
- En Linux, PipeWire debe estar en ejecución. En macOS, el subsistema de audio del sistema maneja el enrutamiento automáticamente.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de audio DAX. El applet está oculto por defecto.
2. Haga clic en **Enable**. El botón se vuelve verde cuando DAX está activo. AetherSDR guarda este estado como `AutoStartDAX`.
3. Revise los indicadores de asignación de slices junto a cada etiqueta de canal DAX (por ejemplo, **DAX 1:**, **DAX 2:**). Cada indicador muestra `—` (ningún slice asignado) o `Slice A` hasta `Slice H`. Confirme que el canal que desea muestra el slice correcto.
4. En su software de modo digital (WSJT-X, FLDigi, etc.), seleccione el dispositivo de audio virtual DAX correspondiente como dispositivo de audio de entrada (y salida para TX). Consulte [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md) para los pasos específicos de cada aplicación.
5. Transmita un tono de audio de prueba desde su software digital y observe el medidor **TX** en el applet. Ajuste el deslizador **TX gain+meter** para que el nivel se mantenga por debajo de la saturación.
6. Reciba una señal y observe el deslizador **DAX 1–4 gain+meter** para el canal que asignó. Ajuste el deslizador para establecer un nivel cómodo para la entrada de audio de su software.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Enable | Interruptor maestro. Inicia o detiene todos los flujos de audio DAX. | Off | On / Off | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor de nivel combinado y deslizador de ganancia para el canal DAX 1. Arrastre para ajustar la ganancia de RX enviada al software en ese canal. Usa el nombre accesible "DAX RX 1 gain". | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Igual que DAX 1, para el canal 2. Usa el nombre accesible "DAX RX 2 gain". | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Igual que DAX 1, para el canal 3. Usa el nombre accesible "DAX RX 3 gain". | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Igual que DAX 1, para el canal 4. Usa el nombre accesible "DAX RX 4 gain". | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor de nivel combinado y deslizador de ganancia para el flujo de TX de DAX (audio desde su software digital hacia la radio). Usa el nombre accesible "DAX TX gain". | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice | Solo lectura. Muestra qué slice (A–H) está enrutado a cada canal DAX, o `—` si ninguno. Las letras de los slices se renderizan en texto enriquecido para mejorar la legibilidad. | `—` | `—` o `Slice A`–`Slice H` | — |

## Consejos

- Para iniciar DAX automáticamente cada vez que AetherSDR se inicie, marque `Settings > Autostart DAX with AetherSDR` en el menú. Esto escribe la misma configuración `AutoStartDAX` que controla el botón **Enable**.
- El indicador TX junto a la etiqueta **TX** muestra qué slice tiene actualmente los privilegios de TX. Si muestra `—`, ningún slice está configurado como slice TX y el audio de TX de DAX no llegará a la radio. Las letras de los slices se renderizan en texto enriquecido para mejorar la legibilidad.
- Los deslizadores de ganancia son post-fader: la barra del medidor refleja el nivel después de su ajuste de ganancia, por lo que lo que ve es lo que recibe la aplicación receptora.
- En Linux (v26.6.1+), la latencia de RX de DAX es de aproximadamente 200 ms, reducida desde aproximadamente 400 ms en versiones anteriores, mediante transmisión nativa de PipeWire.

## Solución de problemas

- **Los canales DAX muestran `—` y no pasa audio** — Ningún slice tiene asignado un canal DAX. Asigne un canal DAX al slice usando los controles de slice en el panadapter, luego confirme que el indicador en el applet se actualice a `Slice A` (o la letra correspondiente).
- **El botón Enable no permanece marcado después de reiniciar AetherSDR** — `AutoStartDAX` no se guardó. Active la configuración a través de `Settings > Autostart DAX with AetherSDR` para que se aplique al inicio.
- **El software digital no recibe audio a pesar de que DAX está habilitado** — Confirme que el dispositivo virtual DAX correcto esté seleccionado como entrada de audio en su software de modo digital. El nombre del dispositivo depende de su sistema operativo y subsistema de audio.
- **El medidor TX está activo pero la radio no transmite** — Confirme que el indicador de slice TX muestre un slice válido. Si muestra `—`, ningún slice tiene privilegios de TX. Consulte [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md).

## Relacionado

- [Descripción general de audio DAX](overview.md)
- [Inicio automático de DAX al arrancar](autostart-dax-on-launch.md)
- [Establecer ganancia de RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Establecer ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

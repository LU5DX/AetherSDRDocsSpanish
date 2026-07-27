# Habilitar DAX para enrutar audio de un slice a WSJT-X / FLDigi / otro software digital

DAX (Digital Audio eXchange) crea flujos de audio virtuales entre AetherSDR y otro software que se ejecuta en la misma máquina. Actívelo cuando desee que WSJT-X, FLDigi o cualquier otro programa de modo digital reciba audio de un slice de radio o envíe audio de vuelta a la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. DAX requiere una conexión de radio activa.
- Cada slice que desee enrutar debe tener un canal DAX asignado en la configuración de slices de la radio. El applet de DAX muestra qué slices ya están asignados.
- En Linux, PipeWire debe estar en ejecución. En macOS, el subsistema de audio del sistema maneja el enrutamiento automáticamente.
- En Windows, AetherSDR no incluye un controlador de audio DAX incorporado. El audio DAX en Windows requiere los controladores SmartSDR DAX de FlexRadio o TCI.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet de Audio DAX. El applet está oculto de forma predeterminada.
2. En macOS y Linux, haga clic en **Enable** (etiquetado como **Disabled** cuando está apagado). El botón cambia a **Enabled** y se vuelve verde cuando DAX está activo. AetherSDR guarda este estado como `AutoStartDAX`.
3. En Windows, el applet DAX muestra una nota "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." El botón Enable y todos los medidores no están disponibles. Proceda con sus controladores SmartSDR DAX existentes.
4. Verifique los indicadores de asignación de slices junto a cada etiqueta de canal DAX (por ejemplo, **DAX 1:**, **DAX 2:**). Cada indicador muestra `—` (ningún slice asignado) o `Slice A` a `Slice H`. Confirme que el canal que desea muestra el slice correcto.
5. En su software de modo digital (WSJT-X, FLDigi, etc.), seleccione el dispositivo de audio virtual DAX correspondiente como dispositivo de audio de entrada (y salida para TX). Consulte [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md) para conocer los pasos específicos de cada aplicación.
6. Transmita un tono de audio de prueba desde su software digital y observe el medidor **TX** en el applet. Ajuste el control deslizante **TX gain+meter** para que el nivel se mantenga por debajo del recorte.
7. Reciba una señal y observe el control deslizante **DAX 1–4 gain+meter** para el canal que asignó. Ajuste el control deslizante para establecer un nivel cómodo para la entrada de audio de su software.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Enable | Interruptor maestro. Inicia o detiene todos los flujos de audio DAX. Solo en macOS/Linux. En Windows, el botón no está disponible. | Disabled | Disabled / Enabled | `AutoStartDAX` |
| DAX 1 gain+meter | Medidor de nivel combinado y control deslizante de ganancia para el canal DAX 1. Arrastre para ajustar la ganancia RX enviada al software en ese canal. Usa el nombre accesible "DAX RX 1 gain". | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| DAX 2 gain+meter | Igual que DAX 1, para el canal 2. Usa el nombre accesible "DAX RX 2 gain". | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| DAX 3 gain+meter | Igual que DAX 1, para el canal 3. Usa el nombre accesible "DAX RX 3 gain". | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| DAX 4 gain+meter | Igual que DAX 1, para el canal 4. Usa el nombre accesible "DAX RX 4 gain". | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| TX gain+meter | Medidor de nivel combinado y control deslizante de ganancia para el flujo TX de DAX (audio desde su software digital hacia la radio). Usa el nombre accesible "DAX TX gain". | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice | Solo lectura. Muestra qué slice (A–H) está enrutado a cada canal DAX, o `—` si ninguno. Las letras de slice se renderizan en texto enriquecido para mejorar la legibilidad. | `—` | `—` o `Slice A`–`Slice H` | — |

## Consejos

- Para iniciar DAX automáticamente cada vez que se lance AetherSDR, marque `Settings > Autostart DAX with AetherSDR` en el menú. Esto escribe la misma configuración `AutoStartDAX` que controla el botón **Enable**.
- El indicador TX junto a la etiqueta **TX** muestra qué slice tiene actualmente los privilegios de TX. Si muestra `—`, ningún slice está configurado como slice TX y el audio TX de DAX no llegará a la radio. Las letras de slice se renderizan en texto enriquecido para mejorar la legibilidad.
- Los controles deslizantes de ganancia son post-fader: la barra del medidor refleja el nivel después de su ajuste de ganancia, por lo que lo que ve es lo que recibe la aplicación receptora.
- En Linux (v26.6.1+), la latencia RX de DAX es de aproximadamente 200 ms, reducida de aproximadamente 400 ms en versiones anteriores, mediante la transmisión nativa de PipeWire.
- En Windows, consulte `Help > Configuring Data Modes` para obtener detalles sobre cómo configurar el enrutamiento de audio con controladores DAX externos.

## Solución de problemas

- **Los canales DAX muestran `—` y no pasa audio** — Ningún slice tiene un canal DAX asignado. Asigne un canal DAX al slice usando los controles de slice en el panadapter, luego confirme que el indicador en el applet se actualice a `Slice A` (o la letra correspondiente).
- **El botón Enable no permanece marcado después de reiniciar AetherSDR** — `AutoStartDAX` no se guardó. Active la configuración a través de `Settings > Autostart DAX with AetherSDR` para que se aplique al iniciar.
- **El software digital no recibe audio a pesar de que DAX está habilitado** — Confirme que el dispositivo virtual DAX correcto esté seleccionado como entrada de audio en su software de modo digital. El nombre del dispositivo depende de su sistema operativo y subsistema de audio. En Windows, asegúrese de que los controladores SmartSDR DAX estén instalados.
- **El medidor TX está activo pero la radio no está transmitiendo** — Confirme que el indicador del slice TX muestre un slice válido. Si muestra `—`, ningún slice tiene privilegios de TX. Consulte [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md).
- **El botón Enable de DAX y los medidores no son visibles en Windows** — Este es un comportamiento esperado. AetherSDR no incluye controladores de audio DAX incorporados para Windows. Use los controladores SmartSDR DAX de FlexRadio o TCI para audio DAX en Windows. Consulte `Help > Configuring Data Modes`.

## Relacionados

- [Descripción general de Audio DAX](overview.md)
- [Iniciar DAX automáticamente al arrancar](autostart-dax-on-launch.md)
- [Configurar la ganancia RX de DAX por canal](set-dax-rx-gain-per-channel.md)
- [Configurar la ganancia TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Identificar qué slice es el slice TX](identify-which-slice-is-the-tx-slice.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)

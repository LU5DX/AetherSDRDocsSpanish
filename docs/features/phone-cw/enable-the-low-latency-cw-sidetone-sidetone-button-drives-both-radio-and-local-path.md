# Activar el tono lateral de CW con baja latencia (El botón de tono lateral controla tanto la ruta de la radio como la local)

Al activar el tono lateral de CW en AetherSDR se habilitan dos rutas simultáneamente: el monitor alimentado por DAX de la radio y un generador de tono local con una latencia de aproximadamente 10 ms. Un único botón y un único control deslizante de volumen controlan ambas rutas al mismo tiempo, para que escuche un tono coherente independientemente de la fluctuación de la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW requiere una conexión activa con la radio.
- El slice activo debe estar en un modo CW. El panel del applet cambia automáticamente del subpanel Phone al subpanel CW cuando se detecta el modo CW.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que se muestra el subpanel CW. Si se muestra el subpanel Phone, cambie el slice activo a un modo CW en la radio; el panel cambiará automáticamente.
3. Haga clic en **Sidetone** para activar el tono lateral. El botón se ilumina cuando está activo.
4. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El control deslizante controla simultáneamente el volumen del monitor de la radio y el volumen del generador de tono local.
5. Opcionalmente, ajuste **Pitch < / >** para establecer la frecuencia del tono lateral. El tono sigue la configuración de `cw_pitch` de la radio automáticamente, pero puede cambiarlo en incrementos de 10 Hz usando los controles **<** y **>**. También puede escribir un valor directamente (100–6000) en el campo QLineEdit (v0.9.8).
6. Para **Delay (CW)**, **Speed (CW)** y **Sidetone volume**, haga clic en el valor numérico y escriba un nuevo número directamente. Presione Enter o Tab para aplicar. El control deslizante y el valor escrito se mantienen sincronizados automáticamente (v0.9.8).

## Qué hace cada control

| Control             | Tipo                                                                                                                                                                                                                                                           | Valor predeterminado                                                                                                      |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Level               | Medidor. Muestra el nivel máximo de entrada del micrófono en dBFS (panel Phone). Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo.                                                                                                   | —                                                                                                                         |
| Compression         | Medidor. Muestra la cantidad de compresión de voz en dB (panel Phone). Relleno inverso. Bloqueado por el estado TRANSMITTING del interbloqueo de la radio y la habilitación del procesador de voz.                                                             | —                                                                                                                         |
| ALC (panel Phone)   | Medidor. Muestra la lectura de control automático de nivel de MeterModel::swAlcChanged (pico SSB post-ALC por software en dBFS). Relleno de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.                                                              | Reconfigurado desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel CW. |
| ALC (panel CW)      | Medidor. Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas coherentes en voz y CW. Relleno de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.                                                               | Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight.                         |
| Mic profile         | Cuadro combinado. Carga el perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile.                                                                                                                                               | —                                                                                                                         |
| Mic source          | Cuadro combinado. Selecciona la fuente de entrada del micrófono (MIC, BAL, LINE, ACC, PC, más cualquier otra de micInputList()); llama a TransmitModel::setMicSelection.                                                                                       | —                                                                                                                         |
| Mic gain            | Control deslizante. Ajusta el nivel de entrada del micrófono (0–100). Para la fuente 'PC' usa la persistencia local de PcMicGain. Valor predeterminado: 50. Clave de configuración: `PcMicGain`.                                                               | 50                                                                                                                        |
| +ACC                | Botón de alternancia. Habilita la mezcla de entrada del micrófono auxiliar; llama a TransmitModel::setMicAcc.                                                                                                                                                  | —                                                                                                                         |
| PROC                | Botón de alternancia. Activa el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable.                                                                                                                                                            | —                                                                                                                         |
| NOR/DX/DX+          | Control deslizante. Nivel del procesador de tres posiciones (0=NOR, 1=DX, 2=DX+); llama a TransmitModel::setSpeechProcessorLevel.                                                                                                                              | 0 (NOR)                                                                                                                   |
| DAX                 | Botón de alternancia. Habilita DAX como fuente de audio TX; llama a TransmitModel::setDax.                                                                                                                                                                    | —                                                                                                                         |
| MON                 | Botón de alternancia. Habilita el monitor de tono lateral TX; llama a TransmitModel::setSbMonitor.                                                                                                                                                            | —                                                                                                                         |
| Monitor volume      | Control deslizante. Establece el volumen del monitor de banda lateral (0–100); llama a TransmitModel::setMonGainSb.                                                                                                                                            | —                                                                                                                         |
| Delay (CW)          | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (0–2000 ms) directamente en el campo o arrastre el control deslizante. Llama a TransmitModel::setCwDelay.                                                                                          | 500 ms                                                                                                                    |
| Speed (CW)          | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (5–100 PPM) directamente en el campo o arrastre el control deslizante. Llama a TransmitModel::setCwSpeed.                                                                                          | 20 PPM                                                                                                                    |
| Sidetone            | Botón de alternancia. Activa el monitor de tono lateral CW; llama a TransmitModel::setCwSidetone. También habilita/deshabilita el CwSidetoneGenerator local al mismo tiempo (v0.9.1+).                                                                         | —                                                                                                                         |
| Sidetone volume     | Control deslizante con QLineEdit (v0.9.8). Escriba un valor (0–100) directamente en el campo o arrastre el control deslizante. Llama a TransmitModel::setMonGainCw. También establece el volumen del generador de tono lateral local al mismo tiempo.          | 50                                                                                                                        |
| Pitch < / >         | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para cambiarlo en pasos de 10 Hz. Llama a TransmitModel::setCwPitch (v0.9.8, #2429).                                                                           | 600 Hz                                                                                                                    |
| L / R pan (CW)      | Control deslizante. Establece la panorámica estéreo del monitor CW (0–100); llama a TransmitModel::setMonPanCw y aplica panorámica de potencia constante al generador de tono lateral local (v0.9.1+).                                                          | 50 (centro)                                                                                                               |
| Breakin             | Botón de alternancia. Activa el break-in completo (QSK); llama a TransmitModel::setCwBreakIn.                                                                                                                                                                  | —                                                                                                                         |
| Iambic              | Botón de alternancia. Activa el manipulador de paletas iámbico; llama a TransmitModel::setCwIambic.                                                                                                                                                            | —                                                                                                                         |

## Entrada de valor directa (v0.9.8)

En v0.9.8, las cuatro etiquetas de valor numérico en el subpanel CW se actualizaron de etiquetas de solo lectura a campos QLineEdit editables:

- **Delay (CW)** — Escriba cualquier valor de 0 a 2000 ms. Presione Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Speed (CW)** — Escriba cualquier valor de 5 a 100 PPM. Presione Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Sidetone volume** — Escriba cualquier valor de 0 a 100. Presione Enter o Tab para aplicar. El control deslizante adyacente se mueve para coincidir.
- **Pitch < / >** — Escriba cualquier valor de 100 a 6000 Hz. Presione Enter o Tab para aplicar. Los botones **<** y **>** cambian en pasos de 10 Hz.

Cuando escribe un valor que está fuera del rango válido, el campo limita el valor al límite válido más cercano (paridad SmartSDR).

## Medidores ALC en v26.5.1

En v26.5.1, tanto el subpanel Phone como el CW recibieron indicadores ALC idénticos que leen del medidor de software ALC (MeterModel::swAlcChanged). Esto reemplaza la ruta anterior de hardware ALC (tensión RCA) que producía lecturas sin significado.

- Ambos indicadores muestran en dBFS con un rango de -20 a 0 dBFS.
- La dirección de llenado es de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.
- Aparece una zona roja por encima de -3 dBFS.
- Los valores fuera del rango [-20, 0] se limitan al punto final más cercano.
- La ranura updateAlc() única impulsa ambos indicadores simultáneamente, asegurando que los operadores de SSB y CW vean la misma lectura de pico post-ALC.

## Modo RADE y el control deslizante de nivel de micrófono

Cuando el modo RADE está activo, el control deslizante **Mic gain** opera como un control de ganancia local en lugar de enviar un comando de nivel de micrófono a la radio. El valor del control deslizante se almacena bajo `PcMicGain` (la misma configuración que se usa cuando la fuente del micrófono es PC) y no se escribe en la propiedad `mic_level` de la radio mientras RADE está activo. Esto evita que el modo RADE sobrescriba silenciosamente su configuración de hardware de micrófono en la radio.

- El medidor **Level** permanece activo durante RX cuando RADE está habilitado, para que pueda monitorear el nivel de entrada sin transmitir.
- Cuando se desactiva el modo RADE, el control deslizante vuelve a reflejar el `mic_level` de la radio y el medidor Level vuelve a su comportamiento de supresión normal (oculto durante RX a menos que `met_in_rx` esté activado).

## Consejos

- El tono y la panorámica del generador de tono local siempre siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio. No necesita configurarlos por separado para la ruta local.
- Hacer doble clic en el control deslizante **L / R pan (CW)** lo restablece al centro (50).
- El indicador **Compression** lee 0 dB durante RX. Solo muestra un valor distinto de cero cuando el interbloqueo de la radio informa el estado TRANSMITTING y el procesador de voz (**PROC**) está habilitado. Esto evita que se muestren lecturas obsoletas de la cadena TX mientras está recibiendo.
- Con **Breakin** desactivado, las pulsaciones de tecla se ponen en cola y TX debe activarse manualmente con PTT. Con **Breakin** activado (QSK), los bordes de las teclas activan TX directamente y `break_in_delay` controla el tiempo de retención del relé. Ningún sobreenvolvente automático de PTT anula este comportamiento.
- El control deslizante **Delay (CW)** ahora actualiza su valor almacenado en caché inmediatamente cuando se arrastra, evitando que la radio devuelva el control deslizante a su posición anterior (v0.9.8, #2428).
- El indicador ALC en ambos paneles lee la misma fuente del medidor, por lo que puede monitorear ALC independientemente de qué subpanel esté visible.

## Solución de problemas

- **No se escucha ningún tono a pesar de que Sidetone está activado** — Confirme que el control deslizante **Sidetone volume** esté por encima de 0. También verifique que su dispositivo de salida de audio del sistema esté configurado correctamente, ya que el generador local usa la ruta de audio local.
- **El botón Sidetone no está visible** — El subpanel CW solo aparece cuando el slice activo está en modo CW. Cambie el slice activo a CW en la radio; el panel del applet cambiará automáticamente.
- **El tono no coincide con la expectativa** — El tono sigue la configuración de `cw_pitch` de la radio. Ajústelo usando **Pitch < / >** en el applet, que actualiza la configuración de la radio en pasos de 10 Hz.
- **El indicador de compresión siempre muestra 0** — Esto es esperado durante RX. El indicador está bloqueado por el estado TRANSMITTING del interbloqueo de la radio. Mostrará compresión solo mientras esté transmitiendo con **PROC** habilitado.
- **Breakin OFF no mantiene TX entre caracteres** — Con **Breakin** desactivado, AetherSDR ya no aplica un sobreenvolvente automático de PTT. Active PTT manualmente antes de enviar y suéltelo cuando termine.
- **El control deslizante Mic gain no tiene efecto en el modo RADE** — En el modo RADE, el control deslizante establece la ganancia local almacenada como `PcMicGain` y no envía comandos a la radio. Ajuste el control deslizante al nivel deseado; surte efecto en la ruta de audio RADE local.
- **El control deslizante Delay vuelve a su posición después de arrastrarlo** — Este error se corrigió en v0.9.8 (#2428). Actualice a la última versión si experimenta esto.
- **El indicador ALC muestra valores inesperados** — Ambos indicadores ALC ahora leen de MeterModel::swAlcChanged (pico SSB post-ALC por software en dBFS). Si ve lecturas fuera del rango de -20 a 0 dBFS, los valores se limitan a los límites del indicador. La ruta anterior HWALC (tensión RCA) se ha eliminado.

## Relacionado

- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Panorámica del tono lateral CW a la izquierda o derecha](pan-the-cw-sidetone-left-or-right.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Establecer la velocidad de manipulación CW en PPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)

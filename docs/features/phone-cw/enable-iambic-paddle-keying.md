# Applet Phone/CW

## Resumen

El applet Phone/CW es un panel de transmisión sensible al modo que muestra los controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a controles CW (retardo, velocidad, tono lateral, iámbico, tono) cuando la porción activa está en modo CW. En v0.9.8, las cuatro etiquetas de valor CW (Retardo, Velocidad, Volumen de tono lateral, Tono) son ahora widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente (paridad SmartSDR). El único conmutador de tono lateral y el deslizador de volumen controlan tanto el monitor alimentado por DAX de la radio como el tono lateral de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada; el tono y la panorámica siempre siguen automáticamente la configuración de cw_pitch y mon_pan_cw de la radio (v0.9.1+). En v0.9.7, el indicador de Compresión ahora está controlado por el estado TRANSMITTING del interbloqueo de la radio (no por el flujo del medidor), por lo que marca 0 durante RX; Breakin ahora respeta completamente la configuración break_in de la radio — ya no hay ningún sobre de PTT automático que fuerce TX; el bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

## Controles de Phone

| Control                | Tipo              | Descripción                                                                                                                                | Valor por defecto | Rango                |
|------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------------------|
| Nivel                  | Medidor           | Nivel pico de entrada de micrófono en dBFS. Suprimido a -150 cuando met_in_rx está desactivado y no se transmite.                         | —                 | -40 a +10 dBFS (rojo > 0) |
| Compresión             | Medidor           | Cantidad de compresión de voz en dB (relleno invertido). Controlado por el estado TRANSMITTING del interbloqueo de la radio y la habilitación del procesador de voz; marca 0 dB durante RX. | —                 | -25 a 0 dB           |
| Perfil de micrófono    | Cuadro combinado  | Carga un perfil de procesamiento de micrófono con nombre; llama a TransmitModel::loadMicProfile.                                          | —                 | Poblado desde micProfileList() de la radio |
| Fuente de micrófono    | Cuadro combinado  | Selecciona la fuente de entrada de micrófono; llama a TransmitModel::setMicSelection.                                                     | —                 | MIC, BAL, LINE, ACC, PC (más las de micInputList()) |
| Ganancia de micrófono  | Deslizador        | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local de PcMicGain (la radio informa mic_level=0 cuando la fuente=PC). | 50                | 0-100                |
| +ACC                   | Botón de conmutación | Habilita la mezcla de entrada de micrófono auxiliar; llama a TransmitModel::setMicAcc.                                                | —                 | —                    |
| PROC                   | Botón de conmutación | Conmuta el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable.                                                        | —                 | —                    |
| NOR/DX/DX+             | Deslizador        | Nivel del procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel.                                               | 0                 | 0 (NOR), 1 (DX), 2 (DX+) |
| DAX                    | Botón de conmutación | Habilita DAX como fuente de audio TX; llama a TransmitModel::setDax.                                                                | —                 | —                    |
| MON                    | Botón de conmutación | Habilita el monitor de tono lateral TX; llama a TransmitModel::setSbMonitor.                                                         | —                 | —                    |
| Volumen del monitor    | Deslizador        | Ajusta el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb.                                                  | —                 | 0-100                |

## Controles de CW

| Control                      | Tipo                      | Descripción                                                                                                                                                                                         | Valor por defecto | Rango                |
|------------------------------|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|----------------------|
| ALC                          | Medidor                   | Lectura del control automático de nivel.                                                                                                                                                           | —                 | 0-100 (rojo > 80)   |
| Retardo (CW)                 | Deslizador + QLineEdit    | Establece el retardo de Break-in CW. Haga clic en el valor y escriba un número directamente (0–2000). Llama a TransmitModel::setCwDelay. En v0.9.8, setCwDelay almacena en caché el valor inmediatamente. | 500               | 0-2000 ms (paso 10) |
| Velocidad (CW)               | Deslizador + QLineEdit    | Establece la velocidad de manipulación CW. Haga clic en el valor y escriba un número directamente (5–100). Llama a TransmitModel::setCwSpeed.                                                   | 20                | 5-100 WPM            |
| Tono lateral                 | Botón de conmutación      | Conmuta el monitor de tono lateral CW. También habilita/deshabilita el CwSidetoneGenerator de baja latencia del lado del cliente de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el tono lateral local de PortAudio son controlados por este único botón. El tono y la panorámica siguen automáticamente cw_pitch y mon_pan_cw de la radio. | —                 | —                    |
| Volumen de tono lateral      | Deslizador + QLineEdit    | Establece el volumen del monitor CW. Un solo deslizador controla tanto el volumen del lado de la radio (mon_gain_cw) como el del tono lateral del lado del cliente. Haga clic en el valor y escriba un número directamente (0–100). | 50                | 0-100                |
| Panorámica L / R (CW)       | Deslizador                | Establece la panorámica estéreo del monitor CW. También aplica panorámica de potencia constante al generador de tono lateral local (v0.9.1+). Haga doble clic para volver a centrar en 50 (centro). | 50                | 0-100                |
| Breakin                      | Botón de conmutación      | Conmuta el break-in completo (QSK). En v0.9.7, respeta completamente la configuración break_in de la radio: con Breakin activado, los bordes de las teclas activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las teclas se ponen en cola y el operador activa PTT manualmente. | —                 | —                    |
| Iámbico                      | Botón de conmutación      | Conmuta el manipulador de paletas iámbico; llama a TransmitModel::setCwIambic.                                                                                                                    | —                 | —                    |
| Tono < / >                   | QLineEdit con botones      | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para avanzar en pasos de 10 Hz. Llama a TransmitModel::setCwPitch (v0.9.8, #2429).               | 600               | 100-6000 Hz (paso 10) |

## Indicadores

| Indicador             | Estados                  | Significado                              |
|-----------------------|--------------------------|------------------------------------------|
| Indicador de nivel    | -40 .. +10 dBFS          | Nivel pico del micrófono.                |
| Indicador de compresión| -25 .. 0 dB              | Cantidad de compresión de voz (relleno invertido). |
| Indicador de ALC      | 0..100                   | Control automático de nivel (subpanel CW). |

# Habilitar la manipulación con paleta iámbica

Habilite el manipulador iámbico integrado de la radio para que una paleta de doble palanca conectada a la FLEX-8600 manipule CW usando el modo iámbico. Esto le permite configurar la velocidad de manipulación y el comportamiento de break-in desde AetherSDR.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- La porción activa debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel CW cuando una porción CW está activa.
- Una paleta de doble palanca debe estar físicamente conectada al conector de llave de la FLEX-8600.

## Pasos

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya está visible, omita este paso.
2. Confirme que se muestra el subpanel CW. Si la porción activa está en modo CW, el applet muestra los controles CW que incluyen **Iámbico**, **Velocidad (CW)**, **Retardo (CW)** y **Breakin**.
3. Haga clic en **Iámbico** para habilitar el manipulador de paletas iámbico. El botón se resalta cuando está activo.

## Consejos

- Para obtener retroalimentación de tono lateral de baja latencia al usar una paleta, habilite **Tono lateral** en el subpanel CW. El único botón **Tono lateral** y el deslizador **Volumen de tono lateral** controlan tanto el monitor alimentado por DAX de la radio como el tono lateral de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panorámica siguen automáticamente la configuración de `cw_pitch` y `mon_pan_cw` de la radio. En Windows, el flujo de tono lateral ahora comienza inmediatamente al conectar (v0.9.3, corrección #2105). Consulte [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md).
- Ajuste **Velocidad (CW)** antes de habilitar **Iámbico** para evitar enviar a una velocidad inesperada. Consulte [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md).
- Si desea una operación QSK completa, habilite también **Breakin**. En v0.9.7, **Breakin** se respeta completamente: con **Breakin** activado, los bordes de las teclas activan TX y `break_in_delay` mantiene el relé; con **Breakin** desactivado, las teclas se ponen en cola y usted activa PTT manualmente. El sobre de PTT automático anterior que enmascaraba **Breakin** desactivado y eliminaba el tiempo de espera QSK se ha eliminado. Para establecer un tiempo de espera en su lugar, desactive **Breakin** y configure **Retardo (CW)** en un valor distinto de cero. Consulte [Establecer el retardo de break-in CW](set-cw-break-in-delay.md).
- En v0.9.8, los valores de Retardo (CW), Velocidad (CW), Volumen de tono lateral y Tono ahora son widgets QLineEdit editables. Haga clic en cualquier valor y escriba un número directamente. Los deslizadores se actualizan automáticamente cuando termina de editar, y viceversa.

## Solución de problemas

- **El subpanel CW no es visible, solo aparecen los controles de Phone** — La porción activa no está en un modo CW. Cambie el modo de la porción a CW o CW-USB/CW-LSB en la radio o en AetherSDR; el applet cambiará automáticamente.
- **El botón Iámbico está presente pero la paleta no manipula** — Verifique que la paleta esté conectada al conector de llave correcto en la FLEX-8600. El manipulador iámbico es una función del lado de la radio; AetherSDR envía el comando de habilitación, pero la manipulación física depende de la conexión de hardware.
- **El indicador de Nivel no aparece después de conectar con la fuente de micrófono configurada en PC** — En v0.9.3, el indicador de Nivel aparece inmediatamente al conectar cuando la fuente de micrófono es PC (#2086). Si falta el indicador, confirme que la fuente de micrófono esté configurada en **PC** en el selector **Fuente de micrófono** y que esté ejecutando v0.9.3 o posterior. Cuando la fuente es PC, el medidor usa la medición del lado del cliente y no es suprimido por la configuración `met_in_rx`. La misma medición del lado del cliente se aplica cuando el modo RADE está activo, y el indicador de Nivel permanece visible durante RX en ese caso.
- **El indicador de Compresión muestra una lectura distinta de cero durante la recepción** — En v0.9.7, el indicador de Compresión está controlado por el estado TRANSMITTING del interbloqueo de la radio. Marca 0 dB durante RX. Si ve una lectura distinta de cero en reposo, confirme que está ejecutando v0.9.7 o posterior.
- **Breakin OFF no pone las teclas en cola correctamente; PTT se cae inesperadamente** — El sobre de PTT automático que anteriormente anulaba la configuración **Breakin** se eliminó en v0.9.7. Si observa este comportamiento, confirme que está ejecutando v0.9.7 o posterior y que la configuración `break_in` de la radio coincide con el estado del botón **Breakin** en el applet.

## Relacionado

- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Cambiar el tono CW / frecuencia de tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)

# Applet de Phone/CW

## Descripción general

El applet de Phone/CW es un panel de transmisión sensible al modo que muestra controles de micrófono, procesador y monitor en modos de voz, y cambia automáticamente a controles de CW (retardo, velocidad, sidetone, iámbico, tono) cuando el slice activo está en modo CW. En v0.9.8, las cuatro etiquetas de valor de CW (Delay, Speed, Sidetone Volume, Pitch) ahora son widgets QLineEdit con QIntValidator: haga clic en cualquier valor y escriba un número directamente (paridad con SmartSDR). El único conmutador de Sidetone y el deslizador de volumen controlan tanto el monitor alimentado por DAX de la radio como el sidetone local de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) de forma sincronizada: el tono y la panorámica siguen automáticamente la configuración de `cw_pitch` y `mon_pan_cw` de la radio (v0.9.1+). En v0.9.7, el indicador de Compression ahora está controlado por el estado TRANSMITTING del interlock de la radio (no por el flujo del medidor), por lo que marca 0 durante RX; Breakin ahora respeta completamente la configuración `break_in` de la radio — ya no se fuerza ninguna envolvente de PTT automática que active TX; el bus de sidetone se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo). En v26.5.1, el medidor ALC en ambos subpaneles de Phone y CW se recableó de HWALC (voltaje RCA) al medidor de ALC de software (MeterModel::swAlcChanged, pico dBFS posterior al medidor SSB, #2552) y se agregó un nuevo indicador ALC en el panel CW (idéntico al indicador ALC del panel Phone).

## Controles de Phone

| Control         | Tipo                                                                                                                                    | Descripción                                                                                                                                                              |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Level           | Medidor                                                                                                                                 | Nivel pico de entrada del micrófono en dBFS. Suprimido a -150 cuando met_in_rx está desactivado y no se está transmitiendo.                                              |
| Compression     | Medidor                                                                                                                                 | Cantidad de compresión de voz en dB (relleno invertido). Controlado por el estado TRANSMITTING del interlock de la radio y la habilitación del procesador de voz; marca 0 dB durante RX. |
| Mic profile     | Combo box                                                                                                                               | Carga un perfil de procesamiento de micrófono nombrado; llama a TransmitModel::loadMicProfile.                                                                            |
| Mic source      | Combo box                                                                                                                               | Selecciona la fuente de entrada del micrófono; llama a TransmitModel::setMicSelection.                                                                                    |
| Mic gain        | Deslizador                                                                                                                              | Ajusta el nivel de entrada del micrófono. Para la fuente 'PC' usa la persistencia local PcMicGain (la radio reporta mic_level=0 cuando la fuente es PC).                 |
| +ACC            | Botón de conmutación                                                                                                                    | Habilita la mezcla de entrada del micrófono auxiliar; llama a TransmitModel::setMicAcc.                                                                                  |
| PROC            | Botón de conmutación                                                                                                                    | Conmuta el procesador de voz; llama a TransmitModel::setSpeechProcessorEnable.                                                                                            |
| NOR/DX/DX+      | Deslizador                                                                                                                              | Nivel del procesador de tres posiciones; llama a TransmitModel::setSpeechProcessorLevel.                                                                                  |
| DAX             | Botón de conmutación                                                                                                                    | Habilita DAX como fuente de audio de TX; llama a TransmitModel::setDax.                                                                                                   |
| MON             | Botón de conmutación                                                                                                                    | Habilita el monitor de sidetone de TX; llama a TransmitModel::setSbMonitor.                                                                                               |
| Monitor volume  | Deslizador                                                                                                                              | Ajusta el volumen del monitor de banda lateral; llama a TransmitModel::setMonGainSb.                                                                                     |
| ALC (panel Phone) | Medidor                                                                                                                               | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Recableado de HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel CW. |

## Controles de CW

| Control                  | Tipo                 | Descripción                                                                                                                                                                         | Valor predeterminado | Rango                |
|--------------------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|----------------------|
| ALC (panel CW)           | Medidor              | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Usa el modo HGauge::setFillFromRight: vacío a -20 dBFS, lleno a 0 dBFS. Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. | —                    | -20 a 0 dBFS (rojo > -3) |
| Delay (CW)               | Deslizador + QLineEdit | Ajusta el retardo de break-in de CW. Haga clic en el valor y escriba un número directamente (0–2000). Llama a TransmitModel::setCwDelay. En v0.9.8, setCwDelay almacena en caché el valor inmediatamente. | 500                  | 0-2000 ms (paso 10)  |
| Speed (CW)               | Deslizador + QLineEdit | Ajusta la velocidad de manipulación de CW. Haga clic en el valor y escriba un número directamente (5–100). Llama a TransmitModel::setCwSpeed.                                      | 20                   | 5-100 WPM            |
| Sidetone                 | Botón de conmutación  | Conmuta el monitor de sidetone de CW. También habilita/deshabilita el CwSidetoneGenerator local de baja latencia de forma sincronizada (v0.9.1+). Tanto el monitor alimentado por DAX de la radio como el sidetone local de PortAudio son controlados por este único botón. El tono y la panorámica siguen automáticamente `cw_pitch` y `mon_pan_cw` de la radio. | —                    | —                    |
| Sidetone volume          | Deslizador + QLineEdit | Ajusta el volumen del monitor de CW. Un solo deslizador controla tanto el volumen del lado de la radio (mon_gain_cw) como el del sidetone local. Haga clic en el valor y escriba un número directamente (0–100). | 50                   | 0-100                |
| L / R pan (CW)           | Deslizador            | Ajusta la panorámica estéreo del monitor de CW. También aplica panorámica de potencia constante al generador de sidetone local (v0.9.1+). Haga doble clic para centrar en 50.       | 50                   | 0-100                |
| Breakin                  | Botón de conmutación  | Conmuta el break-in completo (QSK). En v0.9.7, respeta completamente la configuración `break_in` de la radio: con Breakin activado, los bordes de la clave activan TX y break_in_delay mantiene el relé; con Breakin desactivado, las claves se ponen en cola y el operador activa PTT manualmente. | —                    | —                    |
| Iambic                   | Botón de conmutación  | Conmuta el manipulador de paletas iámbico; llama a TransmitModel::setCwIambic.                                                                                                      | —                    | —                    |
| Pitch < / >              | QLineEdit con botones | QLineEdit con botones < / > (CwTriBtn). Escriba un valor (100–6000) o haga clic en los botones para aumentar/disminuir en pasos de 10 Hz. Llama a TransmitModel::setCwPitch (v0.9.8, #2429). | 600                  | 100-6000 Hz (paso 10) |

## Indicadores

| Indicador               | Estados                | Significado                                                   |
|-------------------------|------------------------|---------------------------------------------------------------|
| Level gauge             | -40 .. +10 dBFS        | Nivel pico del micrófono.                                     |
| Compression gauge       | -25 .. 0 dB            | Cantidad de compresión de voz (relleno invertido).            |
| ALC gauge (Phone)       | -20 .. 0 dBFS (relleno desde la derecha) | Control automático de nivel — pico SSB posterior al ALC de software, leído de MeterModel::swAlcChanged. |
| ALC gauge (CW)          | -20 .. 0 dBFS (relleno desde la derecha) | Reflejo del indicador ALC del panel Phone, con la misma escala. |

# Habilitar la manipulación con paletas iámbicas

Habilite el manipulador iámbico incorporado de la radio para que una paleta de doble palanca conectada a la FLEX-8600 manipule CW en modo iámbico. Esto le permite ajustar la velocidad de manipulación y el comportamiento de break-in desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al subpanel CW cuando un slice CW está activo.
- Una paleta de doble palanca debe estar físicamente conectada al conector de clave de la FLEX-8600.

## Pasos

1. Haga clic en el botón **P/CW** en la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya es visible, omita este paso.
2. Confirme que se muestra el subpanel CW. Si el slice activo está en modo CW, el applet muestra los controles de CW, incluidos **Iambic**, **Speed (CW)**, **Delay (CW)** y **Breakin**.
3. Haga clic en **Iambic** para habilitar el manipulador de paletas iámbico. El botón se resalta cuando está activo.

## Consejos

- Para una retroalimentación de sidetone de baja latencia al usar una paleta, habilite **Sidetone** en el subpanel CW. El único botón **Sidetone** y el deslizador **Sidetone volume** controlan tanto el monitor alimentado por DAX de la radio como el sidetone local de baja latencia (aproximadamente 10 ms de latencia) de forma sincronizada. El tono y la panorámica siguen automáticamente la configuración `cw_pitch` y `mon_pan_cw` de la radio. En Windows, el flujo de sidetone ahora se inicia inmediatamente al conectar (v0.9.3, corrección #2105). Consulte [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md).
- Ajuste **Speed (CW)** antes de habilitar **Iambic** para evitar enviar a una velocidad inesperada. Consulte [Establecer la velocidad de manipulación de CW en WPM](set-cw-keying-speed-in-wpm.md).
- Si desea una operación QSK completa, habilite también **Breakin**. En v0.9.7, **Breakin** se respeta completamente: con **Breakin** activado, los bordes de la clave activan TX y `break_in_delay` mantiene el relé; con **Breakin** desactivado, las claves se ponen en cola y usted activa PTT manualmente. Se ha eliminado la envolvente de PTT automática anterior que enmascaraba **Breakin** desactivado y eliminaba el tiempo de retención de QSK. Para establecer un tiempo de retención en su lugar, desactive **Breakin** y configure **Delay (CW)** en un valor distinto de cero. Consulte [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md).
- En v0.9.8, los valores de Delay (CW), Speed (CW), Sidetone volume y Pitch ahora son widgets QLineEdit editables. Haga clic en cualquier valor y escriba un número directamente. Los deslizadores se actualizan automáticamente cuando termina de editar, y viceversa.

## Solución de problemas

- **El subpanel CW no es visible, solo aparecen los controles de Phone** — El slice activo no está en un modo CW. Cambie el modo del slice a CW o CW-USB/CW-LSB en la radio o en AetherSDR; el applet cambiará automáticamente.
- **El botón Iambic está presente pero la paleta no manipula** — Verifique que la paleta esté conectada al conector de clave correcto en la FLEX-8600. El manipulador iámbico es una función del lado de la radio; AetherSDR envía el comando de habilitación, pero la manipulación física depende de la conexión de hardware.
- **El indicador Level no aparece después de conectar con la fuente de micrófono configurada en PC** — En v0.9.3, el indicador Level aparece inmediatamente al conectar cuando la fuente de micrófono es PC (#2086). Si falta el indicador, confirme que la fuente de micrófono esté configurada en **PC** en el selector **Mic source** y que esté ejecutando v0.9.3 o posterior. Cuando la fuente es PC, el medidor usa la medición del lado del cliente y no es suprimido por la configuración `met_in_rx`. La misma medición del lado del cliente se aplica cuando el modo RADE está activo, y el indicador Level permanece visible durante RX en ese caso.
- **El indicador Compression muestra un valor distinto de cero durante la recepción** — En v0.9.7, el indicador Compression está controlado por el estado TRANSMITTING del interlock de la radio. Marca 0 dB durante RX. Si ve un valor distinto de cero en reposo, confirme que está ejecutando v0.9.7 o posterior.
- **Breakin OFF no pone las claves en cola correctamente; PTT cae inesperadamente** — La envolvente de PTT automática que anteriormente anulaba la configuración **Breakin** se eliminó en v0.9.7. Si observa este comportamiento, confirme que está ejecutando v0.9.7 o posterior y que la configuración `break_in` de la radio coincide con el estado del botón **Breakin** en el applet.
- **El indicador ALC muestra valores sin sentido o no responde** — En v26.5.1, el medidor ALC se recableó de HWALC (voltaje RCA) al medidor de ALC de software (MeterModel::swAlcChanged). Si ve lecturas antiguas y sin sentido, confirme que está ejecutando v26.5.1 o posterior. Un nuevo indicador ALC en el panel CW coincide con el indicador del panel Phone; ambos leen de la misma fuente.

## Relacionado

- [Establecer la velocidad de manipulación de CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Cambiar el tono / frecuencia de sidetone de CW](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)

# Editar retardo de CW / velocidad / volumen de tono local / tono escribiendo un valor directamente

Escriba un número preciso directamente en cualquiera de los cuatro campos de valor de CW (Retardo, Velocidad, Volumen de tono local, Tono) en lugar de arrastrar un control deslizante o hacer clic en los botones de paso. Esto coincide con el comportamiento nativo de SmartSDR y es útil cuando ya conoce el valor exacto que desea.

## Antes de comenzar

- Asegúrese de que el slice activo esté en modo CW (el applet Phone/CW cambia automáticamente a los controles de CW).

## Pasos

1. Haga clic en el botón **P/CW** de la barra de herramientas lateral derecha si el applet Phone/CW no está visible.
2. Localice el control de CW que desea editar: **Delay**, **Speed**, **Sidetone volume** o **Pitch**. Cada uno está junto a su control deslizante correspondiente.
3. Haga clic dentro del campo numérico (un QLineEdit). El campo mostrará un cursor de texto.
4. Escriba el valor deseado usando su teclado.
5. Presione **Enter** o haga clic en otro lugar para aplicar el valor.

## Función de cada control

| Control             | Valor predeterminado | Rango válido                                                                                                             |
|---------------------|----------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Delay**           | 500                  | 0–2000 ms (paso 10)                                                                                                      |
| **Speed**           | 20                   | 5–100 WPM                                                                                                                |
| **Sidetone volume** | 50                   | 0–100                                                                                                                    |
| **Pitch**           | 600                  | 100–6000 Hz (paso 10)                                                                                                    |
| **ALC (panel Phone)** | —                  | Muestra la lectura de control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. Reconectado desde HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel de CW. |
| **ALC (panel CW)**    | —                  | Refleja el indicador ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. |

## Vista general del applet Phone/CW

El applet Phone/CW es un panel de transmisión que reconoce el modo. Muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono local, iambic, tono) cuando el slice activo está en modo CW. Los indicadores ALC aparecen tanto en los subpaneles de Phone como de CW, ambos alimentados por el medidor ALC por software (MeterModel::swAlcChanged, pico post-SSBMeter en dBFS, #2552), reemplazando la ruta anterior HWALC (voltaje RCA) que producía lecturas sin sentido.

El medidor de Compresión está controlado por el estado TRANSMITTING del bloqueo de la radio (lee 0 durante RX). Breakin respeta completamente la configuración break_in de la radio — no hay un sobre de PTT automático que fuerce TX. El bus de tono local se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

## Indicadores ALC (v26.5.1)

Tanto el panel Phone como el panel CW contienen un indicador ALC. Estos indicadores son espejos idénticos que leen de la misma fuente MeterModel::swAlcChanged. Esto asegura que los operadores de SSB que observan la ganancia del micrófono vean el mismo indicador que los operadores de CW usan para verificar la forma correcta del sobre de keying.

- **Rango**: -20 dBFS (vacío) a 0 dBFS (lleno)
- **Zona roja**: > -3 dBFS
- **Dirección de llenado**: De derecha a izquierda (vacío a -20, se llena hacia la izquierda hasta 0)
- **Marcas de escala**: -20, -15, -10, -5, 0 dBFS

## Controles del panel Phone

| Control           | Tipo         | Valor predeterminado | Rango válido                  | Comportamiento                                                              |
|-------------------|--------------|----------------------|-------------------------------|-----------------------------------------------------------------------------|
| **Level**         | Medidor      | —                    | -40 a +10 dBFS (rojo > 0)     | Muestra el nivel pico de entrada del micrófono en dBFS. Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo. |
| **Compression**   | Medidor      | —                    | -25 a 0 dB (llenado invertido)| Muestra la cantidad de compresión de voz en dB. Controlado por el estado TRANSMITTING del bloqueo de la radio y la activación del procesador de voz. |
| **ALC**           | Medidor      | —                    | -20 a 0 dBFS (rojo > -3)      | Muestra el control automático de nivel desde MeterModel::swAlcChanged. Se llena de derecha a izquierda. |
| **Mic profile**   | Cuadro combinado| —                  | Poblado desde la radio         | Carga el perfil de procesamiento de micrófono nombrado.                      |
| **Mic source**    | Cuadro combinado| —                  | MIC, BAL, LINE, ACC, PC       | Selecciona la fuente de entrada del micrófono.                              |
| **Mic gain**      | Control deslizante | 50              | 0-100                         | Ajusta el nivel de entrada del micrófono. Para fuente PC usa la persistencia local PcMicGain. |
| **+ACC**          | Botón de alternancia| —                | —                             | Activa la mezcla de entrada de micrófono accesorio.                          |
| **PROC**          | Botón de alternancia| —                | —                             | Activa o desactiva el procesador de voz.                                    |
| **NOR/DX/DX+**    | Control deslizante | 0                | 0 (NOR), 1 (DX), 2 (DX+)     | Nivel del procesador de tres posiciones.                                    |
| **DAX**           | Botón de alternancia| —                | —                             | Activa DAX como fuente de audio TX.                                         |
| **MON**           | Botón de alternancia| —                | —                             | Activa el monitor de tono local TX.                                         |
| **Monitor volume**| Control deslizante | —                | 0-100                         | Establece el volumen del monitor de banda lateral.                          |

## Controles del panel CW

| Control              | Tipo             | Valor predeterminado | Rango válido               | Comportamiento                                                                   |
|----------------------|------------------|----------------------|----------------------------|----------------------------------------------------------------------------------|
| **ALC**              | Medidor          | —                    | -20 a 0 dBFS (rojo > -3)   | Refleja el indicador ALC del panel Phone. Se llena de derecha a izquierda.      |
| **Delay**            | Deslizante + edición | 500              | 0-2000 ms (paso 10)        | Establece el retardo de break-in en CW. Escriba valores 0-2000 directamente.    |
| **Speed**            | Deslizante + edición | 20               | 5-100 WPM                  | Establece la velocidad de keying CW. Escriba valores 5-100 directamente.        |
| **Sidetone**         | Botón de alternancia | —                | —                          | Activa o desactiva el monitor de tono local CW. Controla tanto el monitor alimentado por DAX de la radio como el generador local de baja latencia CwSidetoneGenerator de forma sincronizada. |
| **Sidetone volume**  | Deslizante + edición | 50               | 0-100                      | Establece el volumen del monitor CW. Controla tanto los volúmenes del lado de la radio como del tono local. Escriba valores 0-100 directamente. |
| **L / R pan (CW)**   | Control deslizante | 50                | 0-100                      | Establece la panorámica estéreo del monitor CW. Doble clic centra en 50.        |
| **Breakin**          | Botón de alternancia | —                | —                          | Activa o desactiva el break-in completo (QSK). Las rutas de teclado/MIDI CW respetan completamente esta configuración. |
| **Iambic**           | Botón de alternancia | —                | —                          | Activa o desactiva el keyer de paletas iambic.                                    |
| **Pitch < / >**      | Edición + botones | 600               | 100-6000 Hz (paso 10)      | QLineEdit con botones < / >. Escriba valores 100-6000 o haga clic en los botones para avanzar en pasos de 10 Hz. |

## Solución de problemas

- **El valor escrito vuelve al valor anterior** — Es posible que la radio haya rechazado el valor. Asegúrese de que su entrada esté dentro del rango válido mostrado arriba. Para valores de Delay, la emisión de la radio ya no devuelve el control deslizante en v0.9.8 (#2428).

## Relacionados

- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
- [Enable the low-latency CW sidetone (Sidetone button drives both radio and local path)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)

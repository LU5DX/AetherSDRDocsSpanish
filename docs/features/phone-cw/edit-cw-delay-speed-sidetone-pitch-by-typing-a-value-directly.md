# Indicadores ALC (v26.5.1)

Tanto el panel de Phone como el de CW contienen un indicador ALC. Estos indicadores son espejos idénticos que leen de la misma fuente `MeterModel::swAlcChanged`. Esto asegura que los operadores de SSB que observan la ganancia del micrófono vean el mismo indicador que los operadores de CW usan para verificar una envolvente de clave limpia.

- **Rango**: -20 dBFS (vacío) a 0 dBFS (lleno)
- **Zona roja**: > -3 dBFS
- **Dirección de llenado**: De derecha a izquierda (vacío en -20, se llena hacia la izquierda hasta 0)
- **Marcas de escala**: -20, -15, -10, -5, 0 dBFS
- **Estado inicial**: Ambos indicadores comienzan en -20 dBFS al construir el applet (v26.5.3).

# Editar Retardo CW / Velocidad / Tono lateral / Tono escribiendo un valor directamente

Escriba un número preciso directamente en cualquiera de los cuatro campos de valor CW (Retardo, Velocidad, Volumen del tono lateral, Tono) en lugar de arrastrar un control deslizante o hacer clic en los botones de paso. Esto coincide con el comportamiento nativo de SmartSDR y es útil cuando ya conoce el valor exacto que desea.

## Antes de comenzar

- Asegúrese de que la franja activa esté en modo CW (el applet Phone/CW cambia automáticamente a los controles CW).

## Pasos

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha si el applet Phone/CW no está visible.
2. Localice el control CW que desea editar: **Retardo**, **Velocidad**, **Volumen del tono lateral** o **Tono**. Cada uno está junto a su control deslizante correspondiente.
3. Haga clic dentro del campo numérico (un QLineEdit). El campo mostrará un cursor de texto.
4. Escriba el valor deseado usando su teclado.
5. Presione **Enter** o haga clic en otro lugar para aplicar el valor.

## Qué hace cada control

| Control              | Por defecto | Rango válido                                                                                                             |
|----------------------|-------------|--------------------------------------------------------------------------------------------------------------------------|
| **Retardo**          | 500         | 0–2000 ms (paso 10)                                                                                                      |
| **Velocidad**        | 20          | 5–100 WPM                                                                                                                |
| **Volumen tono lateral** | 50      | 0–100                                                                                                                    |
| **Tono**             | 600         | 100–6000 Hz (paso 10)                                                                                                    |
| **ALC (panel Phone)** | —          | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC por software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS. Reconectado desde HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). Es reflejado por un indicador idéntico en el subpanel CW. Ambos indicadores se inicializan en -20 dBFS en v26.5.3. |
| **ALC (panel CW)**   | —           | Refleja el indicador ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. |

## Resumen del applet Phone/CW

El applet Phone/CW es un panel de transmisión que reconoce el modo. Muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles CW (retardo, velocidad, tono lateral, iámbico, tono) cuando la franja activa está en modo CW. Los indicadores ALC aparecen tanto en los subpaneles Phone como CW, ambos impulsados por el medidor ALC por software (MeterModel::swAlcChanged, pico posterior a SSBMeter en dBFS, #2552), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin sentido.

El indicador de Compresión está controlado por el estado de TRANSMISIÓN del interlock del radio (lee 0 durante RX). El break-in respeta completamente la configuración break_in del radio — sin envolvente de auto-PTT que fuerce TX. El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En v26.5.3, el tono lateral CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899).

## Controles del panel Phone

| Control             | Tipo         | Por defecto | Rango válido                    | Comportamiento                                                               |
|---------------------|--------------|-------------|---------------------------------|------------------------------------------------------------------------------|
| **Nivel**           | Medidor      | —           | -40 a +10 dBFS (rojo > 0)       | Muestra el nivel pico de entrada del micrófono en dBFS. Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo (v26.5.3 aplica la supresión inmediatamente en cambios de estado). |
| **Compresión**      | Medidor      | —           | 0 a -25 dB (llenado invertido)  | Muestra la cantidad de compresión de voz en dB. Controlado por el estado de TRANSMISIÓN del interlock del radio y la activación del procesador de voz. v26.5.3: MeterModel COMPPEAK (positivo 0–25 dB) convertido a visualización de medidor negativa. |
| **ALC**             | Medidor      | —           | -20 a 0 dBFS (rojo > -3)        | Muestra el control automático de nivel desde MeterModel::swAlcChanged. Se llena de derecha a izquierda. Inicializado a -20 dBFS en v26.5.3. |
| **Perfil mic**      | Cuadro comb. | —           | Poblado desde el radio          | Carga el perfil de procesamiento de micrófono nombrado.                       |
| **Fuente mic**      | Cuadro comb. | —           | MIC, BAL, LINE, ACC, PC         | Selecciona la fuente de entrada del micrófono.                                |
| **Ganancia mic**    | Deslizador   | 50          | 0-100                           | Ajusta el nivel de entrada del micrófono. Para fuente PC usa la persistencia local PcMicGain. |
| **+ACC**            | Botón altern.| —           | —                               | Activa la mezcla de entrada del micrófono auxiliar.                           |
| **PROC**            | Botón altern.| —           | —                               | Activa/desactiva el procesador de voz.                                        |
| **NOR/DX/DX+**      | Deslizador   | 0           | 0 (NOR), 1 (DX), 2 (DX+)       | Nivel del procesador de tres posiciones.                                      |
| **DAX**             | Botón altern.| —           | —                               | Activa DAX como fuente de audio de TX.                                        |
| **MON**             | Botón altern.| —           | —                               | Activa el monitor de tono lateral de TX.                                      |
| **Volumen monitor** | Deslizador   | —           | 0-100                           | Establece el volumen del monitor de banda lateral.                            |

## Controles del panel CW

| Control                | Tipo            | Por defecto | Rango válido              | Comportamiento                                                                   |
|------------------------|-----------------|-------------|---------------------------|----------------------------------------------------------------------------------|
| **ALC**                | Medidor         | —           | -20 a 0 dBFS (rojo > -3)  | Refleja el indicador ALC del panel Phone. Se llena de derecha a izquierda. Inicializado a -20 dBFS en v26.5.3. |
| **Retardo**            | Deslizador + ed.| 500         | 0-2000 ms (paso 10)       | Establece el retardo del break-in CW. Escriba valores 0-2000 directamente.       |
| **Velocidad**          | Deslizador + ed.| 20          | 5-100 WPM                 | Establece la velocidad de clave CW. Escriba valores 5-100 directamente.          |
| **Tono lateral**       | Botón altern.   | —           | —                         | Activa/desactiva el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX del radio como el generador local CwSidetoneGenerator de baja latencia al unísono. El tono y la panorámica siguen automáticamente cw_pitch y mon_pan_cw del radio. v26.5.3: se enruta a la salida de audio seleccionada por el usuario en lugar de la predeterminada. |
| **Volumen tono lateral**| Deslizador + ed.| 50        | 0-100                     | Establece el volumen del monitor CW. Controla tanto el volumen del lado del radio como el tono lateral local. Escriba valores 0-100 directamente. |
| **Panorámica L / R (CW)**| Deslizador     | 50          | 0-100                     | Establece la panorámica estéreo del monitor CW. Doble clic para centrar en 50. |
| **Breakin**            | Botón altern.   | —           | —                         | Activa/desactiva el break-in completo (QSK). Las rutas de teclado CW/MIDI respetan completamente esta configuración. |
| **Iámbico**            | Botón altern.   | —           | —                         | Activa/desactiva el manipulador de paletas iámbico.                               |
| **Tono < / >**         | Edición + bot.  | 600         | 100-6000 Hz (paso 10)     | QLineEdit con botones < / >. Escriba valores 100-6000 o haga clic en los botones para avanzar en pasos de 10 Hz. |

## Solución de problemas

- **El valor escrito vuelve al valor anterior** — El radio puede haber rechazado el valor. Asegúrese de que su entrada esté dentro del rango válido mostrado arriba. Para valores de Retardo, la emisión del radio ya no devuelve el deslizador en v0.9.8 (#2428).
- **El medidor de nivel permanece en -150 después de detener la transmisión** — En v26.5.3, el medidor de nivel se suprime siempre que se recibe con met_in_rx desactivado. Verifique **Settings > Appearance > Disable level meter during receive** si ve lecturas inesperadas de -150 en RX.
- **El indicador de Compresión muestra valores inesperados** — v26.5.3 cambió la interpretación de COMPPEAK a positivo 0–25 dB; la cara del medidor se invierte a -25–0 dB. Si ve una escala invertida, verifique que está ejecutando v26.5.3 o posterior.

## Relacionado

- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
- [Enable the low-latency CW sidetone (Sidetone button drives both radio and local path)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)

# Applet de Phone/CW

## Resumen

El applet de Phone/CW es un panel de transmisión sensible al modo. Muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono) cuando la porción activa está en modo CW. Los indicadores ALC aparecen tanto en el subpanel de Phone como en el de CW, ambos alimentados por el medidor ALC de software (MeterModel::swAlcChanged, pico SSB posterior al medidor en dBFS, #2552), reemplazando la ruta anterior HWALC (voltaje RCA) que producía lecturas sin sentido.

El indicador de Compresión está bloqueado por el estado de TRANSMISIÓN del interbloqueo de la radio (marca 0 durante RX). El modo break-in respeta completamente la configuración de break_in de la radio (no hay una envolvente de PTT automática que fuerce TX). El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En la v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899).

En la v26.6.1, el applet ahora hereda correctamente la paleta de colores del tema activo. Los deslizadores usan el estilo de deslizador principal (`applyPrimarySliderStyle`) en lugar de valores de color codificados, y los colores de las etiquetas siguen el color de texto secundario del tema (`{{color.text.secondary}}`). El contenedor del panel se estiliza usando `theme::setContainer` para una apariencia consistente en todos los temas.

## Abrir el applet de Phone/CW

1. Haga clic en el botón **P/CW** de la barra lateral derecha.

El applet muestra automáticamente los controles de Phone cuando la porción activa está en un modo de voz (LSB, USB, AM, FM, etc.) y los controles de CW cuando la porción activa está en modo CW o CWL.

## Controles del panel Phone

| Control           | Tipo         | Valor predeterminado | Rango válido                  | Comportamiento                                                               |
|-------------------|--------------|----------------------|--------------------------------|------------------------------------------------------------------------------|
| **Level**         | Medidor      | —                    | -40 a +10 dBFS (rojo > 0)     | Muestra el nivel pico de entrada del micrófono en dBFS. Suprimido a -150 cuando met_in_rx está desactivado y no se transmite (la v26.5.3 aplica la supresión inmediatamente en los cambios de estado). |
| **Compression**   | Medidor      | —                    | 0 a -25 dB (relleno invertido)| Muestra la cantidad de compresión de voz en dB. Bloqueado en el estado TRANSMISIÓN del interbloqueo de la radio y en la habilitación del procesador de voz. v26.5.3: COMPPEAK de MeterModel (positivo 0–25 dB) convertido a visualización de indicador negativo. |
| **ALC**           | Medidor      | —                    | -20 a 0 dBFS (rojo > -3)      | Muestra el control automático de nivel desde MeterModel::swAlcChanged. Se llena de derecha a izquierda. Inicializado a -20 dBFS en la v26.5.3. |
| **Mic profile**   | Cuadro combinado | —                | Poblado desde la radio        | Carga el perfil de procesamiento de micrófono nombrado.                      |
| **Mic source**    | Cuadro combinado | —                | MIC, BAL, LINE, ACC, PC       | Selecciona la fuente de entrada del micrófono.                              |
| **Mic gain**      | Deslizador   | 50                  | 0-100                         | Ajusta el nivel de entrada del micrófono. Para fuente PC usa la persistencia local PcMicGain. |
| **+ACC**          | Botón de alternancia | —            | —                             | Habilita la mezcla de entrada de micrófono accesoria.                       |
| **PROC**          | Botón de alternancia | —            | —                             | Activa o desactiva el procesador de voz.                                     |
| **NOR/DX/DX+**    | Deslizador   | 0                   | 0 (NOR), 1 (DX), 2 (DX+)     | Nivel de procesador de tres posiciones.                                      |
| **DAX**           | Botón de alternancia | —            | —                             | Habilita DAX como fuente de audio TX.                                       |
| **MON**           | Botón de alternancia | —            | —                             | Habilita el monitor de tono lateral TX.                                    |
| **Monitor volume**| Deslizador   | —                   | 0-100                         | Establece el volumen del monitor de banda lateral.                          |

## Controles del panel CW

| Control              | Tipo         | Valor predeterminado | Rango válido               | Comportamiento                                                                   |
|----------------------|--------------|----------------------|-----------------------------|----------------------------------------------------------------------------------|
| **ALC**              | Medidor      | —                    | -20 a 0 dBFS (rojo > -3)    | Refleja el indicador ALC del panel Phone. Se llena de derecha a izquierda. Inicializado a -20 dBFS en la v26.5.3. |
| **Delay**            | Deslizador + edición | 500           | 0-2000 ms (paso 10)         | Establece el retardo de break-in de CW. Escriba valores de 0-2000 directamente. |
| **Speed**            | Deslizador + edición | 20            | 5-100 WPM                   | Establece la velocidad de manipulación CW. Escriba valores de 5-100 directamente.|
| **Sidetone**         | Botón de alternancia | —              | —                           | Activa o desactiva el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX de la radio como el generador local de tono lateral de baja latencia CwSidetoneGenerator de forma sincronizada. El tono y la panorámica siempre siguen automáticamente cw_pitch y mon_pan_cw de la radio. v26.5.3: se enruta a la salida de audio seleccionada por el usuario en lugar de a la predeterminada. |
| **Sidetone volume**  | Deslizador + edición | 50            | 0-100                       | Establece el volumen del monitor CW. Controla tanto los volúmenes del lado de la radio como del tono lateral local. Escriba valores de 0-100 directamente. |
| **L / R pan (CW)**   | Deslizador   | 50                  | 0-100                       | Establece la panorámica estéreo del monitor CW. Haga doble clic para centrar en 50 (centro). |
| **Breakin**          | Botón de alternancia | —              | —                           | Activa o desactiva el break-in completo (QSK). Las rutas de teclado CW/MIDI respetan completamente esta configuración. |
| **Iambic**           | Botón de alternancia | —              | —                           | Activa o desactiva el manipulador de paleta iámbica.                             |
| **Pitch < / >**      | Edición + botones | 600              | 100-6000 Hz (paso 10)       | QLineEdit con botones < / >. Escriba valores de 100-6000 o haga clic en los botones para avanzar en pasos de 10 Hz. |

## Editar valores de CW escribiendo

Puede escribir un número preciso directamente en cualquiera de los cuatro campos de valor CW (Delay, Speed, Sidetone Volume, Pitch) en lugar de arrastrar un deslizador o hacer clic en botones de paso. Esto coincide con el comportamiento nativo de SmartSDR.

### Pasos

1. Abra el applet de Phone/CW con la porción activa en modo CW.
2. Localice el control CW que desea editar: **Delay**, **Speed**, **Sidetone volume** o **Pitch**. Cada uno está junto a su deslizador correspondiente.
3. Haga clic dentro del campo numérico (un QLineEdit). El campo mostrará un cursor de texto.
4. Escriba el valor deseado usando su teclado.
5. Presione **Enter** o haga clic en otro lugar para aplicar el valor.

### Rangos de valores para entrada directa

| Control             | Valor predeterminado | Rango válido                                    |
|---------------------|----------------------|--------------------------------------------------|
| **Delay**           | 500                  | 0-2000 ms (paso 10)                              |
| **Speed**           | 20                   | 5-100 WPM                                        |
| **Sidetone volume** | 50                   | 0-100                                            |
| **Pitch**           | 600                  | 100-6000 Hz (paso 10)                            |

## Indicadores ALC (v26.5.1)

Tanto el panel Phone como el panel CW contienen un indicador ALC. Estos indicadores son espejos idénticos que leen de la misma fuente `MeterModel::swAlcChanged`. Esto garantiza que los operadores de SSB que observan la ganancia del micrófono vean el mismo indicador que los operadores de CW usan para verificar la forma de la envolvente de manipulación limpia.

- **Rango**: -20 dBFS (vacío) a 0 dBFS (lleno)
- **Zona roja**: > -3 dBFS
- **Dirección de llenado**: De derecha a izquierda (vacío en -20, se llena hacia la izquierda hasta 0)
- **Marcas de escala**: -20, -15, -10, -5, 0 dBFS
- **Estado inicial**: Ambos indicadores comienzan en -20 dBFS en la construcción del applet (v26.5.3).

## Solución de problemas

- **El valor escrito vuelve al valor anterior** — La radio puede haber rechazado el valor. Asegúrese de que su entrada esté dentro del rango válido mostrado arriba. Para valores de Delay, la emisión de la radio ya no devuelve el deslizador en la v0.9.8 (#2428).
- **El medidor de nivel permanece en -150 después de dejar de transmitir** — En la v26.5.3, el medidor de nivel se suprime siempre que se recibe con met_in_rx desactivado. Verifique **Settings > Appearance > Disable level meter during receive** si ve lecturas -150 inesperadas en RX.
- **El indicador de Compresión muestra valores inesperados** — La v26.5.3 cambió la interpretación de COMPPEAK a positivo 0–25 dB; la cara del indicador se invierte a -25–0 dB. Si ve una escala invertida, verifique que está ejecutando la v26.5.3 o posterior.
- **Los colores no coinciden con el tema activo** — La v26.6.1 corrigió la herencia del tema para todos los elementos de la interfaz de usuario en este applet. Si los colores aparecen codificados (por ejemplo, azul sobre negro independientemente del tema), verifique que está ejecutando la v26.6.1 o posterior.

## Relacionado

- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Habilitar el tono lateral CW de baja latencia (el botón Sidetone controla tanto la ruta de la radio como la local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)

# Applet de Voz/CW

## Visión general

El applet de Voz/CW es un panel de transmisión sensible al modo. Muestra controles de Voz (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono) cuando la franja activa está en modo CW. Los indicadores ALC aparecen en ambos subpaneles, Voz y CW, ambos impulsados por el medidor ALC de software (MeterModel::swAlcChanged, pico post-SSBMeter en dBFS, #2552), reemplazando la ruta HWALC anterior (tensión RCA) que producía lecturas sin sentido.

El indicador de Compresión está controlado por el estado de TRANSMISIÓN del interbloqueo de la radio (marca 0 durante RX). El break-in respeta completamente la configuración break_in de la radio — no hay ningún sobre de PTT automático que fuerce TX. El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899).

En v26.6.1, el applet ahora hereda correctamente la paleta de colores del tema activo. Los deslizadores usan el estilo de deslizador principal (`applyPrimarySliderStyle`) en lugar de valores de color codificados, y los colores de las etiquetas siguen el color de texto secundario del tema (`{{color.text.secondary}}`). El contenedor del panel se estiliza usando `theme::setContainer` para una apariencia consistente en todos los temas.

En v26.7.4, los cuatro indicadores (Nivel, Compresión y ambos medidores ALC) muestran una lectura numérica exacta cuando pasa el ratón sobre ellos, mostrando valores con un decimal. Cuando la radio es modulada por AetherSDR (modulación de host), el cuadro combinado de fuente de micrófono se bloquea en "PC" y muestra un tooltip que explica que solo la entrada de PC está disponible.

## Abrir el applet de Voz/CW

1. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha.

El applet muestra automáticamente los controles de Voz cuando la franja activa está en un modo de voz (LSB, USB, AM, FM, etc.) y los controles de CW cuando la franja activa está en modo CW o CWL.

## Controles del panel de Voz

| Control                | Tipo           | Predeterminado | Rango válido                  | Comportamiento                                                                                       |
|------------------------|----------------|----------------|-------------------------------|------------------------------------------------------------------------------------------------------|
| **Nivel**              | Medidor        | —              | -40 a +10 dBFS (rojo > 0)     | Muestra el nivel pico de entrada del micrófono en dBFS. Pase el ratón para ver el valor exacto en dB con un decimal. Suprimido a -150 cuando met_in_rx está desactivado y no está transmitiendo (v26.5.3 aplica la supresión inmediatamente en cambios de estado). |
| **Compresión**         | Medidor        | —              | 0 a -25 dB (relleno invertido)| Muestra la cantidad de compresión de voz en dB. Pase el ratón para ver el valor exacto como una "cantidad de compresión" positiva en dB con un decimal. Controlado por el estado de TRANSMISIÓN del interbloqueo de la radio y la activación del procesador de voz. v26.5.3: MeterModel COMPPEAK (positivo 0-25 dB) convertido a visualización de indicador negativo. |
| **ALC**                | Medidor        | —              | -20 a 0 dBFS (rojo > -3)      | Muestra el control automático de nivel desde MeterModel::swAlcChanged. Se llena de derecha a izquierda. Pase el ratón para ver el valor exacto en dBFS con un decimal. Inicializado a -20 dBFS en v26.5.3. |
| **Perfil de mic**      | Cuadro combinado| —              | Poblado desde la radio        | Carga el perfil de procesamiento de micrófono con nombre.                                            |
| **Fuente de mic**      | Cuadro combinado| —              | MIC, BAL, LINE, ACC, PC       | Selecciona la fuente de entrada del micrófono. Bloqueado en "PC" y deshabilitado cuando la modulación de host está activa. |
| **Ganancia de mic**    | Deslizador      | 50             | 0-100                         | Ajusta el nivel de entrada del micrófono. Para la fuente PC usa la persistencia local PcMicGain.    |
| **+ACC**               | Botón de alternar| —              | —                             | Activa la mezcla de entrada de micrófono accesorio.                                                  |
| **PROC**               | Botón de alternar| —              | —                             | Activa o desactiva el procesador de voz.                                                             |
| **NOR/DX/DX+**         | Deslizador      | 0              | 0 (NOR), 1 (DX), 2 (DX+)      | Nivel de procesador de tres posiciones.                                                              |
| **DAX**                | Botón de alternar| —              | —                             | Activa DAX como fuente de audio TX.                                                                  |
| **MON**                | Botón de alternar| —              | —                             | Activa el monitor de tono lateral TX.                                                               |
| **Volumen del monitor**| Deslizador      | —              | 0-100                         | Establece el volumen del monitor de banda lateral.                                                   |

## Controles del panel de CW

| Control                     | Tipo                | Predeterminado | Rango válido               | Comportamiento                                                                                           |
|-----------------------------|---------------------|----------------|----------------------------|----------------------------------------------------------------------------------------------------------|
| **ALC**                     | Medidor             | —              | -20 a 0 dBFS (rojo > -3)   | Refleja el indicador ALC del panel de Voz. Se llena de derecha a izquierda. Pase el ratón para ver el valor exacto en dBFS con un decimal. Inicializado a -20 dBFS en v26.5.3. |
| **Retardo**                 | Deslizador + edición| 500            | 0-2000 ms (paso 10)        | Establece el retardo de break-in de CW. Escriba valores de 0-2000 directamente.                         |
| **Velocidad**               | Deslizador + edición| 20             | 5-100 WPM                  | Establece la velocidad de manipulación CW. Escriba valores de 5-100 directamente.                       |
| **Tono lateral**            | Botón de alternar   | —              | —                          | Activa o desactiva el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX de la radio como el CwSidetoneGenerator local de baja latencia al unísono. El tono y la panoramización siguen automáticamente cw_pitch y mon_pan_cw de la radio. v26.5.3: se enruta a la salida de audio seleccionada por el usuario en lugar de la predeterminada. |
| **Volumen de tono lateral** | Deslizador + edición| 50             | 0-100                      | Establece el volumen del monitor CW. Controla tanto los volúmenes del lado de la radio como del tono lateral local. Escriba valores de 0-100 directamente. |
| **Pan L / R (CW)**          | Deslizador          | 50             | 0-100                      | Establece la panoramización estéreo del monitor CW. Haga doble clic para volver a centrar en 50 (centro).|
| **Breakin**                 | Botón de alternar   | —              | —                          | Activa o desactiva el break-in completo (QSK). Las rutas de teclado/MIDI CW respetan totalmente esta configuración. |
| **Iámbico**                 | Botón de alternar   | —              | —                          | Activa o desactiva el manipulador de paletas iámbico.                                                     |
| **Tono < / >**              | Edición + botones   | 600            | 100-6000 Hz (paso 10)      | QLineEdit con botones < / >. Escriba valores de 100-6000 o haga clic en los botones para avanzar de 10 en 10 Hz. |

## Editar valores de CW escribiendo

Puede escribir un número preciso directamente en cualquiera de los cuatro campos de valor de CW (Retardo, Velocidad, Volumen del tono lateral, Tono) en lugar de arrastrar un deslizador o hacer clic en botones de paso. Esto coincide con el comportamiento nativo de SmartSDR.

### Pasos

1. Abra el applet de Voz/CW con la franja activa en modo CW.
2. Localice el control de CW que desea editar: **Retardo**, **Velocidad**, **Volumen del tono lateral** o **Tono**. Cada uno está junto a su deslizador correspondiente.
3. Haga clic dentro del campo numérico (un QLineEdit). El campo mostrará un cursor de texto.
4. Escriba el valor deseado usando su teclado.
5. Presione **Enter** o haga clic en otro lugar para aplicar el valor.

### Rangos de valor para entrada directa

| Control                     | Predeterminado | Rango válido               |
|-----------------------------|----------------|----------------------------|
| **Retardo**                 | 500            | 0-2000 ms (paso 10)        |
| **Velocidad**               | 20             | 5-100 WPM                  |
| **Volumen del tono lateral**| 50             | 0-100                      |
| **Tono**                    | 600            | 100-6000 Hz (paso 10)      |

## Indicadores ALC (v26.5.1)

Tanto el panel de Voz como el panel de CW contienen un indicador ALC. Estos indicadores son reflejos idénticos que leen de la misma fuente `MeterModel::swAlcChanged`. Esto asegura que los operadores de SSB que observan la ganancia del micrófono vean el mismo indicador que los operadores de CW usan para verificar una forma de envolvente de manipulación limpia.

- **Rango**: -20 dBFS (vacío) a 0 dBFS (lleno)
- **Zona roja**: > -3 dBFS
- **Dirección de llenado**: De derecha a izquierda (vacío en -20, se llena hacia la izquierda hasta 0)
- **Marcas de escala**: -20, -15, -10, -5, 0 dBFS
- **Estado inicial**: Ambos indicadores comienzan en -20 dBFS al construir el applet (v26.5.3).
- **Lectura al pasar el ratón**: Pase el ratón sobre cualquiera de los indicadores ALC para ver el valor exacto en dBFS con un decimal (v26.7.4).

## Lecturas al pasar el ratón sobre indicadores (v26.7.4)

Los cuatro indicadores (Nivel, Compresión y ambos medidores ALC) muestran una lectura numérica exacta cuando pasa el cursor del ratón sobre ellos. Esto permite leer el valor de medición preciso sin tener que calcularlo visualmente contra la escala.

| Indicador                    | Formato al pasar el ratón                              |
|------------------------------|--------------------------------------------------------|
| **Nivel**                    | Muestra el valor como dB con un decimal (ej., "-12.3 dB")|
| **Compresión**               | Muestra el valor como dB positivo con un decimal (ej., "8.5 dB")|
| **ALC (ambos paneles)**      | Muestra el valor como dBFS con un decimal (ej., "-5.7 dBFS")|

## Bloqueo de fuente de micrófono para modulación de host (v26.7.4)

Cuando la radio es modulada por AetherSDR (modulación de host activa), el cuadro combinado **Fuente de mic** se establece automáticamente en "PC" y se deshabilita. El tooltip explica:

> Esta radio es modulada por AetherSDR, por lo que el micrófono de PC es la única entrada. Las otras fuentes son conectores de FlexRadio.

Esto evita seleccionar conectores de micrófono que no existen en una radio modulada por host.

## Solución de problemas

- **El valor escrito vuelve al valor anterior** — La radio puede haber rechazado el valor. Asegúrese de que su entrada esté dentro del rango válido mostrado arriba. Para los valores de Retardo, la emisión de la radio ya no devuelve el deslizador en v0.9.8 (#2428).
- **El medidor de Nivel permanece en -150 después de detener la transmisión** — En v26.5.3, el medidor de nivel se suprime siempre que se recibe con met_in_rx desactivado. Verifique **Settings > Appearance > Disable level meter during receive** si ve lecturas inesperadas de -150 en RX.
- **El indicador de Compresión muestra valores inesperados** — v26.5.3 cambió la interpretación de COMPPEAK a positiva de 0-25 dB; la cara del indicador se invierte a -25-0 dB. Si ve una escala invertida, verifique que está ejecutando v26.5.3 o posterior.
- **Los colores no coinciden con el tema activo** — v26.6.1 corrigió la herencia del tema para todos los elementos de la interfaz de usuario en este applet. Si los colores aparecen codificados (ej., azul sobre negro independientemente del tema), verifique que está ejecutando v26.6.1 o posterior.
- **La lectura al pasar el ratón sobre el indicador no aparece** — Las lecturas al pasar el ratón se agregaron en v26.7.4. Si no las ve, verifique que está ejecutando v26.7.4 o posterior.
- **El cuadro combinado Fuente de mic está atascado en "PC"** — La modulación de host puede estar activa. Pase el ratón sobre el cuadro combinado para ver el tooltip que explica por qué está bloqueado.

## Relacionado

- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
- [Enable the low-latency CW sidetone (Sidetone button drives both radio and local path)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)

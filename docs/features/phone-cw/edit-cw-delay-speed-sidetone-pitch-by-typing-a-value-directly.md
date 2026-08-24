# Applet de Phone/CW

## Descripción general

El applet de Phone/CW es un panel de transmisión consciente del modo. Muestra controles de Phone (micrófono, procesador, monitor) en modos de voz y cambia automáticamente a controles de CW (retardo, velocidad, tono lateral, iámbico, tono) cuando el slice activo está en modo CW. Los medidores de ALC aparecen en ambos subpaneles, Phone y CW, ambos controlados por el medidor ALC de software (MeterModel::swAlcChanged, dBFS posterior al pico del medidor SSB, #2552), reemplazando la ruta anterior de HWALC (voltaje RCA) que producía lecturas sin significado.

El medidor de Compresión está controlado por el estado de TRANSMISIÓN del interlock del radio (lee 0 durante RX). El break-in respeta completamente la configuración break_in del radio — ninguna envolvente de PTT automática fuerza TX. El bus de tono lateral se comparte con los tonos Quindar (mutuamente excluyentes a nivel de modo).

En v26.5.3, el tono lateral de CW ahora se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899).

En v26.6.1, el applet ahora hereda correctamente la paleta de colores del tema activo. Los deslizadores usan el estilo de deslizador primario (`applyPrimarySliderStyle`) en lugar de valores de color codificados, y los colores de las etiquetas siguen el color de texto secundario del tema (`{{color.text.secondary}}`). El contenedor del panel se estiliza usando `theme::setContainer` para una apariencia consistente en todos los temas.

En v26.7.4, los cuatro medidores (Nivel, Compresión y ambos medidores ALC) muestran una lectura numérica exacta al pasar el cursor del mouse sobre ellos, mostrando valores con un decimal. Cuando el radio es modulado por AetherSDR (modulación del host), el cuadro combinado de fuente de micrófono se bloquea en "PC" y muestra una información sobre herramientas explicando que solo la entrada de PC está disponible.

En v26.8.4, el applet detecta la capacidad de audio de transmisión del radio y adapta el cuadro combinado de fuente de micrófono en consecuencia. Cuando el audio de transmisión del radio proviene del puerto de red de este equipo (en lugar de sus propios conectores de micrófono), el cuadro combinado de fuente de micrófono se limita solo a "PC", se deshabilita, y una información sobre herramientas explica que la selección de entrada del propio radio se realiza en el radio. El medidor de nivel de micrófono se oculta en dichos radios porque no hay un nivel de entrada utilizable disponible. El botón DAX se oculta cuando el radio no tiene capacidad DAX. La detección de modo CW ahora reconoce las variantes CWL y CWU (para radios Icom y HL2), no solo "CW" simple como en los radios Flex.

## Abrir el applet de Phone/CW

1. Haga clic en el botón de bandeja **Phone/CW** en la barra lateral derecha.

El applet muestra automáticamente los controles de Phone cuando el slice activo está en un modo de voz (LSB, USB, AM, FM, etc.) y los controles de CW cuando el slice activo está en modo CW, CWL o CWU.

## Controles del panel Phone

| Control           | Tipo         | Predeterminado | Rango válido                 | Comportamiento                                                              |
|-------------------|--------------|---------|------------------------------|-----------------------------------------------------------------------------|
| **Nivel**         | Medidor      | —       | -40 a +10 dBFS (rojo > 0)    | Muestra el nivel pico de entrada del micrófono en dBFS. Pase el cursor para ver el valor exacto en dB con un decimal. Se suprime a -150 cuando met_in_rx está desactivado y no hay transmisión (v26.5.3 aplica la supresión inmediatamente en los cambios de estado). Oculto cuando el audio de transmisión del radio proviene de este equipo (sin nivel de entrada utilizable). |
| **Compresión**    | Medidor      | —       | 0 a -25 dB (relleno invertido)| Muestra la cantidad de compresión de voz en dB. Pase el cursor para ver el valor exacto como una "cantidad de compresión" positiva en dB con un decimal. Controlado por el estado de TRANSMISIÓN del interlock del radio y la habilitación del procesador de voz. v26.5.3: COMPPEAK de MeterModel (positivo de 0–25 dB) convertido a visualización de medidor negativa. |
| **ALC**           | Medidor      | —       | -20 a 0 dBFS (rojo > -3)     | Muestra el control automático de nivel de MeterModel::swAlcChanged. Se llena de derecha a izquierda. Pase el cursor para ver el valor exacto en dBFS con un decimal. Inicializado a -20 dBFS en v26.5.3. |
| **Perfil de micrófono** | Cuadro combinado | — | Se completa desde el radio  | Carga el perfil de procesamiento de micrófono nombrado.                     |
| **Fuente de micrófono** | Cuadro combinado | — | MIC, BAL, LINE, ACC, PC     | Selecciona la fuente de entrada del micrófono. Deshabilitado y limitado a "PC" cuando la modulación del host está activa o cuando la entrada del radio no puede ser elegida por este cliente. La información sobre herramientas explica el motivo en dichos radios. |
| **Ganancia de micrófono** | Deslizador  | 50      | 0-100                        | Ajusta el nivel de entrada del micrófono. Para fuente PC usa la persistencia local PcMicGain. |
| **+ACC**          | Botón de alternancia | —  | —                            | Habilita la mezcla de entrada de micrófono auxiliar.                        |
| **PROC**          | Botón de alternancia | —  | —                            | Alterna el procesador de voz.                                               |
| **NOR/DX/DX+**    | Deslizador   | 0       | 0 (NOR), 1 (DX), 2 (DX+)     | Nivel de procesador de tres posiciones.                                     |
| **DAX**           | Botón de alternancia | —  | —                            | Habilita DAX como fuente de audio de TX. Oculto cuando el radio no tiene capacidad DAX. |
| **MON**           | Botón de alternancia | —  | —                            | Habilita el monitor de tono lateral de TX.                                  |
| **Volumen del monitor** | Deslizador  | —  | 0-100                        | Establece el volumen del monitor de banda lateral.                          |

## Controles del panel CW

| Control              | Tipo         | Predeterminado | Rango válido              | Comportamiento                                                                   |
|----------------------|--------------|---------|---------------------------|----------------------------------------------------------------------------------|
| **ALC**              | Medidor      | —       | -20 a 0 dBFS (rojo > -3)  | Refleja el medidor ALC del panel Phone. Se llena de derecha a izquierda. Pase el cursor para ver el valor exacto en dBFS con un decimal. Inicializado a -20 dBFS en v26.5.3. |
| **Retardo**          | Deslizador + edición | 500 | 0-2000 ms (paso 10)       | Establece el retardo de break-in de CW. Escriba valores de 0-2000 directamente. |
| **Velocidad**        | Deslizador + edición | 20  | 5-100 PPM                  | Establece la velocidad de tecleo CW. Escriba valores de 5-100 directamente.     |
| **Tono lateral**     | Botón de alternancia | —  | —                         | Alterna el monitor de tono lateral de CW. Controla tanto el monitor alimentado por DAX del radio como el CwSidetoneGenerator local de baja latencia en sincronía. El tono y el paneo siempre siguen automáticamente cw_pitch y mon_pan_cw del radio. v26.5.3: se enruta a la salida de audio seleccionada por el usuario en lugar de la predeterminada. |
| **Volumen del tono lateral** | Deslizador + edición | 50 | 0-100                     | Establece el volumen del monitor CW. Controla tanto los volúmenes del lado del radio como los del tono lateral local. Escriba valores de 0-100 directamente. |
| **Paneo L / R (CW)** | Deslizador   | 50      | 0-100                     | Establece el paneo estéreo del monitor CW. Doble clic recentra a 50 (centro). |
| **Breakin**          | Botón de alternancia | —  | —                         | Alterna el break-in completo (QSK). Las rutas de teclado/MIDI CW respetan completamente esta configuración. |
| **Iámbico**          | Botón de alternancia | —  | —                         | Alterna el manipulador de paleta iámbica.                                      |
| **Tono < / >**       | Edición + botones | 600    | 100-6000 Hz (paso 10)     | QLineEdit con botones < / >. Escriba valores de 100-6000 o haga clic en los botones para avanzar en pasos de 10 Hz. |

## Edición de valores CW escribiendo

Puede escribir un número preciso directamente en cualquiera de los cuatro campos de valor CW (Retardo, Velocidad, Volumen del tono lateral, Tono) en lugar de arrastrar un deslizador o hacer clic en los botones de paso. Esto coincide con el comportamiento nativo de SmartSDR.

### Pasos

1. Abra el applet de Phone/CW con el slice activo en modo CW.
2. Localice el control CW que desea editar: **Retardo**, **Velocidad**, **Volumen del tono lateral** o **Tono**. Cada uno está junto a su deslizador correspondiente.
3. Haga clic dentro del campo numérico (un QLineEdit). El campo mostrará un cursor de texto.
4. Escriba el valor deseado usando su teclado.
5. Presione **Enter** o haga clic en otro lugar para aplicar el valor.

### Rangos de valores para entrada directa

| Control             | Predeterminado | Rango válido                                     |
|---------------------|---------|--------------------------------------------------|
| **Retardo**         | 500     | 0-2000 ms (paso 10)                              |
| **Velocidad**       | 20      | 5-100 PPM                                        |
| **Volumen del tono lateral** | 50 | 0-100                                            |
| **Tono**            | 600     | 100-6000 Hz (paso 10)                            |

## Medidores ALC (v26.5.1)

Tanto el panel Phone como el panel CW contienen un medidor ALC. Estos medidores son espejos idénticos que leen de la misma fuente `MeterModel::swAlcChanged`. Esto garantiza que los operadores de SSB que observan la ganancia del micrófono vean el mismo indicador que los operadores de CW usan para verificar la forma limpia de la envolvente de tecleo.

- **Rango**: -20 dBFS (vacío) a 0 dBFS (lleno)
- **Zona roja**: > -3 dBFS
- **Dirección de llenado**: De derecha a izquierda (vacío en -20, se llena hacia la izquierda hasta 0)
- **Marcas de escala**: -20, -15, -10, -5, 0 dBFS
- **Estado inicial**: Ambos medidores comienzan en -20 dBFS al construir el applet (v26.5.3).
- **Lectura al pasar el cursor**: Pase el cursor sobre cualquiera de los medidores ALC para ver el valor exacto en dBFS con un decimal (v26.7.4).

## Lecturas al pasar el cursor sobre los medidores (v26.7.4)

Los cuatro medidores (Nivel, Compresión y ambos medidores ALC) muestran una lectura numérica exacta al pasar el cursor del mouse sobre ellos. Esto le permite leer el valor de medición preciso sin tener que calcularlo visualmente contra la escala.

| Medidor             | Formato al pasar el cursor                          |
|---------------------|-----------------------------------------------------|
| **Nivel**           | Muestra el valor en dB con un decimal (p. ej., "-12.3 dB") |
| **Compresión**      | Muestra el valor en dB positivo con un decimal (p. ej., "8.5 dB") |
| **ALC (ambos paneles)** | Muestra el valor en dBFS con un decimal (p. ej., "-5.7 dBFS") |

## Bloqueo de la fuente de micrófono para modulación del host (v26.7.4)

Cuando el radio es modulado por AetherSDR (modulación del host activa), el cuadro combinado **Fuente de micrófono** se establece automáticamente en "PC" y se deshabilita. La información sobre herramientas explica:

> Este radio es modulado por AetherSDR, por lo que el micrófono de PC es la única entrada. Las otras fuentes son conectores de FlexRadio.

Esto evita seleccionar conectores de micrófono que no existen en un radio modulado por el host.

## Limitación de la fuente de micrófono según la capacidad del radio (v26.8.4)

Cuando el audio de transmisión del radio proviene de este equipo (su propia selección de entrada se realiza en el radio, no por este cliente), el cuadro combinado **Fuente de micrófono** se limita a una sola entrada, "PC", y se deshabilita. La información sobre herramientas explica:

> Este radio toma el audio de transmisión de este equipo. Su propia selección de entrada se realiza en el radio.

Establecer el estado del modelo en "PC" en esta situación mantiene a radiocert y otros lectores del modelo sincronizados con lo que muestra la interfaz.

## Visibilidad del botón DAX (v26.8.4)

El botón de alternancia **DAX** se oculta cuando el radio conectado no tiene capacidad DAX. Cuando está oculto, DAX también se fuerza a desactivado del lado del cliente para que no persista ningún estado obsoleto.

## Solución de problemas

- **El valor escrito vuelve al valor anterior** — El radio puede haber rechazado el valor. Asegúrese de que su entrada esté dentro del rango válido mostrado arriba. Para valores de Retardo, la emisión del radio ya no devuelve el deslizador a su posición en v0.9.8 (#2428).
- **El medidor de nivel permanece en -150 después de detener la transmisión** — En v26.5.3, el medidor de nivel se suprime siempre que se recibe con met_in_rx desactivado. Verifique **Settings > Appearance > Disable level meter during receive** si ve lecturas de -150 inesperadas en RX.
- **El medidor de nivel no aparece en absoluto** — En v26.8.4, el medidor de Nivel se oculta en radios cuyo audio de transmisión proviene de este equipo, porque no existe un nivel de entrada utilizable. Verifique el modelo del radio y su configuración de entrada de audio.
- **El medidor de compresión muestra valores inesperados** — v26.5.3 cambió la interpretación de COMPPEAK a positivo de 0–25 dB; la cara del medidor se invierte a -25–0 dB. Si ve una escala invertida, verifique que esté ejecutando v26.5.3 o posterior.
- **Los colores no coinciden con el tema activo** — v26.6.1 corrigió la herencia de tema para todos los elementos de la interfaz en este applet. Si los colores parecen codificados (p. ej., azul sobre negro independientemente del tema), verifique que esté ejecutando v26.6.1 o posterior.
- **La lectura al pasar el cursor sobre el medidor no aparece** — Las lecturas al pasar el cursor se agregaron en v26.7.4. Si no las ve, verifique que esté ejecutando v26.7.4 o posterior.
- **El cuadro combinado de fuente de micrófono está fijo en "PC"** — La modulación del host puede estar activa, o la entrada del radio no puede ser elegida por este cliente. Pase el cursor sobre el cuadro combinado para ver la información sobre herramientas que explica el motivo.

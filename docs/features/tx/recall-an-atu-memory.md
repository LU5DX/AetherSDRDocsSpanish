# Recordar una Forma de Onda

Use el recuerdo de memoria del ATU para aplicar una solución de sintonización previamente almacenada para la banda o frecuencia actual, omitiendo un ciclo completo de resintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles de TX requiere una conexión activa con la radio.
- El ATU interno de la radio debe tener al menos una memoria almacenada de un ciclo de sintonización anterior. Si no existe memoria para la frecuencia actual, recordarla no tendrá ningún efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE o cuando la radio no tiene sintonizador de antena.

## Pasos

1. Abra el applet de Controles de TX. Si no está visible, haga clic en el botón de la bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar el recuerdo de memoria del ATU.
3. Confirme que el indicador **Mem** se enciende en verde. Un indicador **Mem** verde confirma que el ATU está usando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a atenuarse.

## Qué hace cada control

| Control    | Tipo       | Comportamiento                                                                                                                                                                                                                     |
|------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Pwr     | Medidor    | Muestra la potencia directa en la salida del excitador con retención de pico PEP (retención de 2 s y luego decaimiento al valor suavizado actual en ~2,5 s). El pico se restablece inmediatamente al desactivar la transmisión. Pase el cursor del mouse sobre el indicador para ver la potencia exacta en vatios (#3936). La escala cambia según el modelo de radio. La balística de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del medidor S de RX. |
| SWR        | Medidor    | Muestra la relación de onda estacionaria en el excitador. Rango 1.0–3.0, en rojo por encima de 2.5. Pase el cursor del mouse sobre el indicador para ver la relación exacta en forma N.N:1 (#3936). |
| RF Power   | Control deslizante | Establece el nivel de potencia de RF de transmisión (0–100% del máximo). Muestra el valor actual en porcentaje mientras arrastra. Al soltar, sincroniza el valor desde el modelo de radio.                                                                             |
| Tune Pwr   | Control deslizante | Establece el nivel de potencia de la portadora de sintonía (0–100% del máximo). Muestra el valor actual en porcentaje mientras arrastra. Al soltar, sincroniza el valor desde el modelo de radio.                                                                            |
| TX Profile | Cuadro combinado | Selecciona un perfil de TX de la lista de perfiles de la radio. Al seleccionarlo, carga el perfil inmediatamente.                                                                                                                                      |
| Success    | Indicador  | Se enciende en verde cuando el estado del ATU es Successful u OK.                                                                                                                                                                 |
| Byp        | Indicador  | Se enciende en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                                                                                |
| Mem        | Indicador  | Se enciende en verde cuando el ATU está usando una memoria.                                                                                                                                                                        |
| TUNE       | Botón      | Inicia/detiene la portadora de sintonía; el texto cambia a 'TUNING...' con fondo rojo mientras está activo. El clic derecho selecciona la forma de la portadora (Mono Tone / Two Tone) para el siguiente ciclo de sintonía. Activa el transmisor (#3646).                            |
| MOX        | Botón de alternancia | Alterna la transmisión manual. El botón se pone rojo mientras la TX está activada. El estado inactivo muestra borde/texto con acento ámbar (#3663), editable en el Editor de Temas (color.tx.mox.*). Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado en modos de telefonía. Activa el transmisor (#3646). |
| ATU        | Botón      | Inicia el ciclo de sintonización del ATU interno. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía bypass en su lugar. El clic derecho abre las acciones de barrido previo a la sintonía y Borrar memorias del ATU. Deshabilitado cuando el TGXL está en modo OPERATE o cuando la radio no tiene sintonizador de antena. Activa el transmisor (#3646). |
| MEM        | Botón de alternancia | Alterna el recuerdo de memoria del ATU activado/desactivado. Deshabilitado cuando el TGXL está en modo OPERATE o cuando la radio no tiene sintonizador de antena.                                                                                                                                                          |
| APD        | Botón de alternancia | Alterna la predistorsión adaptativa en la radio.                                                                                                                                                                                    |
| Active     | Indicador  | Se enciende en verde cuando APD está activado y el ecualizador se está aplicando activamente.                                                                                                                                                                |
| Cal        | Indicador  | Se enciende en verde cuando APD está activado y aún está calibrando.                                                                                                                                                                |
| Avail      | Indicador  | Se enciende en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.                                                                                                                                                   |

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón **ATU** alterna entre sintonizar y pasar por alto (bypass) según la frecuencia, coincidiendo con el comportamiento de SmartSDR. Haga clic derecho en el botón **ATU** para acceder a opciones adicionales de gestión del ATU.

| Situación | Resultado de hacer clic en ATU |
|-----------|--------------------------------|
| No hay una sintonía exitosa previa, o la frecuencia ha cambiado desde la última sintonía | Inicia un ciclo de sintonización del ATU nuevo. |
| El estado del ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonía | Cambia el ATU a bypass. |
| El ATU está en Bypass o ManualBypass | Inicia un ciclo de sintonización del ATU nuevo. |

**Puntos clave:**

- La radio recuerda la frecuencia en la que el ATU reportó por última vez una sintonía exitosa. Si cambia de frecuencia entre clics, el botón siempre inicia un ciclo de sintonización nuevo en lugar de pasar a bypass, incluso si el estado anterior era Successful u OK.
- Después de que el ATU entra en bypass, la frecuencia sintonizada almacenada se borra. El siguiente clic iniciará un ciclo de sintonización nuevo independientemente de la frecuencia.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales, coincidiendo con SmartSDR Windows:

| Acción | Descripción |
|--------|-------------|
| **Pre-tune bands…** | Abre un diálogo para ejecutar un barrido previo a la sintonía en las bandas seleccionadas. Esta acción solo está disponible cuando el recuerdo de memoria del ATU (MEM) está habilitado. Si MEM está desactivado, la acción aparece atenuada con una sugerencia que indica que primero habilite MEM. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias del ATU almacenadas en la radio. |

## MOX y tonos Quindar

Al hacer clic en **MOX**, el comando se enruta a través del coordinador de tonos Quindar en lugar de alternar directamente la transmisión. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de telefonía, el tono K se reproduce al activar PTT y el tono BK se reproduce al desactivar PTT. Cuando Quindar está deshabilitado o el slice de TX activo no está en un modo de telefonía, el comportamiento es idéntico a versiones anteriores.

No se requiere configuración adicional en el applet de Controles de TX. Habilite o deshabilite los tonos Quindar desde el control QUIN de la tira de canales de audio.

## Menú contextual del botón TUNE

Haga clic derecho en el botón **TUNE** para establecer la forma de la portadora para el siguiente ciclo de sintonía. Esta es una selección de una sola vez: el modo de sintonía de la radio se almacena en estado volátil y no se conserva entre ciclos de encendido ni se guarda en la configuración de AetherSDR.

| Opción del menú | Descripción |
|-----------------|-------------|
| **Mono Tone** | Establece la portadora de sintonía a un tono único. Este es el comportamiento predeterminado. |
| **Two Tone** | Establece la portadora de sintonía a un patrón de dos tonos. |

El modo de sintonía actualmente activo se muestra con una marca de verificación. Al seleccionar una opción, se aplica inmediatamente para la siguiente pulsación de TUNE.

## Marcadores de activación de TX

Los botones **TUNE**, **MOX** y **ATU** están marcados como controles de activación de TX (#3646). Esto significa que se identifican visualmente como botones que activan el transmisor, lo que le ayuda a distinguirlos rápidamente de otros controles.

## Medidor de potencia directa con retención de pico

El medidor **RF Pwr** incluye una barra de retención de pico que sigue la potencia de envolvente de pico (PEP). El valor de pico se mantiene durante 2 segundos y luego decae suavemente hacia el nivel de potencia actual. La tasa de decaimiento se escala al rango de escala completa del indicador (120 W sin amplificador o 600 W con el excitador Aurora 500W), por lo que la sensación visual permanece consistente.

- El valor de retención de pico se restablece a cero inmediatamente cuando la radio desactiva la transmisión, evitando que una lectura de PEP retenida persista entre transmisiones.
- El comportamiento de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del medidor S de RX.

## Lecturas al pasar el cursor sobre los indicadores

Los indicadores **RF Pwr** y **SWR** ahora muestran una lectura numérica exacta al pasar el cursor del mouse sobre ellos (#3936):

- **RF Pwr** — Muestra la potencia directa precisa en vatios (p. ej., "45 W"), redondeada al vatio más cercano.
- **SWR** — Muestra la relación de onda estacionaria exacta en la forma convencional N.N:1 (p. ej., "1.32:1").

Esto elimina la necesidad de estimar valores entre las marcas de graduación, especialmente cuando se opera en niveles de potencia donde la escala del indicador comprime el rango útil.

## Visualización de porcentaje en los controles deslizantes

Los controles deslizantes **RF Power** y **Tune Pwr** muestran el valor actual como porcentaje (p. ej., "50%") mientras arrastra el control deslizante. Al soltar, el valor se sincroniza desde el modelo de radio para garantizar que la posición del control coincida con el estado real de la radio.

## Estilo de acento del estado inactivo de MOX

Cuando **MOX** no está activo (estado inactivo/azul), el botón utiliza un borde y texto en color ámbar (#3663) que lo distingue de sus vecinos **TUNE**, **ATU** y **MEM**. Los colores de acento están tokenizados bajo `color.tx.mox.*` y se pueden personalizar en el Editor de Temas, reflejando el enfoque utilizado para el chip LIVE del waterfall (#3761).

- Cuando está activo (transmitiendo), el botón usa el fondo rojo estándar (#cc2222).
- Cuando está deshabilitado, el botón usa una apariencia gris atenuada.

## Consejos

- Si **Byp** se enciende en naranja después de habilitar **MEM**, el ATU ha vuelto a bypass. Ejecute un ciclo de sintonización nuevo con **ATU** para crear una memoria nueva para la frecuencia actual.
- Los indicadores **Mem** y **Success** pueden estar encendidos al mismo tiempo; **Mem** confirma que se está usando una memoria, mientras que **Success** confirma que la solución almacenada es válida.
- Para pasar el ATU a bypass sin ejecutar un ciclo de sintonización nuevo, haga clic en **ATU** una segunda vez en la misma frecuencia donde ocurrió la última sintonía exitosa. El indicador **Byp** se encenderá en naranja para confirmar que el bypass está activo.
- Para borrar las memorias del ATU en todas las bandas, haga clic derecho en **ATU** y seleccione **Clear ATU memories…**. Use **Pre-tune bands…** para reconstruir memorias para las bandas de uso frecuente.
- Pase el cursor sobre los indicadores RF Pwr o SWR para obtener una lectura numérica exacta en lugar de estimar entre las marcas de graduación.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE, o la radio no tiene sintonizador de antena. Si la radio tiene un sintonizador, verifique el modo de operación del TGXL antes de continuar. Si la radio no tiene sintonizador (por ejemplo, una Hermes-Lite 2), los controles ATU y MEM no están disponibles.
- **El indicador Mem permanece atenuado después de hacer clic en MEM** — No existe una memoria del ATU almacenada para la frecuencia actual. Ejecute primero un ciclo completo de sintonización del ATU usando **ATU** y luego intente **MEM** nuevamente.
- **Byp se enciende en naranja en lugar de que Mem se encienda en verde** — El ATU ha entrado en bypass porque no se encontró ninguna memoria utilizable. Use **ATU** para sintonizar y almacenar una solución nueva.
- **El botón ATU inicia una sintonía nueva en lugar de pasar a bypass** — La frecuencia de transmisión cambió desde la última sintonía exitosa. El botón no pasará a bypass hasta que vuelva a la frecuencia exacta que se sintonizó. Sintonice nuevamente en la frecuencia actual primero.
- **MOX se activa pero no se reproducen tonos Quindar** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que el slice de TX activo está configurado en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **Pre-tune bands… está atenuado** — Habilite MEM primero haciendo clic en el botón **MEM**. El barrido previo a la sintonía requiere que el recuerdo de memoria esté activo.

## Relacionado

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonía para verificar la SWR](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de los Controles de TX](overview.md)

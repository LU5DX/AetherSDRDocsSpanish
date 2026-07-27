# Recordar una memoria del ATU

Use la función de recuperación de memoria del ATU para aplicar una solución de sintonizador previamente almacenada para la banda o frecuencia actual, omitiendo un ciclo completo de resintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX Controls requiere una conexión de radio activa.
- El ATU interno de la radio debe tener al menos una memoria almacenada de un ciclo de sintonización anterior. Si no existe memoria para la frecuencia actual, la recuperación no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra el applet TX Controls. Si no está visible, haga clic en el botón de la bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar la recuperación de memoria del ATU.
3. Confirme que el indicador **Mem** se encienda en verde. Un indicador **Mem** verde confirma que el ATU está usando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a un estado tenue.

## Qué hace cada control

| Control    | Tipo       | Comportamiento                                                                                                                                                                                                                           |
|------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Pwr     | Medidor    | Muestra la potencia directa a la salida del excitador con retención de pico PEP (retención de 2 s, luego decaimiento al valor suavizado actual en ~2.5 s). El pico se reinicia inmediatamente al dejar de transmitir. Pase el cursor del mouse sobre el indicador para ver la potencia exacta en vatios (#3936). La escala cambia según el modelo de radio. La balística de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del S-meter de recepción. |
| SWR        | Medidor    | Muestra la relación de onda estacionaria en el excitador. Rango 1.0–3.0, rojo por encima de 2.5. Pase el cursor del mouse sobre el indicador para ver la relación exacta en forma N.N:1 (#3936).                                                            |
| RF Power   | Control deslizante | Establece el nivel de potencia de transmisión de RF (0–100% del máximo). Muestra el valor actual en porcentaje mientras se arrastra. Al soltarlo, sincroniza el valor desde el modelo de radio.                                                                             |
| Tune Pwr   | Control deslizante | Establece el nivel de potencia de la portadora de sintonía (0–100% del máximo). Muestra el valor actual en porcentaje mientras se arrastra. Al soltarlo, sincroniza el valor desde el modelo de radio.                                                                            |
| TX Profile | Cuadro combinado  | Selecciona un perfil de TX de la lista de perfiles de la radio. La selección carga el perfil inmediatamente.                                                                                                                                      |
| Success    | Indicador  | Se enciende en verde cuando el estado del ATU es Successful u OK.                                                                                                                                                                                 |
| Byp        | Indicador  | Se enciende en naranja cuando el ATU está en Bypass o ManualBypass.                                                                                                                                                                          |
| Mem        | Indicador  | Se enciende en verde cuando el ATU está usando una memoria.                                                                                                                                                                                      |
| TUNE       | Botón      | Inicia/detiene la portadora de sintonía; el texto cambia a 'TUNING...' con fondo rojo mientras está activo. El clic derecho selecciona la forma de la portadora (Mono Tone / Two Tone) para el próximo ciclo de sintonía. Activa el transmisor (#3646).                            |
| MOX        | Botón de alternancia | Activa/desactiva la transmisión manual. El botón se vuelve rojo mientras la TX está activa. En estado inactivo muestra borde/texto en ámbar (#3663), editable en el Editor de temas (color.tx.mox.*). La ruta pasa a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado en modos de telefonía. Activa el transmisor (#3646). |
| ATU        | Botón      | Inicia el ciclo de sintonización del ATU interno. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía un bypass. El clic derecho abre las acciones de barrido de presintonización y borrado de memorias del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. Activa el transmisor (#3646). |
| MEM        | Botón de alternancia | Activa/desactiva la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE.                                                                                                                                                          |
| APD        | Botón de alternancia | Activa/desactiva la predistorsión adaptativa en la radio.                                                                                                                                                                                     |
| Active     | Indicador  | Se enciende en verde cuando APD está activado y el ecualizador se aplica activamente.                                                                                                                                                                |
| Cal        | Indicador  | Se enciende en verde cuando APD está activado y aún está calibrando.                                                                                                                                                                                |
| Avail      | Indicador  | Se enciende en verde cuando APD está activado y hay una calibración disponible pero aún no se ha aplicado.                                                                                                                                                   |

## Comportamiento del botón ATU

A partir de v0.9.5.1, el botón **ATU** alterna entre sintonización y bypass por frecuencia, coincidiendo con el comportamiento de SmartSDR. Haga clic derecho en el botón **ATU** para acceder a opciones adicionales de gestión del ATU.

| Situación | Resultado de hacer clic en ATU |
|-----------|--------------------------------|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización ATU. |
| El estado del ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonización | Cambia el ATU a bypass. |
| El ATU está en Bypass o ManualBypass | Inicia un nuevo ciclo de sintonización ATU. |

**Puntos clave:**

- La radio recuerda la frecuencia en la que el ATU informó por última vez una sintonización exitosa. Si cambia la frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonización en lugar de hacer bypass, incluso si el estado anterior era Successful u OK.
- Después de que el ATU entra en bypass, la frecuencia sintonizada almacenada se borra. El siguiente clic iniciará un nuevo ciclo de sintonización independientemente de la frecuencia.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales, coincidiendo con SmartSDR Windows:

| Acción | Descripción |
|--------|-------------|
| **Pre-tune bands…** | Abre un diálogo para ejecutar un barrido de presintonización en las bandas seleccionadas. Esta acción solo está disponible cuando la recuperación de memoria del ATU (MEM) está habilitada. Si MEM está desactivado, la acción aparece atenuada con una sugerencia que indica que habilite MEM primero. |
| **Clear ATU memories…** | Solicita confirmación, luego borra todas las memorias almacenadas del ATU en la radio. |

## MOX y tonos Quindar

Al hacer clic en **MOX**, la ruta pasa a través del coordinador de tonos Quindar en lugar de activar/desactivar directamente la transmisión. Cuando el chip QUIN está habilitado en la tira de canal de audio y el slice TX activo está en un modo de telefonía, el tono K se reproduce al presionar PTT y el tono BK se reproduce al soltar PTT. Cuando Quindar está deshabilitado o el slice TX activo no está en un modo de telefonía, el comportamiento es idéntico a versiones anteriores.

No se requiere configuración adicional en el applet TX Controls. Habilite o deshabilite los tonos Quindar desde el control QUIN de la tira de canal de audio.

## Menú contextual de TUNE

Haga clic derecho en el botón **TUNE** para establecer la forma de la portadora para el próximo ciclo de sintonía. Esta es una selección única: el modo de sintonía de la radio se almacena en estado volátil y no se conserva entre ciclos de encendido ni se guarda en la configuración de AetherSDR.

| Opción del menú | Descripción |
|-----------------|-------------|
| **Mono Tone**   | Establece la portadora de sintonía como un tono único. Este es el comportamiento predeterminado. |
| **Two Tone**    | Establece la portadora de sintonía como un patrón de dos tonos. |

El modo de sintonía actualmente activo se muestra con una marca de verificación. Seleccionar una opción la aplica inmediatamente para la próxima pulsación de TUNE.

## Marcadores de activación de TX

Los botones **TUNE**, **MOX** y **ATU** están marcados como controles de activación de TX (#3646). Esto significa que se identifican visualmente como botones que activan el transmisor, lo que ayuda a distinguirlos rápidamente de otros controles.

## Medidor de retención de pico de potencia directa

El medidor **RF Pwr** incluye una barra de retención de pico que sigue la potencia de envolvente de pico (PEP). El valor pico se mantiene durante 2 segundos, luego decae suavemente hacia el nivel de potencia actual. La tasa de decaimiento se escala al rango de escala completa del indicador (120 W sin amplificador o 600 W con excitador Aurora 500W), por lo que la sensación visual permanece consistente.

- El valor de retención de pico se reinicia a cero inmediatamente cuando la radio deja de transmitir, evitando que una lectura de PEP retenida persista entre transmisiones.
- El comportamiento de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del S-meter de recepción.

## Lecturas al pasar el cursor sobre los indicadores

Los indicadores **RF Pwr** y **SWR** ahora muestran una lectura numérica exacta cuando pasa el cursor del mouse sobre ellos (#3936):

- **RF Pwr** — Muestra la potencia directa precisa en vatios (por ejemplo, "45 W"), redondeada al vatio más cercano.
- **SWR** — Muestra la relación de onda estacionaria exacta en la forma convencional N.N:1 (por ejemplo, "1.32:1").

Esto elimina la necesidad de estimar valores entre las marcas de graduación, especialmente cuando se opera en niveles de potencia donde la escala del indicador comprime el rango útil.

## Visualización de porcentaje en los controles deslizantes

Los controles deslizantes **RF Power** y **Tune Pwr** muestran el valor actual como un porcentaje (por ejemplo, "50%") mientras arrastra el control deslizante. Al soltarlo, el valor se sincroniza desde el modelo de radio para garantizar que la posición del control deslizante coincida con el estado real de la radio.

## Estilo de acento inactivo de MOX

Cuando **MOX** no está activo (estado inactivo/azul), el botón usa un color de borde y texto ámbar (#3663) que lo distingue de sus vecinos **TUNE**, **ATU** y **MEM**. Los colores de acento están tokenizados bajo `color.tx.mox.*` y se pueden personalizar en el Editor de temas, reflejando el enfoque utilizado para el chip LIVE de la cascada (#3761).

- Cuando está activo (transmisión), el botón usa el fondo rojo estándar (#cc2222).
- Cuando está deshabilitado, el botón usa una apariencia grisácea atenuada.

## Consejos

- Si **Byp** se enciende en naranja después de habilitar **MEM**, el ATU ha caído en bypass. Ejecute un nuevo ciclo de sintonía con **ATU** para crear una nueva memoria para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar encendidos al mismo tiempo; **Mem** confirma que se está usando una memoria, mientras que **Success** confirma que la solución almacenada es válida.
- Para poner el ATU en bypass sin ejecutar un nuevo ciclo de sintonía, haga clic en **ATU** una segunda vez en la misma frecuencia donde ocurrió la última sintonía exitosa. El indicador **Byp** se encenderá en naranja para confirmar que el bypass está activo.
- Para borrar las memorias del ATU en todas las bandas, haga clic derecho en **ATU** y seleccione **Clear ATU memories…**. Use **Pre-tune bands…** para reconstruir memorias para bandas de uso frecuente.
- Pase el cursor sobre el indicador RF Pwr o SWR para obtener una lectura numérica exacta en lugar de estimar entre las marcas de graduación.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. La recuperación de memoria no se puede activar en este modo. Verifique el modo de funcionamiento del TGXL antes de continuar.
- **El indicador Mem permanece tenue después de hacer clic en MEM** — No existe una memoria de ATU almacenada para la frecuencia actual. Ejecute primero un ciclo completo de sintonización ATU usando **ATU**, luego intente **MEM** nuevamente.
- **Byp se enciende en naranja en lugar de que Mem se ponga verde** — El ATU ha entrado en bypass porque no se encontró una memoria utilizable. Use **ATU** para sintonizar y almacenar una nueva solución.
- **El botón ATU inicia una nueva sintonización en lugar de hacer bypass** — La frecuencia de transmisión cambió desde la última sintonización exitosa. El botón no hará bypass hasta que vuelva a la frecuencia exacta que fue sintonizada. Sintonice nuevamente en la frecuencia actual primero.
- **MOX se activa pero no se reproducen los tonos Quindar** — Confirme que el chip QUIN está habilitado en la tira de canal de audio y que el slice TX activo está configurado en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **Pre-tune bands… está atenuado** — Habilite MEM primero haciendo clic en el botón **MEM**. El barrido de presintonización requiere que la recuperación de memoria esté activa.

## Relacionado

- [Run the internal ATU](run-the-internal-atu.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [TX Controls overview](overview.md)

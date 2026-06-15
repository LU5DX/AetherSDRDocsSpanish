# Recordar una memoria de la ATU

Utilice el recuerdo de memoria de la ATU para aplicar una solución de sintonización previamente almacenada para la banda o frecuencia actual, omitiendo un ciclo de resintonización completo.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa con la radio.
- La ATU interna de la radio debe tener almacenada al menos una memoria de un ciclo de sintonización anterior. Si no existe ninguna memoria para la frecuencia actual, el recuerdo no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra el applet Controles de TX. Si no está visible, haga clic en el botón de la bandeja **TX** en la barra lateral derecha.
2. Haga clic en **MEM** para activar el recuerdo de memoria de la ATU.
3. Confirme que el indicador **Mem** se ilumina en verde. Un indicador **Mem** verde confirma que la ATU está usando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a atenuarse.

## Función de cada control

| Control    | Tipo                                                                                                                             | Comportamiento                                                                                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Pwr     | Medidor                                                                                                                          | Muestra la potencia directa en la salida del excitador. La escala cambia según el modelo de la radio (0–120 W sin amplificador, 0–600 W con excitador Aurora 500W). Rojo por encima de 100 W / 500 W. Incluye una barra de retención de pico que sigue la PEP durante 2 segundos y luego se desvanece suavemente. |
| SWR        | Medidor                                                                                                                          | Muestra la relación de onda estacionaria en el excitador. Rango 1.0–3.0, rojo por encima de 2.5.                                                                                                                                                                |
| RF Power   | Deslizador                                                                                                                       | Establece el nivel de potencia de RF de transmisión (0–100% del máximo). Muestra el valor actual como porcentaje mientras se arrastra.                                                                                                                          |
| Tune Pwr   | Deslizador                                                                                                                       | Establece el nivel de potencia de la portadora de sintonía (0–100% del máximo). Muestra el valor actual como porcentaje mientras se arrastra.                                                                                                                   |
| TX Profile | Cuadro combinado                                                                                                                 | Selecciona un perfil de TX de la lista de perfiles de la radio. La selección carga el perfil inmediatamente.                                                                                                                                                    |
| Success    | Indicador                                                                                                                        | Se ilumina en verde cuando el estado de la ATU es Successful u OK.                                                                                                                                                                                              |
| Byp        | Indicador                                                                                                                        | Se ilumina en naranja cuando la ATU está en modo Bypass o ManualBypass.                                                                                                                                                                                         |
| Mem        | Indicador                                                                                                                        | Se ilumina en verde cuando la ATU está usando una memoria.                                                                                                                                                                                                      |
| TUNE       | Inicia/detiene la portadora de sintonía; el texto cambia a 'TUNING...' con fondo rojo mientras está activo. El clic derecho selecciona la forma de la portadora (Mono Tone / Two Tone) para el siguiente ciclo de sintonía. | El menú contextual del clic derecho (showTuneContextMenu) es una selección única y transitoria — no se persiste nada; la radio vuelve a single_tone al reiniciar.                                                                                              |
| MOX        | Botón de conmutación                                                                                                             | Conmuta la transmisión manual. El botón se vuelve rojo mientras la TX está activa. Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado en modos de telefonía.                                                                |
| ATU        | Inicia el ciclo de sintonización de la ATU interna. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía bypass en su lugar. El clic derecho abre las acciones de barrido de pre-sintonía y Borrar memorias de la ATU. | Deshabilitado cuando el TGXL está en modo OPERATE. El menú contextual del clic derecho (showAtuContextMenu) expone el barrido de pre-sintonía de banda (#2624) y Borrar memorias de la ATU.                                                                   |
| MEM        | Botón de conmutación                                                                                                             | Conmuta el recuerdo de memoria de la ATU activado/desactivado. Deshabilitado cuando el TGXL está en modo OPERATE.                                                                                                                                               |
| APD        | Botón de conmutación                                                                                                             | Conmuta la predistorsión adaptativa en la radio.                                                                                                                                                                                                                |
| Active     | Indicador                                                                                                                        | Se ilumina en verde cuando la APD está activada y el ecualizador se aplica activamente.                                                                                                                                                                         |
| Cal        | Indicador                                                                                                                        | Se ilumina en verde cuando la APD está activada y aún está calibrando.                                                                                                                                                                                          |
| Avail      | Indicador                                                                                                                        | Se ilumina en verde cuando la APD está activada y hay una calibración disponible pero aún no aplicada.                                                                                                                                                          |

## Comportamiento del botón ATU

A partir de la versión v0.9.5.1, el botón **ATU** conmuta entre sintonización y bypass por frecuencia, coincidiendo con el comportamiento de SmartSDR. Haga clic derecho en el botón **ATU** para acceder a opciones adicionales de gestión de la ATU.

| Situación | Resultado al hacer clic en ATU |
|------------|---------------------------------|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización de la ATU. |
| El estado de la ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonización | Cambia la ATU a bypass. |
| La ATU está en modo Bypass o ManualBypass | Inicia un nuevo ciclo de sintonización de la ATU. |

**Puntos clave:**

- La radio recuerda la frecuencia en la que la ATU reportó por última vez una sintonización exitosa. Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonización en lugar de bypass, incluso si el estado anterior era Successful u OK.
- Después de que la ATU entra en bypass, la frecuencia sintonizada almacenada se borra. El siguiente clic iniciará un nuevo ciclo de sintonización independientemente de la frecuencia.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales, que coinciden con SmartSDR Windows:

| Acción | Descripción |
|--------|-------------|
| **Pre-tune bands…** | Abre un diálogo para ejecutar un barrido de pre-sintonía en las bandas seleccionadas. Esta acción solo está disponible cuando el recuerdo de memoria de la ATU (MEM) está activado. Si MEM está desactivado, la acción se muestra atenuada con una sugerencia que indica que debe activar MEM primero. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias almacenadas de la ATU en la radio. |

## MOX y tonos Quindar

Al hacer clic en **MOX**, se enruta a través del coordinador de tonos Quindar en lugar de conmutar la transmisión directamente. Cuando el chip QUIN está habilitado en la tira de canal de audio y el slice de TX activo está en un modo de telefonía, el tono K se reproduce al presionar PTT y el tono BK se reproduce al soltar PTT. Cuando Quindar está deshabilitado o el slice de TX activo no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores.

No se requiere configuración adicional en el applet Controles de TX. Active o desactive los tonos Quindar desde el control QUIN de la tira de canal de audio.

## Menú contextual del botón TUNE

Haga clic derecho en el botón **TUNE** para establecer la forma de la portadora para el siguiente ciclo de sintonía. Esta es una selección única: el modo de sintonía de la radio se almacena en un estado volátil y no se conserva al reiniciar ni se guarda en la configuración de AetherSDR.

| Opción de menú | Descripción |
|-------------|-------------|
| **Mono Tone** | Establece la portadora de sintonía como un tono único. Este es el comportamiento predeterminado. |
| **Two Tone** | Establece la portadora de sintonía como un patrón de dos tonos. |

El modo de sintonía actualmente activo se muestra con una marca de verificación. Al seleccionar una opción, se aplica inmediatamente para la siguiente pulsación de TUNE.

## Medidor de retención de pico de potencia directa

El medidor **RF Pwr** incluye una barra de retención de pico que sigue la potencia de pico de la envolvente (PEP). El valor pico se mantiene durante 2 segundos y luego se desvanece suavemente hacia el nivel de potencia actual. La tasa de desvanecimiento se escala al rango de escala completa del indicador (120 W sin amplificador o 600 W con excitador Aurora 500W), por lo que la sensación visual se mantiene consistente.

- El valor de retención de pico se restablece a cero inmediatamente cuando la radio desactiva la transmisión, evitando que una lectura de PEP retenida persista entre ráfagas.
- El comportamiento de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del S-medidor de RX.

## Visualización de porcentaje del deslizador

Los deslizadores **RF Power** y **Tune Pwr** ahora muestran el valor actual como un porcentaje (por ejemplo, "50%") mientras arrastra el control deslizante. Esto proporciona una retroalimentación visual precisa al establecer niveles de potencia en relación con la salida máxima de la radio.

## Consejos

- Si **Byp** se ilumina en naranja después de activar **MEM**, la ATU ha entrado en bypass. Ejecute un nuevo ciclo de sintonización con **ATU** para crear una nueva memoria para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar iluminados al mismo tiempo; **Mem** confirma que se está usando una memoria, mientras que **Success** confirma que la solución almacenada es válida.
- Para poner la ATU en bypass sin ejecutar un nuevo ciclo de sintonización, haga clic en **ATU** una segunda vez en la misma frecuencia donde ocurrió la última sintonización exitosa. El indicador **Byp** se iluminará en naranja para confirmar que el bypass está activo.
- Para borrar las memorias de la ATU en todas las bandas, haga clic derecho en **ATU** y seleccione **Clear ATU memories…**. Use **Pre-tune bands…** para reconstruir memorias para bandas de uso frecuente.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. No se puede conmutar el recuerdo de memoria en este modo. Verifique el modo de funcionamiento del TGXL antes de continuar.
- **El indicador Mem permanece atenuado después de hacer clic en MEM** — No existe una memoria de ATU almacenada para la frecuencia actual. Ejecute un ciclo completo de sintonización de la ATU primero usando **ATU**, luego intente **MEM** nuevamente.
- **Byp se ilumina en naranja en lugar de que Mem se ponga verde** — La ATU ha entrado en bypass porque no se encontró ninguna memoria utilizable. Use **ATU** para sintonizar y almacenar una nueva solución.
- **El botón ATU inicia una nueva sintonización en lugar de bypass** — La frecuencia de transmisión cambió desde la última sintonización exitosa. El botón no entrará en bypass hasta que vuelva a la frecuencia exacta que se sintonizó. Sintonice nuevamente en la frecuencia actual primero.
- **MOX se activa pero no se reproducen tonos Quindar** — Confirme que el chip QUIN esté habilitado en la tira de canal de audio y que el slice de TX activo esté configurado en un modo de telefonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **Pre-tune bands… está atenuado** — Active MEM primero haciendo clic en el botón **MEM**. El barrido de pre-sintonía requiere que el recuerdo de memoria esté activo.

## Relacionado

- [Ejecutar la ATU interna](run-the-internal-atu.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Resumen de Controles de TX](overview.md)

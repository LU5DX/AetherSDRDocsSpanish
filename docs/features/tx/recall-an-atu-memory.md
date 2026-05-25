# Recordar una memoria del ATU

Use la función de recordatorio de memoria del ATU para aplicar una solución de sintonización previamente almacenada para la banda o frecuencia actual, omitiendo un ciclo completo de resintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Controles de TX requiere una conexión activa a la radio.
- El ATU interno de la radio debe tener al menos una memoria almacenada de un ciclo de sintonización anterior. Si no existe ninguna memoria para la frecuencia actual, el recordatorio no tendrá efecto.
- MEM está deshabilitado cuando el TGXL está en modo OPERATE.

## Pasos

1. Abra el applet Controles de TX. Si no está visible, haga clic en el botón **TX** de la bandeja en la barra lateral derecha.
2. Haga clic en **MEM** para activar el recordatorio de memoria del ATU.
3. Confirme que el indicador **Mem** se ilumina en verde. Un indicador **Mem** verde confirma que el ATU está usando activamente una memoria almacenada.
4. Para dejar de usar la memoria almacenada, haga clic en **MEM** nuevamente. El indicador **Mem** vuelve a atenuarse.

## Función de cada control

| Control | Tipo | Comportamiento |
|---------|------|----------|
| RF Pwr | Medidor | Muestra la potencia directa en la salida del excitador. La escala cambia según el modelo de radio (0–120 W sin amplificador, 0–600 W con excitador Aurora 500W). Se vuelve rojo por encima de 100 W / 500 W. Incluye una barra de retención de pico que rastrea la PEP durante 2 segundos y luego decae suavemente. |
| SWR | Medidor | Muestra la relación de onda estacionaria en el excitador. Rango 1.0–3.0, rojo por encima de 2.5. |
| RF Power | Deslizador | Establece el nivel de potencia de RF de transmisión (0–100 W). Muestra el valor actual en vatios mientras se arrastra. |
| Tune Pwr | Deslizador | Establece el nivel de potencia de la portadora de sintonía (0–100 W). Muestra el valor actual en vatios mientras se arrastra. |
| TX Profile | Cuadro combinado | Selecciona un perfil de TX de la lista de perfiles de la radio. Al seleccionarlo, carga el perfil inmediatamente. |
| Success | Indicador | Se ilumina en verde cuando el estado del ATU es Successful u OK. |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. |
| Mem | Indicador | Se ilumina en verde cuando el ATU está usando una memoria. |
| TUNE | Botón pulsador | Inicia/detiene la portadora de sintonía. El texto cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic derecho para elegir la forma de la portadora (Mono Tone / Two Tone) para el próximo ciclo de sintonía. |
| MOX | Botón de alternancia | Alterna la transmisión manual. El botón se vuelve rojo mientras TX está activada. Se enruta a través del coordinador de tonos Quindar cuando el chip QUIN está habilitado en modos de fonía. |
| ATU | Botón pulsador | Inicia el ciclo de sintonización del ATU interno. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía bypass en su lugar. El clic derecho abre las acciones de barrido de presintonización y borrado de memorias del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |
| MEM | Botón de alternancia | Activa/desactiva el recordatorio de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |
| APD | Botón de alternancia | Activa/desactiva la predistorsión adaptativa en la radio. |
| Active | Indicador | Se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente. |
| Cal | Indicador | Se ilumina en verde cuando APD está activado y aún está calibrando. |
| Avail | Indicador | Se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada. |

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón **ATU** alterna entre sintonización y bypass por frecuencia, coincidiendo con el comportamiento de SmartSDR. Haga clic derecho en el botón **ATU** para acceder a opciones adicionales de gestión del ATU.

| Situación | Resultado al hacer clic en ATU |
|-----------|------------------------|
| No hay una sintonización exitosa previa, o la frecuencia ha cambiado desde la última sintonización | Inicia un nuevo ciclo de sintonización del ATU. |
| El estado del ATU es Successful u OK **y** la frecuencia de transmisión no ha cambiado desde que se completó esa sintonización | Cambia el ATU a bypass. |
| El ATU está en Bypass o ManualBypass | Inicia un nuevo ciclo de sintonización del ATU. |

**Puntos clave:**

- La radio recuerda la frecuencia en la que el ATU reportó por última vez una sintonización exitosa. Si cambia de frecuencia entre clics, el botón siempre inicia un nuevo ciclo de sintonización en lugar de pasar a bypass, incluso si el estado anterior era Successful u OK.
- Después de que el ATU entra en bypass, la frecuencia de sintonización almacenada se borra. El siguiente clic iniciará un nuevo ciclo de sintonización independientemente de la frecuencia.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales, coincidiendo con SmartSDR Windows:

| Acción | Descripción |
|--------|-------------|
| **Pre-tune bands…** | Abre un cuadro de diálogo para ejecutar un barrido de presintonización en las bandas seleccionadas. Esta acción solo está disponible cuando el recordatorio de memoria del ATU (MEM) está habilitado. Si MEM está desactivado, la acción aparece atenuada con una sugerencia que indica que habilite MEM primero. |
| **Clear ATU memories…** | Solicita confirmación y luego borra todas las memorias del ATU almacenadas en la radio. |

## MOX y tonos Quindar

Al hacer clic en **MOX**, se enruta a través del coordinador de tonos Quindar en lugar de activar/desactivar la transmisión directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice de TX activo está en un modo de fonía, el tono K se reproduce al activar PTT y el tono BK se reproduce al desactivar PTT. Cuando Quindar está deshabilitado o el slice de TX activo no está en un modo de fonía, el comportamiento es idéntico a versiones anteriores.

No se requiere configuración adicional en el applet Controles de TX. Habilite o deshabilite los tonos Quindar desde el control QUIN de la tira de canales de audio.

## Menú contextual de TUNE

Haga clic derecho en el botón **TUNE** para establecer la forma de la portadora para el próximo ciclo de sintonía. Esta es una selección de un solo uso: el modo de sintonía de la radio se almacena en un estado volátil y no se conserva tras ciclos de alimentación ni se guarda en la configuración de AetherSDR.

| Opción del menú | Descripción |
|-------------|-------------|
| **Mono Tone** | Establece la portadora de sintonía en un tono único. Este es el comportamiento predeterminado. |
| **Two Tone** | Establece la portadora de sintonía en un patrón de dos tonos. |

El modo de sintonía actualmente activo se muestra con una marca de verificación. Seleccionar una opción la aplica inmediatamente para la próxima pulsación de TUNE.

## Medidor de retención de pico de potencia directa

El medidor **RF Pwr** incluye una barra de retención de pico que rastrea la potencia de pico envolvente (PEP). El valor pico se mantiene durante 2 segundos, luego decae suavemente hacia el nivel de potencia actual. La tasa de decaimiento se escala al rango completo del indicador (120 W sin amplificador o 600 W con excitador Aurora 500W), por lo que la sensación visual permanece consistente.

- El valor de retención de pico se restablece a cero inmediatamente cuando la radio desactiva la transmisión, evitando que una lectura de PEP retenida persista entre sobres.
- El comportamiento de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del S-medidor de RX.

## Visualización de vatios en los deslizadores

Los deslizadores **RF Power** y **Tune Pwr** ahora muestran el valor actual en vatios (por ejemplo, "25 W") mientras arrastra el control deslizante. Esto proporciona una retroalimentación visual precisa al establecer niveles de potencia.

## Consejos

- Si **Byp** se ilumina en naranja después de habilitar **MEM**, el ATU ha vuelto al bypass. Ejecute un nuevo ciclo de sintonía con **ATU** para crear una nueva memoria para la frecuencia actual.
- El indicador **Mem** y el indicador **Success** pueden estar iluminados al mismo tiempo; **Mem** confirma que se está usando una memoria, mientras que **Success** confirma que la solución almacenada es válida.
- Para pasar el ATU a bypass sin ejecutar un nuevo ciclo de sintonía, haga clic en **ATU** una segunda vez en la misma frecuencia donde ocurrió la última sintonización exitosa. El indicador **Byp** se iluminará en naranja para confirmar que el bypass está activo.
- Para borrar las memorias del ATU en todas las bandas, haga clic derecho en **ATU** y seleccione **Clear ATU memories…**. Use **Pre-tune bands…** para reconstruir memorias para las bandas de uso frecuente.

## Solución de problemas

- **El botón MEM está atenuado y no se puede hacer clic** — El TGXL está en modo OPERATE. El recordatorio de memoria no se puede alternar en este modo. Verifique el modo de operación del TGXL antes de continuar.
- **El indicador Mem permanece atenuado después de hacer clic en MEM** — No existe una memoria del ATU almacenada para la frecuencia actual. Ejecute primero un ciclo completo de sintonización del ATU usando **ATU**, luego intente **MEM** nuevamente.
- **Byp se ilumina en naranja en lugar de que Mem se ponga verde** — El ATU ha entrado en bypass porque no se encontró una memoria utilizable. Use **ATU** para sintonizar y almacenar una nueva solución.
- **El botón ATU inicia una nueva sintonización en lugar de pasar a bypass** — La frecuencia de transmisión cambió desde la última sintonización exitosa. El botón no pasará a bypass hasta que esté en la frecuencia exacta que se sintonizó. Sintonice nuevamente en la frecuencia actual primero.
- **MOX se activa pero no se reproducen tonos Quindar** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que el slice de TX activo está configurado en un modo de fonía. Los tonos Quindar no se reproducen en modos CW o digitales.
- **Pre-tune bands… está atenuado** — Habilite MEM primero haciendo clic en el botón **MEM**. El barrido de presintonización requiere que el recordatorio de memoria esté activo.

## Relacionados

- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de los Controles de TX](overview.md)

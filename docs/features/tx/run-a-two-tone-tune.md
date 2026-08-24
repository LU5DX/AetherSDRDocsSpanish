# Ejecutar una Prueba de Dos Tonos

Una prueba de dos tonos le permite verificar la linealidad del transmisor y los niveles de excitación, activando la radio manualmente con MOX mientras monitorea la potencia directa y la ROE. Utilice este procedimiento cuando su equipo esté en modo SSB y desee verificar la salida sin transmitir audio.

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 (el indicador de radio muestra conectado).
- El applet de Controles TX es visible. Si no lo está, haga clic en el botón de la bandeja TX en la barra lateral derecha.
- Su transceptor está configurado en modo SSB y se encuentra en una frecuencia despejada.
- Una fuente de audio de dos tonos (generador externo o software) está lista para alimentar la entrada de micrófono o de línea de la radio.

## Pasos

1. En el applet de Controles TX, ajuste el control deslizante **Tune Pwr** al nivel de potencia que desee usar para la prueba. El valor predeterminado es 10; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en porcentaje (p. ej., «10%»).
2. Ajuste el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100; el rango válido es 0–100. Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor de potencia en porcentaje (p. ej., «100%»).
3. Si desea usar un perfil de transmisión específico (por ejemplo, un perfil SSB limpio sin procesamiento), selecciónelo en el menú desplegable **TX Profile**.
4. Inicie la señal de audio de dos tonos desde su fuente externa para que alimente la entrada de la radio.
5. Haga clic en **MOX**. El botón se vuelve rojo y la radio activa la transmisión.
6. Observe el medidor **RF Pwr** (0–120 W, rojo por encima de 100 W) y el medidor **SWR** (1.0–3.0, rojo por encima de 2.5). El medidor RF Pwr incluye una barra de retención de pico que mantiene el nivel máximo durante 2 segundos antes de decaer hacia el nivel de potencia actual. La retención de pico se restablece a cero inmediatamente al desactivar la transmisión. Ajuste el control deslizante **RF Power** mientras transmite para alcanzar su salida objetivo.
   - Pase el cursor sobre el medidor RF Pwr para ver la potencia exacta como información sobre herramientas (p. ej., «47 W»).
   - Pase el cursor sobre el medidor SWR para ver la relación exacta como información sobre herramientas (p. ej., «1.35:1»).
7. Cuando la prueba esté completa, haga clic en **MOX** nuevamente para desactivar la transmisión. El botón vuelve a su estado sin iluminar con un borde y acento de texto ámbar. Tanto el medidor RF Pwr como el SWR se restablecen a sus posiciones de reposo (0 W y 1.0) inmediatamente al desactivar la transmisión.
8. Detenga la fuente de audio de dos tonos.

## Qué hace cada control

| Control    | Tipo                                                                                                                                                                                                                                                              | Valor predeterminado                                                                                                                                                 |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Control deslizante                                                                                                                                                                                                                                                | 100                                                                                                                                                                  |
| Tune Pwr   | Control deslizante                                                                                                                                                                                                                                                | 10                                                                                                                                                                   |
| TX Profile | Menú desplegable                                                                                                                                                                                                                                                  | —                                                                                                                                                                    |
| MOX        | Botón de alternancia                                                                                                                                                                                                                                              | —                                                                                                                                                                    |
| RF Pwr     | Muestra la potencia directa en la salida del excitador con retención de pico PEP (2 s de retención y luego decae al valor suavizado actual en ~2.5 s). El pico se restablece inmediatamente al desactivar la transmisión. Pase el cursor para ver la potencia exacta como información sobre herramientas. | La escala cambia según el modelo de radio mediante setPowerScale. La balística de retención de pico coincide con la barra de retención de pico de SmartSDR y el patrón de retención de pico del medidor S de RX en SMeterWidget (#2561). |
| SWR        | Muestra la relación de onda estacionaria en el excitador. Cuando no hay datos de ROE disponibles (por ejemplo, durante una pausa en la transmisión), el medidor se estaciona en su posición de reposo 1.0 en lugar de leer 0.0 o mantener un valor obsoleto.       | —                                                                                                                                                                    |
| TUNE       | Inicia/detiene la portadora de sintonía; el texto cambia a 'TUNING...' con fondo rojo mientras está activo. El clic derecho selecciona la forma de la portadora (Tono único / Dos tonos) para el siguiente ciclo de sintonía.                                        | El menú contextual del clic derecho (showTuneContextMenu) es transitorio de un solo uso — no se persiste nada; la radio vuelve a single_tone en cada ciclo de encendido. |
| ATU        | Inicia el ciclo de sintonía del ATU interno. Si el estado es Exitoso/OK en la misma frecuencia, un segundo clic envía bypass en su lugar. El clic derecho abre las acciones de barrido de pre-sintonía y borrar memorias ATU.                                           | Deshabilitado cuando TGXL está en modo OPERATE, o cuando la radio no tiene acoplador de antena (p. ej., Hermes-Lite 2). El menú contextual del clic derecho (showAtuContextMenu) expone el barrido de banda de pre-sintonía (#2624) y Borrar memorias ATU. |
| MEM        | Botón de alternancia                                                                                                                                                                                                                                              | —                                                                                                                                                                    |
| APD        | Botón de alternancia                                                                                                                                                                                                                                              | —                                                                                                                                                                    |
| Active     | Indicador (verde)                                                                                                                                                                                                                                                 | atenuado                                                                                                                                                             |
| Cal        | Indicador (verde)                                                                                                                                                                                                                                                 | atenuado                                                                                                                                                             |
| Avail      | Indicador (verde)                                                                                                                                                                                                                                                 | atenuado                                                                                                                                                             |
| Success    | Indicador (verde)                                                                                                                                                                                                                                                 | atenuado                                                                                                                                                             |
| Byp        | Indicador (naranja)                                                                                                                                                                                                                                               | atenuado                                                                                                                                                             |
| Mem        | Indicador (verde)                                                                                                                                                                                                                                                 | atenuado                                                                                                                                                             |
## Consejos

- Mantenga la ROE por debajo de 2.5 durante la prueba. El medidor SWR se vuelve rojo por encima de 2.5 como advertencia visual.
- Seleccione un perfil TX que tenga el procesamiento de micrófono deshabilitado antes de ejecutar una prueba de dos tonos. El procesamiento puede distorsionar la envolvente de dos tonos y producir lecturas IMD engañosas.
- Si tiene memorias ATU disponibles, considere recuperar una memoria conocida antes de activar la transmisión para asegurar que la antena esté acoplada. Consulte [Recuperar una memoria ATU](recall-an-atu-memory.md).
- Si el chip QUIN está habilitado en la tira de canales de audio y la tajada TX activa está en un modo de teléfono, al hacer clic en **MOX** se reproducirá el tono K de Quindar al activar y el tono BK al desactivar. Si Quindar está deshabilitado o la tajada TX no está en un modo de teléfono, **MOX** se comporta como en versiones anteriores.
- Los controles deslizantes RF Power y Tune Pwr ahora también actualizan su valor mostrado desde el modelo al soltar el control deslizante. Esto asegura que el valor mostrado siempre coincida con la configuración real de la radio.

## Comportamiento del botón ATU

El botón **ATU** alterna entre iniciar un ciclo de sintonía y derivar el acoplador, reflejando el comportamiento por frecuencia en SmartSDR.

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía ATU nuevo. El indicador **Success** se enciende en verde cuando el acoplador encuentra una coincidencia.
- **Segundo clic en la misma frecuencia** — si el estado del ATU ya es Exitoso u OK y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente se cambia el acoplador a bypass. El indicador **Byp** se enciende en naranja.
- **Clic después de un cambio de frecuencia** — siempre inicia un ciclo de sintonía nuevo, incluso si el estado anterior era Exitoso u OK.
- **Después del bypass** — la frecuencia sintonizada almacenada internamente se borra. El siguiente clic iniciará un ciclo de sintonía nuevo independientemente de la frecuencia.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE, o cuando la radio conectada no tiene acoplador de antena (por ejemplo, un Hermes-Lite 2). Cuando el botón está deshabilitado por cualquiera de estas razones, pase el cursor sobre él para ver una información sobre herramientas que explique el motivo. La información sobre herramientas prioriza la explicación de ausencia de acoplador sobre la de TGXL-OPERATE, ya que una radio sin acoplador hace irrelevante el estado del TGXL.

## Menú contextual del botón ATU

Haga clic derecho en el botón **ATU** para mostrar un menú contextual con dos acciones adicionales:

- **Pre-tune bands…** — Abre el diálogo de Pre-Sintonía para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando las memorias ATU están habilitadas. Si las memorias están deshabilitadas, el elemento del menú aparece atenuado con una información sobre herramientas que sugiere habilitar MEM primero.
- **Clear ATU memories…** — Borra todas las memorias ATU almacenadas después de un diálogo de confirmación.

## Menú contextual del botón TUNE

Haga clic derecho en el botón **TUNE** para seleccionar la forma de la portadora para el siguiente ciclo de sintonía:

- **Mono Tone** — Tono único, la forma de portadora predeterminada.
- **Two Tone** — Portadora de dos tonos para pruebas de linealidad.

La selección es de un solo uso y no se persiste entre ciclos de encendido. El modo de sintonía de la radio vuelve al tono único por sí mismo entre ciclos de encendido. Una marca de verificación junto a cualquiera de las entradas muestra el modo de sintonía actual de la radio.

## APD (Pre-Distorsión Adaptativa)

El botón de alternancia **APD** habilita o deshabilita la pre-distorsión adaptativa en la radio. Cuando está habilitado, los tres indicadores de estado debajo del botón muestran el estado actual:

- **Active** — Se enciende en verde cuando el ecualizador se aplica activamente.
- **Cal** — Se enciende en verde cuando la radio aún está calibrando.
- **Avail** — Se enciende en verde cuando hay una calibración disponible pero aún no aplicada.

Los indicadores progresan a través de Cal → Avail → Active a medida que el sistema APD completa su ciclo de calibración.

## Acento del botón MOX en estado inactivo

Cuando no está transmitiendo (estado inactivo), el botón **MOX** muestra un borde y acento de texto ámbar que lo distingue de los botones neutros TUNE, ATU y MEM. Este acento es editable en el Editor de Temas bajo los tokens `color.tx.mox.*`, reflejando el acento del chip LIVE en el waterfall.

## Solución de problemas

- **MOX activa pero RF Pwr lee cero** — La fuente de audio de dos tonos puede no estar llegando a la entrada de la radio, o el modo no es SSB. Confirme la ruta de audio y la selección de modo antes de volver a activar la transmisión.
- **SWR se pone rojo inmediatamente al presionar MOX** — La antena no está acoplada. Haga clic en MOX para desactivar la transmisión, luego ejecute el ATU o verifique la línea de bajada antes de continuar. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- **El medidor RF Pwr llega al fondo de escala** — El control deslizante RF Power está configurado demasiado alto para la antena y el amplificador conectados. Haga clic en MOX para desactivar la transmisión, luego reduzca el control deslizante RF Power antes de volver a activar.
- **El botón ATU inicia una nueva sintonía en lugar de derivar** — La frecuencia de transmisión cambió desde la última sintonía exitosa. Esto es lo esperado. El botón solo cambiará a bypass cuando la frecuencia actual coincida con la frecuencia en la que el ATU reportó por última vez una sintonía exitosa.
- **Los botones ATU y MEM aparecen atenuados** — O la radio no tiene acoplador de antena instalado (p. ej., un Hermes-Lite 2), o el amplificador externo TGXL está en modo OPERATE. Pase el cursor sobre cualquiera de los botones para ver qué razón aplica. Si el TGXL está en modo OPERATE, sáquelo de OPERATE antes de usar el acoplador interno.
- **Los tonos Quindar se reproducen inesperadamente al hacer clic en MOX** — El chip QUIN está habilitado en la tira de canales de audio y la tajada TX está en un modo de teléfono. Si no desea tonos Quindar durante esta prueba, deshabilite el chip QUIN en la tira de canales de audio antes de activar la transmisión.

## Relacionados

- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria ATU](recall-an-atu-memory.md)
- Pre-sintonizar bandas para el ATU
- Borrar memorias ATU

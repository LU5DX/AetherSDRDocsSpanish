# Alternar MOX para activar manualmente el transmisor

MOX le permite activar el transmisor sin un pedal o una línea PTT. Úselo para verificar audio, probar su señal o transmitir cuando el PTT por hardware no esté disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. MOX no tiene efecto cuando la radio está fuera de línea.
- Confirme que su perfil de TX y el nivel de potencia de RF estén configurados correctamente antes de activar la transmisión.
- Si tiene habilitados los tonos Quindar en la tira de canales de audio, los tonos K y BK se reproducirán automáticamente al activar y desactivar MOX en modos de teléfono. No se requiere configuración adicional.

## Pasos

1. Si el applet de controles de TX no está visible, haga clic en el botón de bandeja **TX** en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para activar el transmisor. El botón se pone rojo mientras TX está activo.
4. Haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado de reposo con un borde y texto de acento ámbar, distinguiéndolo de los botones TUNE, ATU y MEM.

## Qué hace cada control

| Control                                        | Comportamiento                                                                                                                                                                                                                                                                 | Predeterminado |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| **MOX**                                        | Alterna la transmisión manual activada o desactivada. El botón se pone rojo mientras el transmisor está activado. En el estado de reposo, el botón tiene un borde y texto de acento ámbar para distinguirlo de los botones vecinos TUNE, ATU y MEM. El clic pasa por el coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar en modos de teléfono cuando Quindar está habilitado en la tira de canales de audio. | Desactivado |
| **RF Power**                                   | Establece el nivel de potencia de RF de transmisión enviado a la radio (0–100 % del máximo). Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor actual en porcentaje (p. ej., "50 %"). Al soltar el control deslizante, el valor se sincroniza de vuelta a la radio.                                            | 100     |
| **Tune Pwr**                                   | Establece el nivel de potencia de la portadora de sintonía (0–100 % del máximo). Mientras arrastra el control deslizante, una información sobre herramientas muestra el valor actual en porcentaje (p. ej., "10 %"). Al soltar el control deslizante, el valor se sincroniza de vuelta a la radio.                                                             | 10      |
| **Medidor RF Pwr**                               | Muestra la potencia directa en la salida del excitador. Se pone rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). La barra de retención de pico mantiene la lectura máxima de PEP durante 2 segundos y luego decae al nivel de potencia actual a una velocidad de 48 W/s (escalada proporcionalmente para el excitador Aurora 500W). Pase el mouse sobre el medidor para ver la lectura exacta de vatios en una ventana emergente (p. ej., "75 W"). El medidor y la retención de pico se restablecen a 0 inmediatamente cuando desactiva la transmisión. | —       |
| **Medidor SWR**                                  | Muestra la relación de onda estacionaria en el excitador. Se pone rojo por encima de 2.5. Pase el mouse sobre el medidor para ver la lectura exacta de la relación en una ventana emergente (p. ej., "1.42:1"). El medidor se mantiene en 1.0 cuando no se transmite o cuando los datos de SWR no están disponibles.                                    | —       |
| **Perfil de TX**                                 | Selecciona un perfil de TX de los cargados en la radio.                                                                                                                                                                                                                           | —       |
| **TUNE**                                       | Inicia o detiene la portadora de sintonía. El texto del botón cambia a **TUNING...** con un fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora (tono único o dos tonos) para el siguiente ciclo de sintonía. Esta selección es de un solo uso y no se conserva entre ciclos de encendido.        | TUNE    |
| **ATU**                                        | Inicia un ciclo de sintonía del ATU. Se deshabilita cuando la radio no tiene sintonizador de antena o cuando TGXL está en modo OPERATE. Haga clic derecho para abrir un menú contextual con las opciones **Pre-tune bands…** y **Clear ATU memories…** (consulte el comportamiento del botón ATU a continuación).                                       | —       |
| **MEM**                                        | Alterna el recuerdo de memoria del ATU activado o desactivado. Se deshabilita cuando la radio no tiene sintonizador de antena o cuando TGXL está en modo OPERATE.                                                                                                                                                            | Desactivado |
| **Indicadores ATU** (Success, Byp, Mem)         | **Success** se enciende en verde cuando el estado del ATU es Successful u OK. **Byp** se enciende en naranja cuando el ATU está en Bypass o ManualBypass. **Mem** se enciende en verde cuando el ATU está usando una memoria.                                                                                                    | Atenuado |
| **APD**                                        | Alterna la predistorsión adaptativa en la radio.                                                                                                                                                                                                                                  | Desactivado |
| **Indicadores de estado APD** (Active, Cal, Avail) | **Active** se enciende en verde cuando APD está activado y el ecualizador se aplica activamente. **Cal** se enciende en verde cuando APD está activado y aún está calibrando. **Avail** se enciende en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.                                             | Atenuado |

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón **ATU** alterna entre iniciar un ciclo de sintonía y derivar el sintonizador, coincidiendo con el comportamiento por frecuencia de SmartSDR.

El botón sigue esta lógica cada vez que hace clic en él:

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia, después de una sintonía exitosa** — cambia el ATU a derivación.
- **Cualquier clic después de un cambio de frecuencia** — inicia un ciclo de sintonía nuevo, incluso si la sintonía anterior fue exitosa.

Entrar en derivación borra la frecuencia sintonizada recordada, por lo que el siguiente clic siempre inicia un ciclo de sintonía nuevo.

Los botones **ATU** y **MEM** se deshabilitan cuando TGXL está en modo OPERATE. También se deshabilitan por completo cuando la radio conectada no tiene sintonizador de antena (por ejemplo, una Hermes-Lite 2). Cuando están deshabilitados, pasar el mouse sobre cualquiera de los botones muestra el motivo: "This radio has no antenna tuner" o "Disabled — TGXL is in OPERATE mode".

### Menú contextual de clic derecho del ATU

Al hacer clic derecho en el botón **ATU** se abre un menú contextual con dos opciones:

- **Pre-tune bands…** — Abre el diálogo de pre-sintonía del ATU para realizar un barrido en las bandas seleccionadas. Esta opción solo está disponible cuando MEM está habilitado. Si MEM está desactivado, la opción aparece atenuada con una información sobre herramientas: "Enable MEM before running the pre-tune sweep."
- **Clear ATU memories…** — Abre un diálogo de confirmación. Al hacer clic en Yes se borran todas las memorias del ATU almacenadas en la radio.

## Menú de clic derecho de TUNE

Al hacer clic derecho en el botón **TUNE** se abre un menú contextual para seleccionar la forma de la portadora para el siguiente ciclo de sintonía:

- **Mono Tone** — Una portadora de tono único.
- **Two Tone** — Señal de prueba de dos tonos.

La selección es de un solo uso y se aplica solo a la siguiente pulsación del botón Tune. El modo de sintonía de la radio vuelve a tono único entre ciclos de encendido; AetherSDR no conserva esta elección en AppSettings.

## Consejos

- Observe los medidores **RF Pwr** y **SWR** tan pronto como active MOX. Si el SWR supera 2.5 (zona roja), desactive la transmisión inmediatamente e investigue su sistema de antena.
- Establezca **RF Power** en un valor bajo antes de usar MOX por primera vez en una banda nueva.
- MOX activa la radio a potencia completa en el modo que esté activo. Si solo necesita verificar el SWR o sintonizar un ATU, use **TUNE** en su lugar — transmite una portadora al nivel más bajo de **Tune Pwr**.
- Después de una sintonía exitosa del ATU, hacer clic en **ATU** nuevamente en la misma frecuencia pone el sintonizador en derivación. Para re-sintonizar después de cambiar de banda o frecuencia, simplemente haga clic en **ATU** una vez en la frecuencia nueva.
- Mientras arrastra el control deslizante de **RF Power** o **Tune Pwr**, una información sobre herramientas muestra el valor actual en porcentaje para ayudarle a establecer su nivel deseado con precisión. El valor se sincroniza con la radio cuando suelta el control deslizante.
- Pase el mouse sobre el medidor **RF Pwr** o **SWR** para ver una lectura exacta en una ventana emergente (p. ej., "75 W" para potencia o "1.42:1" para SWR), lo que le ayuda a leer valores precisos sin estimar entre marcas.
- Si los tonos Quindar están habilitados en la tira de canales de audio, cambiar a un modo digital o CW suprime los tonos K/BK automáticamente. MOX en sí se comporta igual independientemente del modo.
- La barra de retención de pico en el medidor **RF Pwr** mantiene la lectura máxima durante 2 segundos y luego decae al nivel de potencia actual. El pico se borra inmediatamente cuando desactiva la transmisión.
- Los controles deslizantes de potencia y potencia de sintonía ahora usan un estilo que respeta el tema. El color de relleno del control deslizante sigue el color de primer plano del control deslizante del tema configurado. Las etiquetas de texto usan los colores de texto primario y secundario del tema para una mejor legibilidad en temas claros y oscuros.
- El acento de reposo del botón MOX (borde y texto ámbar) es editable en el Editor de temas bajo `color.tx.mox.*`, lo que le permite personalizar su apariencia para que coincida con su configuración de operación.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR esté conectado a la radio. El applet de controles de TX requiere una conexión activa con la radio.
- **El transmisor se activa pero no se muestra potencia de RF** — Verifique que **RF Power** no esté en 0 % y que el perfil de TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX una segunda vez** — Otra fuente de PTT (pedal, VOX, comando CAT) puede estar manteniendo la radio activada. Verifique el hardware PTT externo y cualquier cliente CAT conectado.
- **El botón ATU inicia una sintonía nueva en lugar de derivar** — La frecuencia de transmisión ha cambiado desde la última sintonía exitosa. El botón ATU siempre iniciará un ciclo de sintonía nuevo cuando la frecuencia difiera de la frecuencia en la que el sintonizador reportó por última vez una coincidencia exitosa.
- **Los botones ATU y MEM están atenuados** — La radio conectada puede no tener un sintonizador de antena interno, o el TGXL puede estar en modo OPERATE. Pase el mouse sobre cualquiera de los botones para ver el motivo específico mostrado como información sobre herramientas.
- **Los tonos Quindar no se reproducen al hacer clic en MOX** — Confirme que el chip QUIN esté habilitado en la tira de canales de audio y que la franja TX activa esté en un modo de teléfono (SSB, AM, FM). Los tonos Quindar no se generan en modos CW o digitales.
- **La opción Pre-tune bands está atenuada** — Habilite primero el botón **MEM**. El barrido de pre-sintonía requiere que las memorias del ATU estén activas.

## Relacionado

- [Descripción general de controles de TX](overview.md)
- [Iniciar una portadora de sintonía para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Haga su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)

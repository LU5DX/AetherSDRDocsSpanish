# Alternar MOX para activar manualmente el transmisor

MOX le permite activar el transmisor sin necesidad de un pedal de PTT o una línea PTT. Úselo para verificar audio, probar su señal o transmitir cuando no haya PTT por hardware disponible.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. MOX no tiene ningún efecto cuando la radio está fuera de línea.
- Confirme que su perfil de TX y el nivel de potencia de RF estén configurados correctamente antes de activar la transmisión.
- En v26.7.4, si tiene los tonos Quindar habilitados en la tira de canal de audio (Audio Channel Strip), los tonos K y BK se reproducirán automáticamente al activar y desactivar MOX en modos de teléfono. No se requiere configuración adicional.

## Pasos

1. Si el applet de controles de TX no está visible, haga clic en el botón de la bandeja **TX** en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para activar el transmisor. El botón se vuelve rojo mientras la TX está activa.
4. Haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado inactivo con un borde y texto de acento ámbar, distinguiéndolo de los botones TUNE, ATU y MEM.

## Qué hace cada control

| Control                                        | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                                           | Predeterminado |
|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **MOX**                                        | Alterna la transmisión manual activada o desactivada. El botón se vuelve rojo mientras el transmisor está activado. En el estado inactivo, el botón tiene un borde y texto de acento ámbar para distinguirlo de los botones vecinos TUNE, ATU y MEM. El clic pasa a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar en modos de teléfono cuando Quindar está habilitado en la tira de canal de audio (Audio Channel Strip). | Desactivado    |
| **RF Power**                                   | Establece el nivel de potencia de RF de transmisión enviado a la radio (0–100% del máximo). Al arrastrar el control deslizante, un tooltip muestra el valor actual en porcentaje (ej., "50%"). Al soltar el control deslizante, el valor se sincroniza de vuelta a la radio.                                                                                                                                                               | 100            |
| **Tune Pwr**                                   | Establece el nivel de potencia de la portadora de sintonía (0–100% del máximo). Al arrastrar el control deslizante, un tooltip muestra el valor actual en porcentaje (ej., "10%"). Al soltar el control deslizante, el valor se sincroniza de vuelta a la radio.                                                                                                                                                                           | 10             |
| **RF Pwr** meter                               | Muestra la potencia directa en la salida del excitador. Se vuelve rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). La barra de retención de pico mantiene la lectura máxima de PEP durante 2 segundos, luego disminuye al nivel de potencia actual a una tasa de 48 W/s (escalada proporcionalmente para el excitador Aurora 500W). Pase el ratón sobre el indicador para ver la lectura exacta de vatios en una ventana emergente (ej., "75 W"). | —              |
| **SWR** meter                                  | Muestra la relación de onda estacionaria en el excitador. Se vuelve rojo por encima de 2.5. Pase el ratón sobre el indicador para ver la relación exacta en una ventana emergente (ej., "1.42:1").                                                                                                                                                                                                                                         | —              |
| **TX Profile**                                 | Selecciona un perfil de TX de los cargados en la radio.                                                                                                                                                                                                                                                                                                                                                                                  | —              |
| **TUNE**                                       | Inicia o detiene la portadora de sintonía. El texto del botón cambia a **TUNING...** con un fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora (Mono Tone o Two Tone) para el próximo ciclo de sintonía. Esta selección es de un solo uso y no persiste entre ciclos de encendido.                                                                                                                | TUNE           |
| **ATU**                                        | Inicia un ciclo de sintonía del ATU. Haga clic derecho para abrir un menú contextual con las opciones **Pre-tune bands…** y **Clear ATU memories…** (consulte el comportamiento del botón ATU a continuación).                                                                                                                                                                                                                              | —              |
| **MEM**                                        | Alterna la memoria del ATU activada o desactivada. Deshabilitado cuando TGXL está en modo OPERATE.                                                                                                                                                                                                                                                                                                                                       | Desactivado    |
| **Indicadores ATU** (Success, Byp, Mem)        | **Success** se ilumina en verde cuando el estado del ATU es Successful u OK. **Byp** se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. **Mem** se ilumina en verde cuando el ATU está usando una memoria.                                                                                                                                                                                                                  | Atenuado       |
| **APD**                                        | Alterna la predistorsión adaptativa en la radio.                                                                                                                                                                                                                                                                                                                                                                                         | Desactivado    |
| **Indicadores de estado APD** (Active, Cal, Avail) | **Active** se ilumina en verde cuando APD está activado y el ecualizador se aplica de forma activa. **Cal** se ilumina en verde cuando APD está activado y aún se está calibrando. **Avail** se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.                                                                                                                                            | Atenuado       |

## Comportamiento del botón ATU

A partir de v0.9.5.1, el botón **ATU** alterna entre iniciar un ciclo de sintonía y omitir el sintonizador, coincidiendo con el comportamiento por frecuencia de SmartSDR.

El botón sigue esta lógica cada vez que hace clic en él:

- **Primer clic en una nueva frecuencia** — inicia un ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia, después de una sintonía exitosa** — cambia el ATU a bypass.
- **Cualquier clic después de un cambio de frecuencia** — inicia un nuevo ciclo de sintonía, incluso si la sintonía anterior fue exitosa.

Entrar en bypass borra la frecuencia sintonizada recordada, por lo que el siguiente clic siempre inicia un nuevo ciclo de sintonía.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

### Menú contextual de clic derecho del ATU

Al hacer clic derecho en el botón **ATU** se abre un menú contextual con dos opciones:

- **Pre-tune bands…** — Abre el diálogo de pre-sintonía del ATU para ejecutar un barrido en las bandas seleccionadas. Esta opción solo está disponible cuando MEM está habilitado. Si MEM está desactivado, la opción aparece atenuada con un tooltip: "Habilite MEM antes de ejecutar el barrido de pre-sintonía."
- **Clear ATU memories…** — Abre un diálogo de confirmación. Al hacer clic en Yes se borran todas las memorias del ATU almacenadas en la radio.

## Menú de clic derecho de TUNE

Al hacer clic derecho en el botón **TUNE** se abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía:

- **Mono Tone** — Una portadora de un solo tono.
- **Two Tone** — Señal de prueba de dos tonos.

La selección es de un solo uso que se aplica solo a la siguiente pulsación del botón Tune. El modo de sintonía de la radio vuelve a un solo tono entre ciclos de encendido; AetherSDR no persiste esta selección en AppSettings.

## Consejos

- Observe los medidores **RF Pwr** y **SWR** tan pronto como active MOX. Si la SWR supera 2.5 (zona roja), desactive la transmisión inmediatamente e investigue su sistema de antena.
- Establezca **RF Power** en un valor bajo antes de usar MOX por primera vez en una nueva banda.
- MOX activa la radio para transmitir a plena potencia en el modo que esté activo. Si solo necesita verificar la SWR o sintonizar un ATU, use **TUNE** en su lugar: transmite una portadora al nivel más bajo de **Tune Pwr**.
- Después de una sintonía exitosa del ATU, haga clic en **ATU** nuevamente en la misma frecuencia para poner el sintonizador en bypass. Para volver a sintonizar después de cambiar de bandas o frecuencias, simplemente haga clic en **ATU** una vez en la nueva frecuencia.
- Mientras arrastra el control deslizante **RF Power** o **Tune Pwr**, un tooltip muestra el valor actual en porcentaje para ayudarle a establecer su nivel deseado con precisión. El valor se sincroniza con la radio cuando suelta el control deslizante.
- Pase el ratón sobre el indicador **RF Pwr** o **SWR** para ver una lectura exacta en una ventana emergente (ej., "75 W" para potencia o "1.42:1" para SWR), lo que le ayuda a leer valores precisos sin tener que estimar entre marcas.
- Si los tonos Quindar están habilitados en la tira de canal de audio (Audio Channel Strip), al cambiar a un modo digital o CW se suprimen automáticamente los tonos K/BK. MOX se comporta igual independientemente del modo.
- La barra de retención de pico del medidor **RF Pwr** mantiene la lectura máxima durante 2 segundos, luego disminuye al nivel de potencia actual. El pico se borra inmediatamente cuando desactiva la transmisión.
- Los controles deslizantes de potencia y potencia de sintonía ahora usan un estilo que reconoce el tema. El color de relleno del control deslizante sigue el color de primer plano del control deslizante del tema configurado. Las etiquetas de texto usan los colores de texto primario y secundario del tema para una mejor legibilidad en temas claros y oscuros.
- El acento del botón MOX en estado inactivo (borde y texto ámbar) se puede editar en el Editor de Temas bajo `color.tx.mox.*`, lo que le permite personalizar su apariencia para adaptarla a su configuración de operación.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR esté conectado a la radio. El applet de controles de TX requiere una conexión de radio activa.
- **El transmisor se activa pero no se muestra potencia de RF** — Verifique que **RF Power** no esté en 0% y que el perfil de TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente de PTT (pedal, VOX, comando CAT) podría estar manteniendo la radio activada. Verifique el hardware de PTT externo y cualquier cliente CAT conectado.
- **El botón ATU inicia una nueva sintonía en lugar de aplicar bypass** — La frecuencia de transmisión ha cambiado desde la última sintonía exitosa. El botón ATU siempre iniciará un nuevo ciclo de sintonía cuando la frecuencia difiera de la frecuencia en la que el sintonizador reportó por última vez una coincidencia exitosa.
- **Los tonos Quindar no se reproducen al hacer clic en MOX** — Confirme que el chip QUIN esté habilitado en la tira de canal de audio (Audio Channel Strip) y que el slice de TX activo esté en un modo de teléfono (SSB, AM, FM). Los tonos Quindar no se generan en modos CW o digitales.
- **La opción de pre-sintonía de bandas aparece atenuada** — Habilite primero el botón **MEM**. El barrido de pre-sintonía requiere que las memorias del ATU estén activas.

## Relacionados

- [Resumen de controles de TX](overview.md)
- [Iniciar una portadora de sintonía para verificar la SWR](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Haga su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)

# Alternar MOX para activar manualmente el transmisor

MOX le permite activar el transmisor sin un pedal de interruptor o una línea PTT. Úselo para verificar audio, probar su señal o transmitir cuando el PTT por hardware no esté disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. MOX no tiene efecto cuando la radio está desconectada.
- Confirme que su perfil TX y el nivel de potencia RF estén configurados correctamente antes de activar la transmisión.
- En v0.9.7, si tiene los tonos Quindar habilitados en la tira de canal de audio, los tonos K y BK se reproducirán automáticamente al activar y desactivar MOX en modos de fonía. No se requiere configuración adicional.

## Pasos

1. Si el applet Controles TX no está visible, haga clic en el botón de la bandeja **TX** en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para activar el transmisor. El botón se vuelve rojo mientras TX esté activo.
4. Haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado sin iluminación.

## Qué hace cada control

| Control                                        | Comportamiento                                                                                                                                                                                                                                                                         | Predeterminado |
|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **MOX**                                        | Alterna la transmisión manual activada o desactivada. El botón se vuelve rojo mientras el transmisor está activado. En v0.9.7, el clic se enruta a través del coordinador de tonos Quindar, por lo que los tonos K/BK se reproducen al activar/desactivar en modos de fonía cuando Quindar está habilitado en la tira de canal de audio. | Desactivado    |
| **RF Power**                                   | Establece el nivel de potencia RF de transmisión enviado a la radio. Al arrastrar el control deslizante, un tooltip muestra el valor actual en vatios (p. ej., "50 W").                                                                                                                | 100            |
| **Tune Pwr**                                   | Establece el nivel de potencia de la portadora de sintonía. Al arrastrar el control deslizante, un tooltip muestra el valor actual en vatios (p. ej., "10 W").                                                                                                                          | 10             |
| Medidor **RF Pwr**                             | Muestra la potencia directa en la salida del excitador. Se vuelve rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). La barra de retención de pico mantiene la lectura máxima de PEP durante 2 segundos, luego disminuye al nivel de potencia actual a una tasa de 48 W/s (escalada proporcionalmente para el excitador Aurora 500W). | —              |
| Medidor **SWR**                                | Muestra la relación de onda estacionaria en el excitador. Se vuelve rojo por encima de 2.5.                                                                                                                                                                                             | —              |
| **TX Profile**                                 | Selecciona un perfil TX de los cargados en la radio.                                                                                                                                                                                                                                   | —              |
| **TUNE**                                       | Inicia o detiene la portadora de sintonía. El texto del botón se convierte en **TUNING...** con fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora (Mono Tone o Two Tone) para el siguiente ciclo de sintonía. Esta selección es de un solo uso y no se conserva entre ciclos de encendido. | TUNE           |
| **ATU**                                        | Inicia un ciclo de sintonía del ATU. Haga clic derecho para abrir un menú contextual con las opciones **Pre-tune bands…** y **Clear ATU memories…** (consulte el comportamiento del botón ATU a continuación).                                                                          | —              |
| **MEM**                                        | Alterna la recuperación de memoria del ATU activada o desactivada. Deshabilitado cuando TGXL está en modo OPERATE.                                                                                                                                                                      | Desactivado    |
| **Indicadores ATU** (Success, Byp, Mem)        | **Success** se ilumina en verde cuando el estado del ATU es Successful u OK. **Byp** se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. **Mem** se ilumina en verde cuando el ATU está usando una memoria.                                                               | Atenuado       |
| **APD**                                        | Alterna la predistorsión adaptativa en la radio.                                                                                                                                                                                                                                        | Desactivado    |
| **Indicadores de estado APD** (Active, Cal, Avail) | **Active** se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente. **Cal** se ilumina en verde cuando APD está activado y aún está calibrando. **Avail** se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada. | Atenuado       |

## Comportamiento del botón ATU

A partir de v0.9.5.1, el botón **ATU** alterna entre iniciar un ciclo de sintonía y omitir el sintonizador, coincidiendo con el comportamiento por frecuencia de SmartSDR.

El botón sigue esta lógica cada vez que hace clic en él:

- **Primer clic en una nueva frecuencia** — inicia un ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia, después de una sintonía exitosa** — cambia el ATU a bypass.
- **Cualquier clic después de un cambio de frecuencia** — inicia un nuevo ciclo de sintonía, incluso si la sintonía anterior fue exitosa.

Al entrar en bypass se borra la frecuencia sintonizada recordada, por lo que el siguiente clic siempre inicia un nuevo ciclo de sintonía.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

### Menú contextual del botón derecho ATU

Al hacer clic derecho en el botón **ATU** se abre un menú contextual con dos opciones:

- **Pre-tune bands…** — Abre el diálogo de presintonía del ATU para realizar un barrido en las bandas seleccionadas. Esta opción solo está disponible cuando MEM está habilitado. Si MEM está desactivado, la opción aparece atenuada con un tooltip: "Enable MEM before running the pre-tune sweep."
- **Clear ATU memories…** — Abre un diálogo de confirmación. Al hacer clic en Sí, se borran todas las memorias del ATU almacenadas en la radio.

## Menú contextual del botón derecho TUNE

Al hacer clic derecho en el botón **TUNE** se abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía:

- **Mono Tone** — Una portadora de tono único.
- **Two Tone** — Señal de prueba de dos tonos.

La selección es de un solo uso y se aplica solo a la siguiente pulsación del botón TUNE. El modo de sintonía de la radio vuelve al tono único entre ciclos de encendido; AetherSDR no conserva esta elección en AppSettings.

## Consejos

- Observe los medidores **RF Pwr** y **SWR** tan pronto como active MOX. Si la ROE supera 2.5 (zona roja), desactive inmediatamente e investigue su sistema de antena.
- Configure **RF Power** en un valor bajo antes de usar MOX por primera vez en una nueva banda.
- MOX activa la radio para transmitir a máxima potencia en el modo que esté activo. Si solo necesita verificar la ROE o sintonizar un ATU, use **TUNE** en su lugar: transmite una portadora al nivel más bajo de **Tune Pwr**.
- Después de una sintonización exitosa del ATU, al hacer clic en **ATU** nuevamente en la misma frecuencia, el sintonizador se pone en bypass. Para volver a sintonizar después de cambiar de banda o frecuencia, simplemente haga clic en **ATU** una vez en la nueva frecuencia.
- Mientras arrastra el control deslizante de **RF Power** o **Tune Pwr**, un tooltip muestra el valor actual en vatios para ayudarle a establecer su nivel deseado con precisión.
- Si los tonos Quindar están habilitados en la tira de canal de audio, al cambiar a un modo digital o CW se suprimen automáticamente los tonos K/BK. MOX se comporta igual independientemente del modo.
- La barra de retención de pico en el medidor **RF Pwr** mantiene la lectura máxima durante 2 segundos, luego disminuye al nivel de potencia actual. El pico se borra inmediatamente al desactivar la transmisión.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR esté conectado a la radio. El applet Controles TX requiere una conexión de radio activa.
- **El transmisor se activa pero no se muestra potencia RF** — Verifique que **RF Power** no esté configurado en 0 y que el perfil TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente de PTT (pedal, VOX, comando CAT) puede estar manteniendo la radio activada. Verifique el hardware PTT externo y cualquier cliente CAT conectado.
- **El botón ATU inicia una nueva sintonía en lugar de pasar a bypass** — La frecuencia de transmisión ha cambiado desde la última sintonía exitosa. El botón ATU siempre iniciará un nuevo ciclo de sintonía cuando la frecuencia difiera de la frecuencia en la que el sintonizador reportó por última vez una coincidencia exitosa.
- **Los tonos Quindar no se reproducen al hacer clic en MOX** — Confirme que el chip QUIN esté habilitado en la tira de canal de audio y que el slice TX activo esté en un modo de fonía (SSB, AM, FM). Los tonos Quindar no se generan en modos CW o digitales.
- **La opción Pre-tune bands aparece atenuada** — Active primero el botón **MEM**. El barrido de presintonía requiere que las memorias del ATU estén activas.

## Relacionado

- [Descripción general de Controles TX](overview.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Configurar la potencia de salida RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Haga su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)

# Activar MOX para poner manualmente el transmisor en funcionamiento

MOX le permite poner el transmisor en funcionamiento sin un pulsador de pedal ni una línea PTT. Úselo para verificar audio, probar su señal o transmitir cuando no haya PTT por hardware disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. MOX no tiene efecto cuando la radio está fuera de línea.
- Confirme que su perfil de TX y el nivel de potencia de RF estén configurados correctamente antes de activar la transmisión.
- En la versión 26.6.1, si tiene los tonos Quindar habilitados en la tira de canales de audio (Audio Channel Strip), los tonos K y BK se reproducirán automáticamente al activar y desactivar MOX en modos de telefonía. No se requiere configuración adicional.

## Pasos

1. Si el applet de controles de TX (TX Controls) no está visible, haga clic en el botón de la bandeja **TX** en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para activar el transmisor. El botón se vuelve rojo mientras TX está activo.
4. Haga clic en **MOX** nuevamente para desactivar el transmisor. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control                                        | Comportamiento                                                                                                                                                                                                                                                                                                       | Predeterminado |
|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **MOX**                                        | Alterna la transmisión manual activada o desactivada. El botón se vuelve rojo mientras el transmisor está activo. En la versión 26.6.1, el clic pasa por el coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar en modos de telefonía cuando Quindar está habilitado en la tira de canales de audio (Audio Channel Strip). | Apagado        |
| **RF Power**                                   | Establece el nivel de potencia de RF de transmisión enviado a la radio (0–100 % del máximo). Al arrastrar el control deslizante, una información sobre herramientas muestra el valor actual en porcentaje (p. ej., "50 %").                                                                                             | 100            |
| **Tune Pwr**                                   | Establece el nivel de potencia de la portadora de sintonía (0–100 % del máximo). Al arrastrar el control deslizante, una información sobre herramientas muestra el valor actual en porcentaje (p. ej., "10 %").                                                                                                      | 10             |
| Medidor **RF Pwr**                             | Muestra la potencia directa en la salida del excitador. Se vuelve rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). La barra de retención de pico mantiene la lectura máxima de PEP durante 2 segundos, luego decae al nivel de potencia actual a una velocidad de 48 W/s (escalada proporcionalmente para el excitador Aurora 500W). | —              |
| Medidor **SWR**                                | Muestra la relación de onda estacionaria en el excitador. Se vuelve rojo por encima de 2.5.                                                                                                                                                                                                                          | —              |
| **TX Profile**                                 | Selecciona un perfil de TX de los cargados en la radio.                                                                                                                                                                                                                                                              | —              |
| **TUNE**                                       | Inicia o detiene la portadora de sintonía. El texto del botón cambia a **TUNING...** con un fondo rojo mientras está activo. Haga clic derecho para seleccionar la forma de la portadora (Mono Tone o Two Tone) para el próximo ciclo de sintonía. Esta selección es de un solo uso y no se conserva entre ciclos de encendido. | TUNE           |
| **ATU**                                        | Inicia un ciclo de sintonía del ATU. Haga clic derecho para abrir un menú contextual con las opciones **Pre-tune bands…** y **Clear ATU memories…** (consulte el comportamiento del botón ATU a continuación).                                                                                                       | —              |
| **MEM**                                        | Alterna la recuperación de memoria del ATU activada o desactivada. Deshabilitado cuando TGXL está en modo OPERATE.                                                                                                                                                                                                   | Apagado        |
| **Indicadores ATU** (Success, Byp, Mem)        | **Success** se ilumina en verde cuando el estado del ATU es Successful u OK. **Byp** se ilumina en naranja cuando el ATU está en Bypass o ManualBypass. **Mem** se ilumina en verde cuando el ATU está usando una memoria.                                                                                            | Atenuado       |
| **APD**                                        | Alterna la predistorsión adaptativa en la radio.                                                                                                                                                                                                                                                                     | Apagado        |
| **Indicadores de estado APD** (Active, Cal, Avail) | **Active** se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente. **Cal** se ilumina en verde cuando APD está activado y aún está calibrando. **Avail** se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no se ha aplicado.                     | Atenuado       |

## Comportamiento del botón ATU

A partir de la versión 0.9.5.1, el botón **ATU** alterna entre iniciar un ciclo de sintonía y omitir el sintonizador, coincidiendo con el comportamiento por frecuencia de SmartSDR.

El botón sigue esta lógica cada vez que hace clic en él:

- **Primer clic en una nueva frecuencia** — inicia un ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia, después de una sintonización exitosa** — cambia el ATU a bypass.
- **Cualquier clic después de un cambio de frecuencia** — inicia un nuevo ciclo de sintonía, incluso si la sintonización anterior fue exitosa.

Al entrar en bypass se borra la frecuencia sintonizada recordada, por lo que el siguiente clic siempre inicia un nuevo ciclo de sintonía.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL está en modo OPERATE.

### Menú contextual del botón ATU (clic derecho)

Al hacer clic derecho en el botón **ATU** se abre un menú contextual con dos opciones:

- **Pre-tune bands…** — Abre el diálogo de pre-sintonía del ATU para ejecutar un barrido en las bandas seleccionadas. Esta opción solo está disponible cuando MEM está habilitado. Si MEM está desactivado, la opción aparece atenuada con una información sobre herramientas: "Enable MEM before running the pre-tune sweep."
- **Clear ATU memories…** — Abre un diálogo de confirmación. Al hacer clic en Yes se borran todas las memorias del ATU almacenadas en la radio.

## Menú de clic derecho de TUNE

Al hacer clic derecho en el botón **TUNE** se abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía:

- **Mono Tone** — Una portadora de tono único.
- **Two Tone** — Señal de prueba de dos tonos.

La selección es de un solo uso y se aplica solo a la siguiente pulsación del botón Tune. El modo de sintonía de la radio vuelve al tono único entre ciclos de encendido; AetherSDR no conserva esta elección en AppSettings.

## Consejos

- Observe los medidores **RF Pwr** y **SWR** tan pronto como active MOX. Si la SWR supera 2.5 (zona roja), desactive la transmisión inmediatamente e investigue su sistema de antena.
- Establezca **RF Power** en un valor bajo antes de usar MOX por primera vez en una nueva banda.
- MOX activa la radio para transmitir a máxima potencia en el modo que esté activo. Si solo necesita verificar la SWR o sintonizar un ATU, use **TUNE** en su lugar: transmite una portadora al nivel inferior de **Tune Pwr**.
- Después de una sintonización exitosa del ATU, al hacer clic en **ATU** nuevamente en la misma frecuencia, el sintonizador se pone en bypass. Para volver a sintonizar después de cambiar de banda o frecuencia, simplemente haga clic en **ATU** una vez en la nueva frecuencia.
- Mientras arrastra el control deslizante de **RF Power** o **Tune Pwr**, una información sobre herramientas muestra el valor actual en porcentaje para ayudarle a establecer su nivel deseado con precisión.
- Si los tonos Quindar están habilitados en la tira de canales de audio (Audio Channel Strip), al cambiar a un modo digital o CW se suprimen automáticamente los tonos K/BK. MOX se comporta igual independientemente del modo.
- La barra de retención de pico en el medidor **RF Pwr** mantiene la lectura máxima durante 2 segundos, luego decae al nivel de potencia actual. El pico se borra inmediatamente cuando desactiva la transmisión.
- Los controles deslizantes de potencia y potencia de sintonía ahora usan un estilo que respeta el tema. El color de relleno del control deslizante sigue el color de primer plano del control deslizante del tema configurado. Las etiquetas de texto usan los colores de texto primario y secundario del tema para una mejor legibilidad en temas claros y oscuros.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR esté conectado a la radio. El applet de controles de TX (TX Controls) requiere una conexión de radio activa.
- **El transmisor se activa pero no se muestra potencia de RF** — Verifique que **RF Power** no esté configurado al 0% y que el perfil de TX correcto esté cargado en el selector **TX Profile**.
- **La radio permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente de PTT (pulsador de pedal, VOX, comando CAT) puede estar manteniendo la radio activada. Revise el hardware PTT externo y cualquier cliente CAT conectado.
- **El botón ATU inicia una nueva sintonía en lugar de poner en bypass** — La frecuencia de transmisión ha cambiado desde la última sintonización exitosa. El botón ATU siempre iniciará un nuevo ciclo de sintonía cuando la frecuencia difiera de la frecuencia en la que el sintonizador informó por última vez una coincidencia exitosa.
- **Los tonos Quindar no se reproducen al hacer clic en MOX** — Confirme que el chip QUIN esté habilitado en la tira de canales de audio (Audio Channel Strip) y que el slice de TX activo esté en un modo de telefonía (SSB, AM, FM). Los tonos Quindar no se generan en modos CW o digitales.
- **La opción Pre-tune bands está atenuada** — Habilite primero el botón **MEM**. El barrido de pre-sintonía requiere que las memorias del ATU estén activas.

## Relacionado

- [Descripción general de los controles de TX](overview.md)
- [Iniciar una portadora de sintonía para verificar la SWR](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Realice su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)

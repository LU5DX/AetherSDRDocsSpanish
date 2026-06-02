# Iniciar una portadora de sintonía para verificar la ROE

Envía una portadora continua a potencia reducida para leer la ROE de su sistema de antena. Utilícelo antes de un QSO o después de cambiar de antena para confirmar una buena adaptación.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet de Controles de TX solo está activo con una conexión activa al equipo.
- Asegúrese de tener autorización para transmitir en la frecuencia (la banda debe estar legalmente abierta para su estación).
- Ajuste la potencia de sintonía a un nivel adecuado para su sistema de antena. El valor predeterminado es 10; consulte [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón de la bandeja TX en la barra lateral derecha para abrir el applet de Controles de TX si aún no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic con el botón derecho en el botón **TUNE** para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Elija **Mono Tone** o **Two Tone** en el menú contextual. El modo de sintonía del equipo es transitorio: AetherSDR no conserva la selección.
4. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora esté activa.
   - El indicador **SWR** (ROE) se actualiza en tiempo real. La escala va de 1.0 a 3.0; las lecturas superiores a 2.5 se muestran en rojo.
   - El indicador **RF Pwr** muestra la potencia directa a la salida del excitador. Una barra de retención de pico rastrea la potencia de pico de la envolvente (PEP) durante 2 segundos, luego decae hacia la lectura actual.
5. Lea el valor de ROE del indicador **SWR**.
6. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo se despeja.

## Qué hace cada control

| Control       | Tipo           | Valor predeterminado |
|---------------|----------------|----------------------|
| **TUNE**      | Botón pulsador | —                    |
| **Tune Pwr**  | Control deslizante | 10               |
| **RF Pwr**    | Medidor        | —                    |
| **SWR**       | Medidor        | —                    |
| **RF Power**  | Control deslizante | 100              |
| **TX Profile**| Cuadro combinado | —                  |
| **MOX**       | Botón de alternancia | —                |
| **ATU**       | Botón pulsador | —                    |
| **MEM**       | Botón de alternancia | —                |
| **APD**       | Botón de alternancia | —                |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar una ROE razonable.
- El indicador **SWR** se vuelve rojo por encima de 2.5. Si se fija en 3.0, detenga la portadora y verifique las conexiones de su línea de bajada y antena antes de continuar.
- Para ejecutar el ATU interno en lugar de verificar la ROE manualmente, haga clic en **ATU** después de que la portadora de sintonía confirme que la antena es utilizable. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonía, configúrelas en `Settings > Inhibit during TUNE`.
- La barra de retención de pico en el indicador **RF Pwr** se restablece a cero inmediatamente cuando el transmisor desactiva la portadora, por lo que una lectura PEP retenida no persiste entre activaciones.

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón **ATU** se comporta como una alternancia sensible a la frecuencia en lugar de iniciar siempre un nuevo ciclo de sintonía. La lógica refleja el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o después de un cambio de frecuencia)** — Inicia un nuevo ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia** — Si el ATU ya ha reportado una adaptación exitosa (indicador **Success** o **Mem** encendido) y la frecuencia de transmisión no ha cambiado desde esa sintonía, al hacer clic en **ATU** se cambia el sintonizador a bypass en lugar de iniciar otro ciclo.
- **Después de cualquier cambio de frecuencia** — El registro de frecuencia sintonizada se borra. El siguiente clic en **ATU** siempre inicia un nuevo ciclo de sintonía, incluso si el resultado anterior fue exitoso.

Cuando el ATU entra en bypass, el registro de la frecuencia sintonizada también se borra, por lo que el siguiente clic iniciará una nueva sintonía independientemente de la frecuencia.

Este cambio no afecta al botón **MEM** ni a los indicadores de estado del ATU (**Success**, **Byp**, **Mem**), que continúan comportándose como se describe a continuación.

## Menú contextual del botón ATU

Haga clic con el botón derecho en el botón **ATU** para acceder a las siguientes acciones:

- **Pre-tune bands…** — Abre el cuadro de diálogo de Pre-sintonización de bandas para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando MEM está habilitado (el botón **MEM** debe estar activado). Si MEM está desactivado, el elemento del menú se deshabilita con una nota emergente que explica que MEM debe activarse primero.
- **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias del ATU almacenadas.

Esto coincide con el menú contextual oculto del botón ATU en SmartSDR Windows.

## MOX y tonos Quindar

A partir de la v0.9.7, al hacer clic en **MOX** se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice TX activo está en un modo de fonía, el tono K se reproduce al activar el PTT y el tono BK se reproduce al desactivar el PTT. Cuando Quindar está deshabilitado o el slice TX activo no está en un modo de fonía, el comportamiento es idéntico al de versiones anteriores.

Este cambio afecta solo al botón **MOX** en el applet de Controles de TX. El PTT por hardware, VOX y otras fuentes de PTT no se ven afectadas.

## Visualización del valor del control deslizante

A partir de la v26.5.3, al arrastrar el control deslizante **RF Pwr** o **Tune Pwr**, la viñeta del control deslizante muestra el valor actual en porcentaje (p. ej., "50%") como una nota emergente junto a la viñeta. Esto proporciona una retroalimentación visual inmediata del nivel de potencia mientras ajusta el control deslizante.

## Indicadores de estado APD

El grupo de botones **APD** muestra tres indicadores que rastrean el estado de la predistorsión adaptativa:

| Indicador | Color al iluminarse | Significado |
|-----------|---------------------|-------------|
| **Cal**   | Verde               | APD está activo y calibrando activamente. |
| **Avail** | Verde               | APD está activo y hay un resultado de calibración disponible pero aún no aplicado. |
| **Active**| Verde               | APD está activo y el ecualizador se está aplicando activamente. |

La progresión típica es: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado). Todos los indicadores están atenuados cuando APD está desactivado.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión activa al equipo. Verifique que AetherSDR muestre el equipo como conectado antes de intentar transmitir.
- **El indicador SWR no se mueve durante TUNE** — La potencia directa puede ser cero o estar cerca de cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en el estado **TUNING...**, verifique la conexión del equipo; una conexión perdida puede dejar el estado de transmisión sin confirmar.
- **El botón ATU pone el sintonizador en bypass en lugar de resintonizar** — Este es un comportamiento esperado cuando el ATU ya tiene una adaptación exitosa almacenada en la frecuencia actual. Cambie de frecuencia o espere a que el sintonizador borre su resultado, luego haga clic en **ATU** nuevamente para iniciar un nuevo ciclo de sintonía.
- **MOX activa el transmisor pero no se escuchan tonos Quindar** — Confirme que el chip QUIN esté habilitado en la tira de canales de audio y que el slice TX activo esté configurado en un modo de fonía (USB, LSB, AM, FM o similar). Los tonos Quindar no se reproducen en modos CW o digitales.
- **El elemento del menú Pre-tune bands aparece atenuado** — Active MEM haciendo clic en el botón **MEM** en el applet de Controles de TX antes de hacer clic con el botón derecho en **ATU**.
- **La barra de retención de pico no aparece durante la sintonía** — La barra de retención de pico solo rastrea cuando el transmisor está activado. La barra decae después de 2 segundos de mantener un pico y se restablece a cero al desactivar la portadora.

## Relacionados

- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- Pre-sintonización de bandas
- Borrar memorias del ATU
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)

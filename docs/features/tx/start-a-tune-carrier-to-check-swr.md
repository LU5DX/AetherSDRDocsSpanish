# Iniciar una portadora de sintonía para comprobar la ROE

Envíe una portadora continua a potencia reducida para leer la ROE de su sistema de antena. Úselo antes de un QSO o después de cambiar de antena para confirmar una buena adaptación.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet TX Controls solo está activo con una conexión en vivo al equipo.
- Asegúrese de tener autorización para transmitir en la frecuencia (la banda debe estar legalmente abierta para su estación).
- Ajuste la potencia de sintonía a un nivel adecuado para su sistema de antena. El valor predeterminado es 10; consulte [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón de la bandeja TX en la barra lateral derecha para abrir el applet TX Controls si aún no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic con el botón derecho en el botón **TUNE** para seleccionar la forma de la portadora para el siguiente ciclo de sintonía. Elija **Mono Tone** o **Two Tone** en el menú contextual. El modo de sintonía del equipo es transitorio de un solo disparo — AetherSDR no conserva la selección.
4. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora está activa.
   - El medidor **SWR** se actualiza en tiempo real. La escala va de 1.0 a 3.0; las lecturas superiores a 2.5 se muestran en rojo.
   - El medidor **RF Pwr** muestra la potencia directa en la salida del excitador. Una barra de retención de pico rastrea la potencia de envolvente de pico (PEP) durante 2 segundos y luego decae hacia la lectura actual.
5. Lea el valor de ROE en el medidor **SWR**. Pase el mouse sobre el medidor para ver la lectura exacta mostrada como "N.N:1".
6. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo se limpia.

## Qué hace cada control

| Control        | Tipo          | Valor predeterminado |
|----------------|---------------|---------|
| **TUNE**       | Botón pulsador | —       |
| **Tune Pwr**   | Control deslizante | 10      |
| **RF Pwr**     | Medidor        | —       |
| **SWR**        | Medidor        | —       |
| **RF Power**   | Control deslizante | 100     |
| **TX Profile** | Cuadro combinado | —       |
| **MOX**        | Botón de conmutación | —       |
| **ATU**        | Botón pulsador | —       |
| **MEM**        | Botón de conmutación | —       |
| **APD**        | Botón de conmutación | —       |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Súbalo solo después de confirmar una ROE razonable.
- El medidor **SWR** se vuelve rojo por encima de 2.5. Si llega al tope en 3.0, detenga la portadora y revise la línea de alimentación y las conexiones de la antena antes de continuar.
- Pase el mouse sobre el medidor **RF Pwr** para ver la potencia directa exacta en vatios. El medidor muestra valores de retención de pico, pero la lectura al pasar el mouse siempre muestra el valor actual preciso.
- Para ejecutar el ATU interno en lugar de comprobar la ROE manualmente, haga clic en **ATU** después de que la portadora de sintonía confirme que la antena es utilizable. Consulte [Ejecutar el ATU interno](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonía, configúrelas en `Settings > Inhibit during TUNE`.
- La barra de retención de pico en el medidor **RF Pwr** se restablece a cero inmediatamente cuando el transmisor desactiva la transmisión, por lo que una lectura PEP retenida no permanece entre transmisiones.

## Comportamiento del medidor

Los medidores **RF Pwr** y **SWR** muestran lecturas en vivo solo mientras el transmisor está activado. Cuando el transmisor está desactivado:

- El medidor **RF Pwr** vuelve a 0 W inmediatamente.
- El medidor **SWR** vuelve a su posición de reposo 1.0 inmediatamente.
- La barra de retención de pico en el medidor **RF Pwr** se limpia a cero.

A partir de la v26.8.4, nunca se deja pintada una última lectura obsoleta en los medidores después de desactivar la transmisión, incluso si una actualización del medidor en vuelo llega justo después de que el transmisor se apaga.

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón **ATU** se comporta como una conmutación sensible a la frecuencia en lugar de iniciar siempre un nuevo ciclo de sintonía. La lógica refleja el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o después de un cambio de frecuencia)** — Inicia un nuevo ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia** — Si el ATU ya ha informado una adaptación exitosa (indicador **Success** o **Mem** encendido) y la frecuencia de transmisión no ha cambiado desde esa sintonía, al hacer clic en **ATU** el sintonizador cambia a bypass en lugar de iniciar otro ciclo.
- **Después de cualquier cambio de frecuencia** — La frecuencia de sintonía guardada se borra. El siguiente clic en **ATU** siempre inicia un nuevo ciclo de sintonía, incluso si el resultado anterior fue exitoso.

Cuando el ATU entra en bypass, el registro de frecuencia sintonizada también se borra, por lo que el siguiente clic iniciará una sintonía nueva independientemente de la frecuencia.

Este cambio no tiene efecto en el botón **MEM** ni en los indicadores de estado del ATU (**Success**, **Byp**, **Mem**), que continúan comportándose como se describe a continuación.

## Menú contextual del botón ATU

Haga clic con el botón derecho en el botón **ATU** para acceder a las siguientes acciones:

- **Pre-tune bands…** — Abre el diálogo Pre-Tune Bands para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando MEM está habilitado (el botón **MEM** debe estar activado). Si MEM está apagado, el elemento del menú está deshabilitado con una información sobre herramientas que explica que MEM debe habilitarse primero.
- **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias ATU almacenadas.

Esto coincide con el menú contextual oculto de SmartSDR Windows en el botón ATU.

## Botones ATU y MEM en equipos sin sintonizador

A partir de la v26.8.4, AetherSDR verifica si el equipo conectado realmente tiene un sintonizador de antena. En equipos sin sintonizador (por ejemplo, un Hermes-Lite 2), los botones **ATU** y **MEM** están deshabilitados, y al pasar el mouse sobre cualquiera de los botones se muestra la información sobre herramientas **"This radio has no antenna tuner."**

Esto evita un peligro grave: en un equipo sin sintonizador, hacer clic en **ATU** activaría el transmisor para ejecutar un ciclo de sintonía que nada respondería. Los botones permanecen deshabilitados independientemente del estado de TGXL cuando no hay sintonizador presente.

Cuando TGXL está en modo OPERATE y hay un sintonizador presente, los botones están deshabilitados con la información sobre herramientas existente **"Disabled — TGXL is in OPERATE mode."** En ese caso, **TUNE** permanece habilitado para que aún pueda ejecutar una portadora a través del TGXL para verificaciones de potencia/ROE.

## MOX y tonos Quindar

A partir de la v0.9.7, al hacer clic en **MOX** se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando el chip QUIN está habilitado en la tira de canales de audio y el slice TX activo está en modo de fonía, el tono K se reproduce al activar PTT y el tono BK se reproduce al desactivar PTT. Cuando Quindar está deshabilitado o el slice TX activo no está en modo de fonía, el comportamiento es idéntico a versiones anteriores.

Este cambio afecta solo al botón **MOX** en el applet TX Controls. El PTT por hardware, VOX y otras fuentes de PTT no se ven afectadas.

## Apariencia del botón MOX

A partir de la v26.7.4, el botón MOX en su estado de reposo (recepción) muestra un acento ámbar — un borde ámbar y color de texto que lo distingue del estilo neutro de los botones adyacentes TUNE, ATU y MEM. Esta señal visual deja claro que MOX es el botón de transmisión. Cuando el transmisor está activado, el botón se vuelve rojo sólido con texto blanco como antes.

Los colores de acento ámbar están tokenizados en el Editor de temas bajo las claves `color.tx.mox.*`, por lo que puede personalizar la apariencia de reposo si lo desea. Los cambios realizados en el Editor de temas se aplican inmediatamente al botón MOX.

## Visualización del valor del control deslizante

A partir de la v26.5.3, al arrastrar el control deslizante **RF Pwr** o **Tune Pwr**, el pulgar del control deslizante muestra el valor actual en porcentaje (por ejemplo, "50%") como información sobre herramientas junto al pulgar. Esto proporciona retroalimentación visual inmediata del nivel de potencia mientras ajusta el control deslizante.

A partir de la v26.7.4, al soltar el control deslizante después de arrastrarlo, el valor mostrado se sincroniza con el modelo del equipo, asegurando que la posición del control deslizante y el nivel de potencia real permanezcan en concordancia.

## Indicadores de estado APD

El grupo de botones **APD** muestra tres indicadores que rastrean el estado de predistorsión adaptativa:

| Indicador | Color cuando está encendido | Significado |
|-----------|----------------|---------|
| **Cal**   | Verde          | APD está activado y calibrando activamente. |
| **Avail** | Verde          | APD está activado y hay un resultado de calibración disponible pero aún no aplicado. |
| **Active** | Verde         | APD está activado y el ecualizador se está aplicando activamente. |

La progresión típica es: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado). Todos los indicadores están atenuados cuando APD está apagado.

## Visibilidad del botón APD

A partir de la v26.8.4, el botón **APD** y sus indicadores **Active**/**Cal**/**Avail** están ocultos cuando el equipo conectado no admite predistorsión adaptativa. En el arranque en frío, la fila APD se oculta correctamente hasta que el equipo confirma el soporte de APD, coincidiendo con el comportamiento después de una desconexión. Esto evita un botón APD de apariencia activa sin respaldo funcional.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión activa al equipo. Verifique que AetherSDR muestre el equipo como conectado antes de intentar transmitir.
- **El medidor SWR no se mueve durante TUNE** — La potencia directa puede estar en cero o cerca de cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en estado **TUNING...**, verifique la conexión del equipo; una conexión caída puede dejar el estado de transmisión sin confirmar.
- **El botón ATU pasa por alto el sintonizador en lugar de volver a sintonizar** — Este es el comportamiento esperado cuando el ATU ya tiene una adaptación exitosa en la frecuencia actual. Cambie de frecuencia o espere a que el sintonizador borre su resultado, luego haga clic en **ATU** nuevamente para iniciar un nuevo ciclo de sintonía.
- **Los botones ATU y MEM están deshabilitados** — El equipo conectado no tiene sintonizador de antena, o el TGXL está en modo OPERATE. Pase el mouse sobre cualquiera de los botones para ver la razón específica en la información sobre herramientas.
- **MOX activa el transmisor pero no se escuchan tonos Quindar** — Confirme que el chip QUIN está habilitado en la tira de canales de audio y que el slice TX activo está configurado en modo de fonía (USB, LSB, AM, FM o similar). Los tonos Quindar no se reproducen en modos CW o digitales.
- **El elemento de menú Pre-tune bands está atenuado** — Habilite MEM haciendo clic en el botón **MEM** en el applet TX Controls antes de hacer clic con el botón derecho en **ATU**.
- **La barra de retención de pico no aparece durante la sintonía** — La barra de retención de pico solo rastrea cuando el transmisor está activado. La barra decae después de 2 segundos de mantener un pico y se restablece a cero al desactivar la transmisión.
- **La lectura al pasar el mouse sobre RF Pwr o SWR no aparece** — Asegúrese de que el cursor del mouse esté posicionado directamente sobre la barra del medidor. La lectura aparece como una información sobre herramientas emergente que muestra el valor exacto en el formato apropiado (vatios o "N.N:1").

## Relacionados

- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- Pre-tune bands
- Clear ATU memories
- [Recuperar una memoria ATU](recall-an-atu-memory.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)

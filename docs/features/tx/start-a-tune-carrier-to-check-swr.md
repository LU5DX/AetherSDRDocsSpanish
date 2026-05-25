# Iniciar una portadora de sintonía para verificar la ROE

Envíe una portadora continua a potencia reducida para leer la ROE de su sistema de antena. Úselo antes de un QSO o después de cambiar de antena para confirmar una buena adaptación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet de Controles de TX solo está activo con una conexión de radio activa.
- Asegúrese de tener permiso para transmitir en la frecuencia (la banda debe estar legalmente abierta para su estación).
- Ajuste la potencia de sintonía a un nivel adecuado para su sistema de antena. El valor predeterminado es 10; consulte [Ajustar la potencia de la portadora de sintonía](set-tune-carrier-power.md).

## Pasos

1. Haga clic en el botón de la bandeja TX en la barra lateral derecha para abrir el applet de Controles de TX si aún no está visible.
2. Verifique el control deslizante **Tune Pwr**. El valor predeterminado es 10 (de 100). Ajústelo si es necesario antes de transmitir.
3. Haga clic con el botón derecho en el botón **TUNE** para seleccionar la forma de la portadora para el siguiente ciclo de sintonía. Elija **Mono Tone** o **Two Tone** en el menú contextual. El modo de sintonía de la radio es transitorio y de un solo disparo; AetherSDR no conserva la selección.
4. Haga clic en **TUNE**.
   - La etiqueta del botón cambia a **TUNING...** y el fondo del botón se vuelve rojo mientras la portadora está activa.
   - El indicador **SWR** se actualiza en tiempo real. La escala va de 1.0 a 3.0; las lecturas superiores a 2.5 se muestran en rojo.
   - El indicador **RF Pwr** muestra la potencia directa en la salida del excitador. Una barra de retención de pico rastrea la potencia envolvente de pico (PEP) durante 2 segundos y luego disminuye hacia la lectura actual.
5. Lea el valor de ROE en el indicador **SWR**.
6. Haga clic en **TUNE** nuevamente para detener la portadora.
   - La etiqueta del botón vuelve a **TUNE** y el fondo rojo desaparece.

## Función de cada control

| Control      | Tipo          | Valor predeterminado |
|--------------|---------------|----------------------|
| **TUNE**     | Botón pulsador | —                    |
| **Tune Pwr** | Control deslizante | 10               |
| **RF Pwr**   | Medidor       | —                    |
| **SWR**      | Medidor       | —                    |

## Consejos

- Mantenga **Tune Pwr** bajo (10 o menos) al probar un sistema de antena desconocido. Auméntelo solo después de confirmar una ROE razonable.
- El indicador **SWR** se vuelve rojo por encima de 2.5. Si llega a 3.0, detenga la portadora y verifique las conexiones de su línea de transmisión y antena antes de continuar.
- Para ejecutar la ATU interna en lugar de verificar la ROE manualmente, haga clic en **ATU** después de que la portadora de sintonía confirme que la antena es utilizable. Consulte [Ejecutar la ATU interna](run-the-internal-atu.md).
- Si desea inhibir salidas TX específicas (ACC TX, TX1, TX2, TX3) durante la sintonía, configúrelas en `Settings > Inhibit during TUNE`.
- La barra de retención de pico en el indicador **RF Pwr** se restablece a cero inmediatamente cuando el transmisor desactiva la transmisión, por lo que una lectura de PEP retenida no persiste entre transmisiones.

## Comportamiento del botón ATU (v0.9.5.1)

A partir de v0.9.5.1, el botón **ATU** se comporta como un conmutador que reconoce la frecuencia en lugar de iniciar siempre un nuevo ciclo de sintonía. La lógica refleja el comportamiento por frecuencia de SmartSDR:

- **Primer clic (o después de un cambio de frecuencia)** — Inicia un nuevo ciclo de sintonía ATU.
- **Segundo clic en la misma frecuencia** — Si la ATU ya ha informado una adaptación exitosa (indicador **Success** o **Mem** encendido) y la frecuencia de transmisión no ha cambiado desde esa sintonía, hacer clic en **ATU** cambia el sintonizador a bypass en lugar de iniciar otro ciclo.
- **Después de cualquier cambio de frecuencia** — El registro de frecuencia sintonizada se borra. El siguiente clic en **ATU** siempre inicia un nuevo ciclo de sintonía, incluso si el resultado anterior fue exitoso.

Cuando la ATU entra en bypass, el registro de frecuencia sintonizada también se borra, por lo que el siguiente clic iniciará una nueva sintonía independientemente de la frecuencia.

Este cambio no afecta al botón **MEM** ni a los indicadores de estado de la ATU (**Success**, **Byp**, **Mem**), que continúan comportándose como se describe a continuación.

## Menú contextual del botón ATU (v26.5.2.1)

Haga clic con el botón derecho en el botón **ATU** para acceder a las siguientes acciones:

- **Pre-tune bands…** — Abre el diálogo de Pre-sintonía de bandas para ejecutar un barrido en las bandas seleccionadas. Esta acción solo está disponible cuando MEM está habilitado (el botón **MEM** debe estar activado). Si MEM está desactivado, el elemento del menú aparece deshabilitado con una descripción emergente que explica que MEM debe habilitarse primero.
- **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias ATU almacenadas.

Esto coincide con el menú contextual oculto del botón ATU en SmartSDR Windows.

## Tonos MOX y Quindar (v0.9.7)

A partir de v0.9.7, hacer clic en **MOX** se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Cuando el chip QUIN está habilitado en la tira del canal de audio y la franja TX activa está en un modo de telefonía, el tono K se reproduce al activar PTT y el tono BK se reproduce al desactivar PTT. Cuando Quindar está deshabilitado o la franja TX activa no está en un modo de telefonía, el comportamiento es idéntico al de versiones anteriores.

Este cambio afecta solo al botón **MOX** en el applet de Controles de TX. El PTT por hardware, VOX y otras fuentes de PTT no se ven afectadas.

## Visualización del valor del control deslizante (v26.5.3)

A partir de v26.5.3, al arrastrar el control deslizante **RF Pwr** o **Tune Pwr**, el pulgar del control deslizante muestra el valor actual en vatios (p. ej., "50 W") como una descripción emergente junto al pulgar. Esto proporciona información visual inmediata del nivel de potencia mientras ajusta el control deslizante.

## Solución de problemas

- **El botón TUNE no hace nada** — El applet requiere una conexión de radio activa. Verifique que AetherSDR muestre la radio como conectada antes de intentar transmitir.
- **El indicador SWR no se mueve durante TUNE** — La potencia directa puede ser cercana a cero o cero. Verifique que el control deslizante **Tune Pwr** esté por encima de 0 y que el puerto de antena correcto esté seleccionado para la banda actual.
- **La portadora no se detiene** — Haga clic en **TUNE** una vez más. Si el botón permanece en estado **TUNING...**, verifique la conexión de la radio; una conexión perdida puede dejar el estado de transmisión sin confirmar.
- **El botón ATU pasa por alto el sintonizador en lugar de resintonizar** — Este es un comportamiento esperado cuando la ATU ya tiene una adaptación exitosa en la frecuencia actual. Cambie de frecuencia o espere a que el sintonizador borre su resultado, luego haga clic en **ATU** nuevamente para iniciar un nuevo ciclo de sintonía.
- **MOX activa el transmisor pero no se escuchan tonos Quindar** — Confirme que el chip QUIN esté habilitado en la tira del canal de audio y que la franja TX activa esté configurada en un modo de telefonía (USB, LSB, AM, FM o similar). Los tonos Quindar no se reproducen en modos CW o digitales.
- **El elemento del menú Pre-tune bands aparece atenuado** — Habilite MEM haciendo clic en el botón **MEM** en el applet de Controles de TX antes de hacer clic con el botón derecho en **ATU**.
- **La barra de retención de pico no aparece durante la sintonía** — La barra de retención de pico solo realiza el seguimiento cuando el transmisor está activado. La barra disminuye después de 2 segundos de mantener un pico y se restablece a cero al desactivar la transmisión.

## Relacionados

- [Ajustar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Ejecutar la ATU interna](run-the-internal-atu.md)
- Pre-sintonía de bandas
- Borrar memorias ATU
- [Recordar una memoria ATU](recall-an-atu-memory.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)

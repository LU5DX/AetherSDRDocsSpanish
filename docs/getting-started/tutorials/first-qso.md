# Realice su primer QSO con AetherSDR

Esta página le guía a través de la conexión a su FLEX-8600, la sintonización de una frecuencia, la verificación de la antena y la configuración de potencia, y la realización de un contacto. Siga estos pasos en orden la primera vez que use AetherSDR.

## Antes de comenzar

- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora, o tiene credenciales de SmartLink y una radio remota disponible.
- AetherSDR está instalado e iniciado.
- Sabe qué banda y modo desea operar (por ejemplo, 14.225 MHz USB).
- Su micrófono o keyer está conectado y configurado en la radio.

## Pasos

### 1. Conéctese a la radio

1. Cuando no haya ninguna radio conectada, AetherSDR muestra el panel **Connect to a Radio** en la ventana principal. Si ya lo ha cerrado, ábralo mediante `Settings > Connect to Radio...`.
2. El modo predeterminado es **Local**. Si su radio está en la misma LAN, mantenga esta opción seleccionada.
3. Espere unos segundos a que la lista **Available radios** se complete mediante el descubrimiento automático. Su FLEX-8600 debería aparecer por su nombre.
4. Haga clic en su radio en la lista **Available radios** para resaltarla.
5. Haga clic en **Connect Selected Radio**.
6. La etiqueta de estado cambia de "searching" a "connecting" y luego a "connected". La vista principal del panadapter se abre cuando la conexión se realiza correctamente.

Si la lista permanece vacía, haga clic en **Retry Discovery**. Si la radio está en una subred diferente, haga clic en **Connect by IP** e introduzca la dirección IP de la radio en el campo **Radio IP address**, luego haga clic en **Connect by IP (manual)**. El campo **Radio IP address** es un menú desplegable que también muestra hasta tres direcciones utilizadas anteriormente; seleccione una entrada reciente o escriba una nueva. Para una radio remota a través de internet, haga clic en **Remote with SmartLink** e inicie sesión.

Por defecto, la opción **Connect to last radio on start up** está marcada, por lo que AetherSDR se reconectará automáticamente a la radio utilizada más recientemente cada vez que se inicie. Si prefiere elegir una radio manualmente en cada inicio, desmarque esta opción en el panel **Connect to a Radio**. El ajuste se guarda inmediatamente cuando lo cambia (`AutoConnectToLastRadio`).

Al conectarse por IP manualmente, seleccione la interfaz de red local del cuadro combinado **Advanced: Source path**. La etiqueta **Source warning label** aparece debajo de este cuadro combinado cuando la NIC guardada anteriormente ya no es accesible. Seleccione una interfaz de origen válida antes de hacer clic en **Connect by IP (manual)**.

### 2. Seleccione la antena correcta

1. En la barra lateral derecha, haga clic en el botón de la bandeja **RX** para abrir el applet de controles de RX (es visible por defecto).
2. Localice el cuadro combinado de antena etiquetado en azul (antena RX, por defecto **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena receptora.
3. Localice el cuadro combinado de antena etiquetado en rojo (antena TX, por defecto **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena transmisora. Los puertos solo de RX no se muestran aquí.

### 3. Configure el modo de operación y la frecuencia

1. En el applet de controles de RX, haga clic en el **Mode combo** y seleccione su modo, por ejemplo, **USB** para banda lateral única superior en fonía.
2. Haga clic en la etiqueta **Frequency** para cambiarla a modo de edición (aparece el campo **Frequency edit**).
3. Escriba su frecuencia objetivo en MHz (por ejemplo, `14.225`) y presione **Enter**. El panadapter se recentra en la nueva frecuencia. Presione **Escape** para cancelar sin cambiar la frecuencia.
4. Elija un ancho de filtro haciendo clic en uno de los botones **Filter width presets**. Para USB, los preajustes disponibles son 1800, 2100, 2400, 2700, 2900 y 3300 Hz. 2700 Hz es un punto de partida común para SSB.

### 4. Establezca la potencia de transmisión

1. Haga clic en el botón de la bandeja **TX** en la barra lateral derecha para abrir el applet de controles de TX.
2. Arrastre el control deslizante **RF Power** a su nivel de potencia deseado (por defecto **100**, rango 0–100). Observe el medidor **RF Pwr** durante una transmisión para confirmar la salida real.
3. Verifique el medidor **SWR**. Una lectura superior a 2.5 se muestra en rojo; investigue su sistema de antena antes de transmitir si es así.
4. Si desea ejecutar primero la ATU interna, haga clic en **ATU** y espere a que el ciclo termine. El indicador **Success** se ilumina en verde cuando se encuentra una coincidencia.

### 5. Verifique el audio y la ganancia

1. De vuelta en el applet de controles de RX, confirme que el control deslizante **AF gain** está en un nivel de escucha cómodo (por defecto **70**, rango 0–100).
2. Confirme que el cuadro combinado **AGC mode** está configurado en **Med** (el valor predeterminado) para SSB. Ajústelo a **Slow** o **Fast** si es necesario.
3. Si no escucha audio, verifique que la alternancia de silencio (🔊/🔇) muestre el estado sin silencio.

### 6. Realice el contacto

1. Escuche en la frecuencia. Cuando esté listo para llamar, active su micrófono o keyer.
2. Para transmitir usando la activación por software, haga clic en **MOX** en el applet de controles de TX. El botón se vuelve rojo mientras transmite. Haga clic en **MOX** nuevamente para volver a recibir.
3. Observe el medidor **RF Pwr** para confirmar la salida, y el medidor **SWR** para confirmar que la antena está adaptada.
4. Cuando el QSO esté completo, haga clic en **MOX** para asegurarse de estar de vuelta en recepción, o simplemente suelte su PTT de hardware.

## Consejos

- Si la otra estación está ligeramente fuera de frecuencia y no desea mover su VFO, habilite **RIT** en el applet de controles de RX y use el cuadro de ajuste **RIT offset** (pasos de 10 Hz) para desplazar su frecuencia de recepción sin cambiar la transmisión. Haga clic en **RIT 0** para ponerlo a cero después.
- Para evitar resintonizar accidentalmente durante un QSO, haga clic en la alternancia 🔓 en el applet de controles de RX para bloquear el slice. El icono cambia a 🔒.
- El control deslizante **L / R pan** (por defecto **50**, rango 0–100) le permite posicionar el audio de este slice en el campo estéreo. Haga doble clic en él para restablecerlo al centro.
- Si opera en split, use **XIT** en el applet de controles de RX para desplazar su frecuencia de transmisión independientemente del VFO de recepción.
- Use los atajos de teclado **widen** y **narrow** para recorrer los preajustes de filtro por modo. El método `stepFilterWidth(direction)` recorre la lista de preajustes por modo, por lo que la geometría del borde del filtro es siempre correcta para el modo activo (USB, LSB, CW, AM, DIGL, etc.). Por ejemplo, presionar un atajo de widen en modo CW recorre los preajustes de 50, 100, 250, 400 Hz, mientras que en USB recorre los preajustes de 1800, 2100, 2400, 2700, 2900, 3300 Hz.

## Solución de problemas

- **La lista Available radios está vacía** — Haga clic en **Retry Discovery**. Verifique que la radio esté encendida y en el mismo segmento de red. Haga clic en **Open Network Diagnostics** para inspeccionar la ruta. Si la radio está en una subred diferente, use **Connect by IP (manual)** en su lugar.
- **No hay audio del altavoz** — Verifique que la alternancia de silencio en el applet de controles de RX muestre el estado sin silencio (🔊). Verifique que **AF gain** esté por encima de 0. Verifique la configuración del dispositivo de audio en su sistema operativo.
- **MOX se activa pero el medidor RF Pwr lee cero** — Confirme que la antena TX correcta esté seleccionada en el cuadro combinado de antena TX etiquetado en rojo. Confirme que **RF Power** esté por encima de 0 en el applet de controles de TX.
- **El medidor SWR lee en rojo (por encima de 2.5)** — No continúe transmitiendo a máxima potencia. Verifique las conexiones de la antena. Ejecute la **ATU** interna para encontrar una coincidencia, o reduzca la potencia hasta que se resuelva el problema.
- **La edición de frecuencia no acepta el valor** — Asegúrese de estar introduciendo un valor en MHz dentro del rango válido (0.001–54.000 MHz). Presione **Escape** para cancelar y restaurar la frecuencia anterior.
- **El menú desplegable Radio IP address muestra una dirección obsoleta** — La etiqueta **Source warning label** aparece debajo del cuadro combinado **Advanced: Source path** cuando la NIC guardada anteriormente ya no es accesible. Seleccione una interfaz de origen válida antes de hacer clic en **Connect by IP (manual)**.
- **La ventana de conexión no es visible o no restauró su tamaño anterior** — Al entrar o salir del modo sin marco, la ventana restaura su geometría solo si era visible anteriormente. Si la ventana de conexión aparece en una posición inesperada, redimensiónela o reubíquela normalmente y recordará esas dimensiones la próxima vez.

## Relacionado

- [Connect to a local LAN radio](../setup/connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](../setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Retry discovery when no radios appear](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Change mode (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Tune the radio to a frequency (type MHz in the readout)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Pick a filter width preset for the current mode](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Select the RX or TX antenna for this slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Set RF output power](../../features/tx/set-rf-output-power.md)
- [Start a tune carrier to check SWR](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Run the internal ATU](../../features/tx/run-the-internal-atu.md)
- [Toggle MOX to manually key the transmitter](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Use RIT to offset the receive frequency for a drifting station](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Use XIT to offset the transmit frequency without changing RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Lock the slice to prevent accidental retuning](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Understanding slices and VFOs](../concepts/understanding-slices.md)

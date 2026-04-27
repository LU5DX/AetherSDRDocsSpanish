# Haga su primer QSO con AetherSDR

Esta página le guía a través de la conexión con su FLEX-8600, la sintonización de una frecuencia, la verificación de la antena y la configuración de potencia, y la realización de un contacto. Siga estos pasos en orden la primera vez que use AetherSDR.

## Antes de comenzar

- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora, o bien dispone de credenciales SmartLink y un radio remoto disponible.
- AetherSDR está instalado y en ejecución.
- Sabe qué banda y modo desea operar (por ejemplo, 14.225 MHz USB).
- Su micrófono o manipulador está conectado y configurado en el radio.

## Pasos

### 1. Conectarse al radio

1. Cuando no hay ningún radio conectado, AetherSDR muestra el panel **Connect to a Radio** en la ventana principal. Si ya lo cerró, ábralo desde `Settings > Connect to Radio...`.
2. El modo predeterminado es **Local**. Si su radio está en la misma LAN, déjelo seleccionado.
3. Espere unos segundos a que la lista **Available radios** se complete mediante la detección automática. Su FLEX-8600 debería aparecer por nombre.
4. Haga clic en su radio en la lista **Available radios** para resaltarlo.
5. Haga clic en **Connect Selected Radio**.
6. La etiqueta de estado cambia de "searching" a "connecting" y luego a "connected". La vista del panadapter principal se abre cuando la conexión se establece correctamente.

Si la lista permanece vacía, haga clic en **Retry Discovery**. Si el radio está en una subred diferente, haga clic en **Connect by IP** e introduzca la dirección IP del radio en el campo **Radio IP address**, luego haga clic en **Connect by IP (manual)**. Para un radio remoto a través de internet, haga clic en **Remote with SmartLink** e inicie sesión.

### 2. Seleccionar la antena correcta

1. En la barra lateral derecha, haga clic en el botón **RX** para abrir el applet RX Controls (visible de forma predeterminada).
2. Localice el cuadro combinado de antena con etiqueta azul (antena RX, predeterminada **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena de recepción.
3. Localice el cuadro combinado de antena con etiqueta roja (antena TX, predeterminada **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena de transmisión. Los puertos exclusivos de recepción no aparecen en esta lista.

### 3. Configurar el modo de operación y la frecuencia

1. En el applet RX Controls, haga clic en el **Mode combo** y seleccione su modo — por ejemplo, **USB** para telefonía en banda lateral superior.
2. Haga clic en la **Frequency label** para cambiarla al modo de edición (aparece el campo **Frequency edit**).
3. Escriba la frecuencia deseada en MHz (por ejemplo, `14.225`) y presione **Enter**. El panadapter se recentra en la nueva frecuencia. Presione **Escape** para cancelar sin cambiar la frecuencia.
4. Elija un ancho de filtro haciendo clic en uno de los botones **Filter width presets**. Para USB, los valores disponibles son 1800, 2100, 2400, 2700, 2900 y 3300 Hz. 2700 Hz es un punto de partida habitual para SSB.

### 4. Configurar la potencia de transmisión

1. Haga clic en el botón **TX** en la barra lateral derecha para abrir el applet TX Controls.
2. Arrastre el control deslizante **RF Power** hasta el nivel de potencia deseado (predeterminado **100**, rango 0–100). Observe el medidor **RF Pwr** durante una transmisión para confirmar la salida real.
3. Compruebe el medidor **SWR**. Una lectura superior a 2.5 se muestra en rojo; investigue su sistema de antena antes de transmitir si es el caso.
4. Si desea ejecutar primero el ATU interno, haga clic en **ATU** y espere a que el ciclo finalice. El indicador **Success** se ilumina en verde cuando se encuentra una coincidencia.

### 5. Verificar el audio y la ganancia

1. De vuelta en el applet RX Controls, confirme que el control deslizante **AF gain** está en un nivel de escucha cómodo (predeterminado **70**, rango 0–100).
2. Confirme que el cuadro combinado **AGC mode** está configurado en **Med** (el valor predeterminado) para SSB. Ajuste a **Slow** o **Fast** si es necesario.
3. Si no escucha audio, compruebe que el botón de silencio (🔊/🔇) muestra el estado sin silencio.

### 6. Realizar el contacto

1. Escuche en la frecuencia. Cuando esté listo para llamar, active su micrófono o manipulador.
2. Para transmitir mediante control por software, haga clic en **MOX** en el applet TX Controls. El botón se vuelve rojo mientras transmite. Haga clic en **MOX** de nuevo para volver a recepción.
3. Observe el medidor **RF Pwr** para confirmar la salida, y el medidor **SWR** para confirmar que la antena está adaptada.
4. Cuando el QSO haya concluido, haga clic en **MOX** para asegurarse de estar en recepción, o simplemente suelte el PTT por hardware.

## Consejos

- Si la otra estación está ligeramente fuera de frecuencia y no desea mover su VFO, active **RIT** en el applet RX Controls y use el control giratorio **RIT offset** (pasos de 10 Hz) para desplazar su frecuencia de recepción sin cambiar la de transmisión. Haga clic en **RIT 0** para anularlo al finalizar.
- Para evitar una resintonización accidental durante el QSO, haga clic en el botón 🔓 en el applet RX Controls para bloquear el slice (canal de recepción virtual). El ícono cambia a 🔒.
- El control deslizante **L / R pan** (predeterminado **50**, rango 0–100) le permite posicionar el audio de este slice en el campo estéreo. Haga doble clic para restablecerlo al centro.
- Si opera en split, use **XIT** en el applet RX Controls para desplazar su frecuencia de transmisión de forma independiente al VFO de recepción.

## Solución de problemas

- **La lista Available radios está vacía** — Haga clic en **Retry Discovery**. Verifique que el radio esté encendido y en el mismo segmento de red. Haga clic en **Open Network Diagnostics** para inspeccionar la ruta. Si el radio está en una subred diferente, use **Connect by IP (manual)**.
- **Sin audio por el altavoz** — Compruebe que el botón de silencio en el applet RX Controls muestra el estado sin silencio (🔊). Verifique que **AF gain** esté por encima de 0. Confirme la configuración del dispositivo de audio en su sistema operativo.
- **MOX activa la transmisión pero el medidor RF Pwr indica cero** — Confirme que la antena TX correcta está seleccionada en el cuadro combinado de antena TX con etiqueta roja. Confirme que **RF Power** está por encima de 0 en el applet TX Controls.
- **El medidor SWR marca en rojo (por encima de 2.5)** — No continúe transmitiendo a plena potencia. Revise las conexiones de antena. Ejecute el **ATU** interno para encontrar una adaptación, o reduzca la potencia hasta resolver el problema.
- **El campo Frequency edit no acepta el valor** — Asegúrese de introducir un valor en MHz dentro del rango válido (0.001–54.000 MHz). Presione **Escape** para cancelar y restaurar la frecuencia anterior.

## Relacionados

- [Conectar a un radio en LAN local](../setup/connect-to-a-local-lan-radio.md)
- [Conectar a un radio remoto mediante SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectar por IP a través de una VPN o red enrutada](../setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar la detección cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Configurar la potencia de salida RF](../../features/tx/set-rf-output-power.md)
- [Iniciar una portadora de prueba para verificar el SWR](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](../../features/tx/run-the-internal-atu.md)
- [Activar MOX para manipular manualmente el transmisor](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Usar RIT para desplazar la frecuencia de recepción ante una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Bloquear el slice para evitar una resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Comprender los slices y los VFOs](../concepts/understanding-slices.md)

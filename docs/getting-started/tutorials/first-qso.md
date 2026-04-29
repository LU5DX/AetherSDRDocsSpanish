# Haga su primer QSO con AetherSDR

Esta página explica cómo conectarse al FLEX-8600, sintonizar una frecuencia, verificar la antena y la potencia de salida, y establecer un contacto. Siga estos pasos en orden la primera vez que use AetherSDR.

## Antes de comenzar

- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora, o dispone de credenciales SmartLink y un radio remoto disponible.
- AetherSDR está instalado y en ejecución.
- Sabe qué banda y modo desea operar (por ejemplo, 14.225 MHz USB).
- Su micrófono o manipulador (keyer) está conectado y configurado en el radio.

## Pasos

### 1. Conectarse al radio

1. Cuando no hay ningún radio conectado, AetherSDR muestra el panel **Connect to a Radio** en la ventana principal. Si ya lo cerró, ábralo desde `Settings > Connect to Radio...`.
2. El modo predeterminado es **Local**. Si su radio está en la misma LAN, deje esta opción seleccionada.
3. Espere unos segundos para que la lista **Available radios** se complete mediante descubrimiento automático. Su FLEX-8600 debe aparecer por nombre.
4. Haga clic en su radio en la lista **Available radios** para resaltarlo.
5. Haga clic en **Connect Selected Radio**.
6. La etiqueta de estado cambia de "searching" a "connecting" y luego a "connected". La vista del panadapter principal se abre cuando la conexión se establece correctamente.

Si la lista permanece vacía, haga clic en **Retry Discovery**. Si el radio está en una subred diferente, haga clic en **Connect by IP** e ingrese la dirección IP del radio en el campo **Radio IP address**, luego haga clic en **Connect by IP (manual)**. Para un radio remoto a través de internet, haga clic en **Remote with SmartLink** e inicie sesión.

### 2. Seleccionar la antena correcta

1. En la barra lateral derecha, haga clic en el botón de bandeja **RX** para abrir el applet RX Controls (visible de forma predeterminada).
2. Busque el cuadro combinado de antena con etiqueta azul (antena RX, predeterminada **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena de recepción.
3. Busque el cuadro combinado de antena con etiqueta roja (antena TX, predeterminada **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena de transmisión. Los puertos exclusivos de RX no aparecen aquí.

### 3. Establecer el modo de operación y la frecuencia

1. En el applet RX Controls, haga clic en **Mode combo** y seleccione su modo; por ejemplo, **USB** para fonía en banda lateral superior.
2. Haga clic en **Frequency label** para activar el modo de edición (aparece el campo **Frequency edit**).
3. Escriba su frecuencia objetivo en MHz (por ejemplo, `14.225`) y presione **Enter**. El panadapter se recentra en la nueva frecuencia. Presione **Escape** para cancelar sin cambiar la frecuencia.
4. Elija el ancho de filtro haciendo clic en uno de los botones **Filter width presets**. Para USB, los ajustes preestablecidos disponibles son 1800, 2100, 2400, 2700, 2900 y 3300 Hz. 2700 Hz es un punto de partida habitual para SSB.

### 4. Configurar la potencia de transmisión

1. Haga clic en el botón de bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls.
2. Arrastre el control deslizante **RF Power** hasta el nivel de potencia deseado (predeterminado **100**, rango 0–100). Observe el medidor **RF Pwr** durante una transmisión para confirmar la salida real.
3. Verifique el medidor **SWR**. Una lectura superior a 2.5 se muestra en rojo; en ese caso, revise el sistema de antena antes de transmitir.
4. Si desea usar primero el ATU interno, haga clic en **ATU** y espere a que el ciclo finalice. El indicador **Success** se ilumina en verde cuando se encuentra una concordancia.

### 5. Verificar el audio y la ganancia

1. De vuelta en el applet RX Controls, confirme que el control deslizante **AF gain** está en un nivel de escucha cómodo (predeterminado **70**, rango 0–100).
2. Confirme que el cuadro combinado **AGC mode** está configurado en **Med** (el valor predeterminado) para SSB. Ajuste a **Slow** o **Fast** si es necesario.
3. Si no escucha audio, verifique que el botón de silencio (🔊/🔇) muestre el estado sin silencio.

### 6. Establecer el contacto

1. Escuche en la frecuencia. Cuando esté listo para llamar, accione su micrófono o manipulador.
2. Para transmitir mediante activación por software, haga clic en **MOX** en el applet TX Controls. El botón se vuelve rojo mientras transmite. Haga clic en **MOX** nuevamente para volver a la recepción.
3. Observe el medidor **RF Pwr** para confirmar la salida, y el medidor **SWR** para confirmar que la antena está acoplada.
4. Cuando el QSO finalice, haga clic en **MOX** para asegurarse de estar en modo de recepción, o simplemente suelte el PTT de hardware.

## Consejos

- Si la otra estación está ligeramente fuera de frecuencia y no desea mover su VFO, active **RIT** en el applet RX Controls y use el spinbox **RIT offset** (pasos de 10 Hz) para desplazar su frecuencia de recepción sin cambiar la transmisión. Haga clic en **RIT 0** para anularlo luego.
- Para evitar sintonizar accidentalmente en medio de un QSO, haga clic en el botón 🔓 en el applet RX Controls para bloquear el slice (receptor virtual). El icono cambia a 🔒.
- El control deslizante **L / R pan** (predeterminado **50**, rango 0–100) permite posicionar el audio de este slice en el campo estéreo. Haga doble clic para restablecer el centro.
- Si opera en split, use **XIT** en el applet RX Controls para desplazar su frecuencia de transmisión de forma independiente al VFO de recepción.

## Solución de problemas

- **La lista Available radios está vacía** — Haga clic en **Retry Discovery**. Verifique que el radio esté encendido y en el mismo segmento de red. Haga clic en **Open Network Diagnostics** para inspeccionar la ruta. Si el radio está en una subred diferente, utilice **Connect by IP (manual)** en su lugar.
- **Sin audio por el altavoz** — Verifique que el botón de silencio en el applet RX Controls muestre el estado sin silencio (🔊). Compruebe que **AF gain** esté por encima de 0. Verifique la configuración del dispositivo de audio en su sistema operativo.
- **MOX activa la transmisión, pero el medidor RF Pwr muestra cero** — Confirme que la antena TX correcta está seleccionada en el cuadro combinado de antena TX con etiqueta roja. Confirme que **RF Power** está por encima de 0 en el applet TX Controls.
- **El medidor SWR muestra rojo (por encima de 2.5)** — No continúe transmitiendo a plena potencia. Verifique las conexiones de antena. Ejecute el **ATU** interno para encontrar una concordancia, o reduzca la potencia hasta resolver el problema.
- **El campo Frequency edit no acepta el valor** — Asegúrese de ingresar un valor en MHz dentro del rango válido (0.001–54.000 MHz). Presione **Escape** para cancelar y restaurar la frecuencia anterior.

## Relacionados

- [Conectarse a un radio en LAN local](../setup/connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](../setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar el radio a una frecuencia (ingresar MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Seleccionar un ancho de filtro preestablecido para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Configurar la potencia de salida RF](../../features/tx/set-rf-output-power.md)
- [Iniciar una portadora de ajuste para verificar el SWR](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](../../features/tx/run-the-internal-atu.md)
- [Activar MOX para accionar manualmente el transmisor](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Usar RIT para desplazar la frecuencia de recepción ante una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Bloquear el slice para evitar sintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Comprensión de slices y VFOs](../concepts/understanding-slices.md)

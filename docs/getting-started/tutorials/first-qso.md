# Realice su primer QSO con AetherSDR

Esta página le guía a través de la conexión a su FLEX-8600, la sintonización de una frecuencia, la verificación de los ajustes de antena y potencia, y la realización de un contacto. Siga estos pasos en orden la primera vez que use AetherSDR.

## Antes de comenzar

- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora, o tiene credenciales de SmartLink y una radio remota disponible.
- AetherSDR está instalado y en ejecución.
- Usted sabe qué banda y modo desea operar (por ejemplo, 14.225 MHz USB).
- Su micrófono o keyer está conectado y configurado en la radio.

## Pasos

### 1. Conéctese a la radio

1. Cuando no hay ninguna radio conectada, AetherSDR muestra el panel **Connect to a Radio** en la ventana principal. Si ya lo cerró, ábralo mediante `Settings > Connect to Radio...`.
2. El modo predeterminado es **Local**. Si su radio está en la misma LAN, déjelo seleccionado.
3. Espere unos segundos a que la lista **Available radios** se complete mediante el descubrimiento automático. Su FLEX-8600 debería aparecer por nombre.
4. Haga clic en su radio en la lista **Available radios** para resaltarla.
5. Haga clic en **Connect Selected Radio**.
6. La etiqueta de estado cambia de "searching" a "connecting" y finalmente a "connected". La vista principal del panadapter se abre cuando la conexión se establece correctamente.

Si la lista permanece vacía, haga clic en **Retry Discovery**. Si la radio está en una subred diferente, haga clic en **Connect by IP** e ingrese la dirección IP de la radio en el campo **Radio IP address**, luego haga clic en **Connect by IP (manual)**. El campo **Radio IP address** es un menú desplegable que también muestra hasta tres direcciones usadas anteriormente; seleccione una entrada reciente o escriba una nueva. Para una radio remota a través de internet, haga clic en **Remote with SmartLink** e inicie sesión.

Por defecto, **Connect to last radio on start up** está marcado, por lo que AetherSDR se reconectará automáticamente a la radio usada más recientemente cada vez que se inicie. Si prefiere elegir una radio manualmente en cada inicio, desmarque esta opción en el panel **Connect to a Radio**. La configuración se guarda inmediatamente cuando la cambia (`AutoConnectToLastRadio`).

Al conectar manualmente por IP, seleccione la interfaz de red local en el cuadro combinado **Advanced: Source path**. La **Source warning label** aparece debajo de este cuadro combinado cuando la NIC guardada previamente ya no es accesible. Seleccione una interfaz de origen válida antes de hacer clic en **Connect by IP (manual)**.

Si la lista **Available radios** llena el espacio disponible, aparece una barra de desplazamiento vertical para que todas las entradas permanezcan accesibles incluso en pantallas pequeñas. Haga clic derecho en una radio de la lista para establecer un apodo personalizado (esto se almacena localmente y está disponible para radios que no son Flex, como HL2 o backends simulados).

### 2. Seleccione la antena correcta

1. En la barra lateral derecha, haga clic en el botón de la bandeja **RX** para abrir el applet RX Controls (es visible por defecto).
2. Busque el cuadro combinado de antena con etiqueta azul (antena RX, por defecto **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena receptora.
3. Busque el cuadro combinado de antena con etiqueta roja (antena TX, por defecto **ANT1**). Haga clic en él y seleccione el puerto de antena al que está conectada su antena transmisora. Los puertos solo de RX no aparecen listados aquí.

### 3. Establezca el modo de operación y la frecuencia

1. En el applet RX Controls, haga clic en el **Mode combo** y seleccione su modo — por ejemplo, **USB** para telefonía en banda lateral superior.
2. Haga clic en la **Frequency label** para cambiarla al modo de edición (aparece el campo **Frequency edit**).
3. Escriba su frecuencia objetivo en MHz (por ejemplo, `14.225`) y presione **Enter**. El panadapter se recentra en la nueva frecuencia. Presione **Escape** para cancelar sin cambiar la frecuencia.
4. Elija un ancho de filtro haciendo clic en uno de los botones de **Filter width presets**. Para USB, los presets disponibles son 1800, 2100, 2400, 2700, 2900 y 3300 Hz. 2700 Hz es un punto de partida común para SSB.

### 4. Establezca la potencia de transmisión

1. Haga clic en el botón de la bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls.
2. Arrastre el control deslizante **RF Power** hasta el nivel de potencia deseado (por defecto **100**, rango 0–100). Observe el medidor **RF Pwr** durante una transmisión para confirmar la salida real.
3. Revise el medidor **SWR**. Una lectura superior a 2.5 se muestra en rojo; investigue su sistema de antenas antes de transmitir si es así.
4. Si desea ejecutar primero la ATU interna, haga clic en **ATU** y espere a que el ciclo se complete. El indicador **Success** se enciende en verde cuando se encuentra una concordancia.

### 5. Verifique el audio y la ganancia

1. De vuelta en el applet RX Controls, confirme que el control deslizante **AF gain** esté en un nivel de escucha cómodo (por defecto **70**, rango 0–100).
2. Confirme que el cuadro combinado **AGC mode** esté en **Med** (el predeterminado) para SSB. Ajústelo a **Slow** o **Fast** si es necesario.
3. Si no escucha audio, verifique que el conmutador de silencio (🔊/🔇) muestre el estado sin silencio.

### 6. Realice el contacto

1. Escuche en la frecuencia. Cuando esté listo para llamar, active su micrófono o keyer.
2. Para transmitir usando el keying por software, haga clic en **MOX** en el applet TX Controls. El botón se pone rojo mientras transmite. Haga clic en **MOX** nuevamente para volver a recibir.
3. Observe el medidor **RF Pwr** para confirmar la salida, y el medidor **SWR** para confirmar que la antena está concordada.
4. Cuando el QSO esté completo, haga clic en **MOX** para asegurarse de estar de nuevo en recepción, o simplemente suelte su PTT de hardware.

## Consejos

- Si la otra estación está ligeramente fuera de frecuencia y no desea mover su VFO, active **RIT** en el applet RX Controls y use la caja de giro **RIT offset** (pasos de 10 Hz) para desplazar su frecuencia de recepción sin cambiar la de transmisión. Haga clic en **RIT 0** para ponerla a cero después.
- Para evitar resintonizar accidentalmente durante un QSO, haga clic en el conmutador 🔓 en el applet RX Controls para bloquear el slice. El icono cambia a 🔒.
- El control deslizante **L / R pan** (por defecto **50**, rango 0–100) le permite posicionar el audio de este slice en el campo estéreo. Haga doble clic para restablecerlo al centro. El control deslizante muestra "C" en el centro, "L5" en 45, "R10" en 60, y así sucesivamente. El control deslizante tiene un relleno anclado al centro: el color de acento se extiende desde el centro hacia afuera en dirección a la posición del control, para que pueda ver el balance de paneo de un vistazo.
- Si opera en split, use **XIT** en el applet RX Controls para desplazar su frecuencia de transmisión independientemente del VFO de recepción.
- Use los atajos de teclado **widen** y **narrow** para recorrer los presets de filtro por modo. El método `stepFilterWidth(direction)` recorre la lista de presets por modo, por lo que la geometría del borde del filtro siempre es correcta para el modo activo (USB, LSB, CW, AM, DIGL, etc.). Por ejemplo, al presionar un atajo de widen en modo CW, recorre los presets de 50, 100, 250, 400 Hz, mientras que en USB recorre los presets de 1800, 2100, 2400, 2700, 2900, 3300 Hz.
- Haga clic una vez en el botón de silencio (🔊) para silenciar o reactivar el audio de este slice. Haga doble clic para silenciar o reactivar todos los slices propios a la vez.
- Cambiar a modos RTTY o digitales (DIGU, DIGL) desactiva automáticamente el squelch, que de otro modo eliminaría los caracteres FSK y rompería la decodificación.
- Al ingresar una frecuencia, puede escribir un valor superior a 54 MHz (por ejemplo, `144.6`) y será aceptado como entrada VHF/UHF. Anteriormente esto solo estaba permitido cuando el slice ya estaba en una antena XVTR.

## Solución de problemas

- **La lista Available radios está vacía** — Haga clic en **Retry Discovery**. Verifique que la radio esté encendida y en el mismo segmento de red. Haga clic en **Open Network Diagnostics** para inspeccionar la ruta. Si la radio está en una subred diferente, use **Connect by IP (manual)** en su lugar.
- **No hay audio del altavoz** — Verifique que el conmutador de silencio en el applet RX Controls muestre el estado sin silencio (🔊). Verifique que **AF gain** sea superior a 0. Verifique la configuración del dispositivo de audio en su sistema operativo.
- **MOX activa pero el medidor RF Pwr lee cero** — Confirme que la antena TX correcta esté seleccionada en el cuadro combinado de antena TX con etiqueta roja. Confirme que **RF Power** sea superior a 0 en el applet TX Controls.
- **El medidor SWR lee en rojo (superior a 2.5)** — No continúe transmitiendo a plena potencia. Verifique las conexiones de la antena. Ejecute la **ATU** interna para encontrar una concordancia, o reduzca la potencia hasta que el problema se resuelva.
- **El campo de edición de frecuencia no acepta el valor** — Asegúrese de ingresar un valor en MHz dentro del rango válido (0.001–54.000 MHz para HF, o hasta 50,000 MHz para entradas XVTR y VHF/UHF). Presione **Escape** para cancelar y restaurar la frecuencia anterior.
- **El menú desplegable de dirección IP de la radio muestra una dirección obsoleta** — La **Source warning label** aparece debajo del cuadro combinado **Advanced: Source path** cuando la NIC guardada previamente ya no es accesible. Seleccione una interfaz de origen válida antes de hacer clic en **Connect by IP (manual)**.
- **La ventana de conexión no es visible o no restauró su tamaño anterior** — Al entrar o salir del modo sin marcos, la ventana restaura su geometría solo si era visible anteriormente. Si la ventana de conexión aparece en una posición inesperada, redimensiónela o reubíquela normalmente y recordará esas dimensiones la próxima vez.
- **Algunas entradas de radio en la lista Available radios no son visibles** — La lista ahora tiene una altura máxima fija y una barra de desplazamiento vertical para que todas las entradas permanezcan accesibles en pantallas pequeñas. Use la barra de desplazamiento o la rueda del mouse para ver las radios debajo del área visible.

## Relacionados

- [Conectarse a una radio LAN local](../setup/connect-to-a-local-lan-radio.md)
- [Conectarse a una radio remota a través de SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](../setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escriba MHz en la lectura)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Elegir un preset de ancho de filtro para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Establecer la potencia de salida de RF](../../features/tx/set-rf-output-power.md)
- [Iniciar una portadora de prueba para verificar el SWR](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Ejecutar la ATU interna](../../features/tx/run-the-internal-atu.md)
- [Alternar MOX para keyear el transmisor manualmente](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Usar RIT para desplazar la frecuencia de recepción para una estación a la deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Usar XIT para desplazar la frecuencia de transmisión sin cambiar RX](../../features/rx/use-xit-to-offset-the-transmit-frequency-without-changing-rx.md)
- [Bloquear el slice para evitar resintonización accidental](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Comprender los slices y los VFO](../concepts/understanding-slices.md)

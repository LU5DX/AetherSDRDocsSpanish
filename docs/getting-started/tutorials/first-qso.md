# Realice su primer QSO con AetherSDR

Esta página le guía por el proceso de conectarse a su FLEX-8600, sintonizar una frecuencia, verificar la configuración de transmisión y establecer un contacto. La primera vez, siga los pasos en orden.

## Antes de comenzar

- AetherSDR está instalado y en ejecución.
- Su FLEX-8600 está encendido y accesible — ya sea en la misma LAN, a través de SmartLink o mediante una dirección IP conocida.
- Su micrófono y auriculares están configurados en los ajustes de audio del radio.
- Conoce la frecuencia y el modo de la estación con la que desea comunicarse.

## Pasos

### 1. Conéctese a su radio

1. El panel **Connect to a Radio** aparece en la ventana principal. Si no aparece, vaya a `Settings > Connect to Radio...`.
2. Seleccione **Local** si el radio está en su LAN. Espere unos segundos a que la lista **Available radios** se rellene.
3. Resalte su radio en la lista **Available radios**.
4. Haga clic en **Connect Selected Radio**.

La etiqueta de estado avanza por "searching" y "connecting" y luego muestra "connected" cuando se establece el enlace. El panel de applets se activa en el lado derecho.

> Si la lista permanece vacía, haga clic en **Retry Discovery**. Si el radio está en una subred diferente o en una VPN, haga clic en **Connect by IP** y consulte [Conectarse por IP a través de una VPN o red enrutada](../setup/connect-by-ip-across-a-vpn-or-routed-network.md).

### 2. Abra el applet RX Controls

Haga clic en el botón **RX** de la barra lateral derecha para expandir el applet RX Controls. El slice **A** está seleccionado de forma predeterminada.

### 3. Establezca el modo de operación

En el **Mode combo**, seleccione el modo que corresponde al contacto que desea realizar — por ejemplo, **USB** para la mayoría de las comunicaciones telefónicas en HF, **LSB** para las bandas de 40/80/160 m en teléfono, o **CW** para Morse.

Los preajustes de filtro debajo del indicador de frecuencia se actualizan automáticamente según el modo elegido.

### 4. Sintonice la frecuencia

1. Haga clic en la **Frequency label** (que muestra una lectura punteada como `0.000.000`). Esta se convierte en un campo de edición.
2. Escriba la frecuencia en MHz — por ejemplo, `14.225` para 14.225 MHz.
3. Presione **Enter**. El radio sintoniza y el panadapter se recentra en la nueva frecuencia.

Si necesita cancelar sin cambiar la frecuencia, presione **Escape**.

### 5. Elija el ancho de filtro

Haga clic en uno de los botones **Filter width presets** para seleccionar el ancho de banda adecuado para su modo. Para SSB las opciones son 1800, 2100, 2400, 2700, 2900 y 3300 Hz. El ancho de filtro actual se muestra en la **Filter width label** (por ejemplo, `2.7K`).

### 6. Verifique la antena de recepción

Confirme que el combo **ANT1 (RX antenna)** muestra la antena en la que desea recibir. Cámbielo si es necesario.

### 7. Ajuste la ganancia AF

Ajuste el control deslizante **AF gain** para escuchar cómodamente. El valor predeterminado es 70 (rango 0–100).

### 8. Abra el applet TX Controls

Haga clic en el botón **TX** de la barra lateral derecha para expandir el applet TX Controls.

### 9. Establezca la potencia de transmisión

Mueva el control deslizante **RF Power** al nivel de salida deseado. El valor predeterminado es 100 (rango 0–100). Observe el medidor **RF Pwr** y el medidor **SWR** durante el siguiente paso.

### 10. Verifique la antena de transmisión

De vuelta en el applet RX Controls, confirme que el combo **ANT1 (TX antenna)** muestra la antena de transmisión correcta para esta banda.

### 11. Compruebe el SWR con una portadora de ajuste (opcional pero recomendado)

1. En el applet TX Controls, ajuste el control deslizante **Tune Pwr** a un nivel bajo (el valor predeterminado es 10).
2. Haga clic en **TUNE**. La etiqueta del botón cambia a **TUNING...** con fondo rojo mientras la portadora está activa.
3. Lea el medidor **SWR**. Cuando esté satisfecho, haga clic en **TUNE** nuevamente para detenerla.

Una buena lectura de SWR (por debajo de 2.0) indica que su sistema de antena está listo.

### 12. Establezca el contacto

Cuando la frecuencia esté libre y la otra estación esté lista:

1. Active su micrófono o manipulador. El radio pasará a transmitir.
2. Para activar el transmisor manualmente durante pruebas, haga clic en **MOX** en el applet TX Controls. El botón se vuelve rojo mientras la transmisión está activa. Haga clic en **MOX** nuevamente para volver a recepción.
3. Observe el medidor **RF Pwr** para confirmar la potencia de salida y el medidor **SWR** para confirmar el comportamiento de la antena.

## Consejos

- Si está trabajando con una estación que está ligeramente fuera de su frecuencia de recepción, active **RIT** en el applet RX Controls y use el spinbox **RIT offset** para desplazar la recepción sin mover su frecuencia de transmisión. Haga clic en **RIT 0** para zerarlo al terminar.
- Si escucha retroalimentación de su propia transmisión, reduzca el **AF gain** durante la transmisión o use auriculares.
- Los controles deslizantes **RF Power** y **Tune Pwr**, el combo **TX Profile** y los selectores de antena mantienen su estado entre sesiones para el mismo radio.
- Para evitar resintonizar accidentalmente el slice durante un QSO, haga clic en el botón de alternancia 🔓 en el applet RX Controls para bloquear la frecuencia. Cambia a 🔒 cuando está bloqueado.

## Solución de problemas

- **Aparece "No local radios found yet" y la lista permanece vacía** — Haga clic en **Retry Discovery**. Compruebe que el radio esté encendido y en el mismo segmento de red. Si está en una subred diferente, use **Connect by IP** o SmartLink.
- **MOX activa el radio pero el medidor RF Pwr muestra cero** — Compruebe que el control deslizante **RF Power** esté por encima de 0 y que la antena TX correcta esté seleccionada en el combo **ANT1 (TX antenna)**.
- **El SWR aparece en rojo (por encima de 2.5)** — Revise sus conexiones de coaxial y antena. Active el ATU interno si su equipo lo incluye: haga clic en **ATU** en el applet TX Controls.
- **El audio es muy bajo o está ausente en recepción** — Compruebe el control deslizante **AF gain** (valor predeterminado 70) y confirme que el interruptor de silencio 🔊 / 🔇 esté en el estado sin silencio (🔊).

## Relacionados

- [Conectarse a un radio en LAN local](../setup/connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](../setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Iniciar una portadora de ajuste para comprobar el SWR](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de salida RF](../../features/tx/set-rf-output-power.md)
- [Activar el ATU interno](../../features/tx/run-the-internal-atu.md)
- [Usar RIT para desplazar la frecuencia de recepción de una estación con deriva](../../features/rx/use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)

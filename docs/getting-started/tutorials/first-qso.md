# Haga su primer QSO con AetherSDR

Esta página le guía a través del proceso de conexión a su FLEX-8600, sintonización de una frecuencia y realización de un contacto de voz. Siga los pasos en orden la primera vez.

## Antes de comenzar

- AetherSDR está instalado y en ejecución en su computadora.
- Su FLEX-8600 está encendido y accesible — ya sea en la misma LAN o a través de SmartLink.
- Hay una antena conectada al radio.
- Conoce la frecuencia y el modo de la estación con la que desea trabajar.

## Pasos

### 1. Conéctese al radio

1. La pantalla "Connect to a Radio" aparece automáticamente en la ventana principal cuando no hay ningún radio conectado. Si no aparece, elija `Settings > Connect to Radio...`.
2. El modo predeterminado es **Local**. Si su radio está en la misma red, aparecerá en la lista **Available radios** en pocos segundos.
3. Seleccione su radio en la lista.
4. Haga clic en **Connect Selected Radio**.
5. Si no aparece ningún radio, haga clic en **Retry Discovery** y espere. Si el radio aún no se encuentra, consulte [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md).

### 2. Abra el applet RX Controls

1. El botón **RX** está en la barra lateral derecha (Panel de applets). Haga clic en él si el panel RX Controls no está visible todavía.

### 3. Establezca el modo

1. En el applet RX Controls, busque el **Mode combo** (muestra **USB** de forma predeterminada).
2. Haga clic en él y seleccione el modo que corresponde al contacto — por ejemplo, **USB** para un contacto SSB en 20 m, o **LSB** para 40 m/80 m.

### 4. Sintonice la frecuencia

1. Haga clic en el **Frequency label** (la pantalla grande con puntos, p. ej. `0.000.000`). Se convierte en un campo editable.
2. Escriba la frecuencia en MHz — por ejemplo:
   ```
   14.225
   ```
3. Presione **Enter**. El radio sintoniza esa frecuencia y el panadapter se recentra.

### 5. Establezca el ancho de filtro

1. En el applet RX Controls, haga clic en uno de los botones **Filter width presets** para elegir un ancho de banda de recepción adecuado para el modo. Para SSB, 2700 Hz es un punto de partida habitual.

### 6. Verifique el audio de recepción

1. Confirme que el control deslizante **AF gain** no está en cero (el valor predeterminado es 70).
2. Confirme que el botón de silencio 🔊 / 🔇 está en estado activo (🔊).
3. Escuche las señales en el panadapter y en el audio.

### 7. Abra el applet TX Controls

1. Haga clic en el botón **TX** de la barra lateral derecha para abrir el applet TX Controls.

### 8. Establezca la potencia de transmisión

1. Ajuste el control deslizante **RF Power** al nivel de salida deseado (el valor predeterminado es 100; el rango válido es 0–100).

### 9. Verifique que este slice sea el slice de TX

1. En el applet RX Controls, confirme que el indicador **TX (badge)** está iluminado para el slice **A** (el slice predeterminado). Si no lo está, haga clic en el botón **TX (badge)** para designar este slice como el slice de transmisión.

### 10. Verifique la antena de TX

1. En el applet RX Controls, confirme que el cuadro combinado rojo **ANT1 (TX antenna)** muestra la antena por la que desea transmitir. Haga clic en él para cambiarla si es necesario.

### 11. Verifique el ROS antes de transmitir (recomendado)

1. En el applet TX Controls, haga clic en **TUNE**. La etiqueta del botón cambia a **TUNING...** y se transmite una portadora al nivel **Tune Pwr** (predeterminado 10).
2. Observe el medidor de **SWR**. Una lectura claramente por debajo de 2.5 es aceptable. El rojo comienza por encima de 2.5.
3. Haga clic en **TUNE** nuevamente (o espere a que finalice) para detener la portadora.
4. Si el ROS es elevado, verifique la conexión de la antena o active el ATU interno — consulte [Activar el ATU interno](../../features/tx/run-the-internal-atu.md).

### 12. Transmita

1. Active el micrófono normalmente (VOX, pedal o PTT) para transmitir. También puede hacer clic en **MOX** en el applet TX Controls para activar el transmisor manualmente — el botón se pone rojo durante la transmisión.
2. Hable y luego suelte el PTT o haga clic en **MOX** nuevamente para volver a recepción.

### 13. Confirme el contacto

1. Registre el QSO en su aplicación de registro preferida.

## Consejos

- El valor predeterminado del control deslizante **AF gain** es 70 y el del control deslizante **L / R pan** es 50 (centro). Al hacer doble clic en el control de paneo, este se restablece al centro.
- El cuadro combinado **AGC mode** tiene como valor predeterminado **Med**. Si las señales son muy fuertes o muy débiles, pruebe **Slow** o **Fast**.
- Si resintoniza accidentalmente el VFO mientras transmite o registra, haga clic en el botón 🔓 del applet RX Controls para bloquear la frecuencia del slice. El ícono cambia a 🔒 cuando está bloqueado.
- El control deslizante **RF Power** establece la potencia como un porcentaje de la salida máxima del radio, no directamente en watts. Observe el medidor **RF Pwr** en el applet TX Controls para ver la potencia directa real.

## Solución de problemas

- **No aparece ningún radio en la lista Available radios** — Es posible que el radio no esté en la misma subred, o que el descubrimiento no haya finalizado. Haga clic en **Retry Discovery**. Si sigue sin aparecer, intente conectarse por IP: consulte [Conectarse por IP a través de una VPN o red enrutada](../setup/connect-by-ip-across-a-vpn-or-routed-network.md).
- **Sin audio de recepción** — Verifique que el botón de silencio muestre 🔊 (sin silencio) y que el control deslizante **AF gain** esté por encima de cero. Compruebe también que la salida de audio del sistema esté configurada correctamente.
- **MOX activa el radio pero el ROS es muy alto** — Detenga la transmisión de inmediato. Verifique que la antena esté conectada y que el puerto **ANT1 (TX antenna)** correcto esté seleccionado. Active el ATU si está instalado.
- **El Frequency label no acepta entrada del teclado** — Haga clic directamente sobre la pantalla de frecuencia para entrar en modo de edición, luego escriba el valor en MHz y presione **Enter**.

## Relacionados

- [Conectarse a un radio en LAN local](../setup/connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en la pantalla)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preset de ancho de filtro para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Establecer la potencia de salida de RF](../../features/tx/set-rf-output-power.md)
- [Iniciar una portadora de ajuste para verificar el ROS](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Activar el ATU interno](../../features/tx/run-the-internal-atu.md)
- [Alternar MOX para activar manualmente el transmisor](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)

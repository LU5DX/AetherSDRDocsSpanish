# Realice su primer QSO con AetherSDR

Este tutorial le guía a través de la conexión a su FLEX-8600, la sintonización a una frecuencia y el establecimiento de un contacto de voz con AetherSDR por primera vez.

## Antes de comenzar

- AetherSDR está instalado y en ejecución.
- Su FLEX-8600 está encendido y accesible en la red local, o dispone de credenciales SmartLink para acceso remoto.
- Un micrófono y auriculares están conectados y configurados en su sistema operativo.

## Pasos

### 1. Conectarse al radio

1. El panel **Connect to a Radio** aparece automáticamente en la ventana principal cuando no hay ningún radio conectado. Si no está visible, haga clic en `Settings > Connect to Radio...`.
2. Haga clic en **Local** si su radio está en la misma LAN. AetherSDR ejecuta descubrimiento mDNS; su FLEX-8600 aparece en la lista **Available radios** en pocos segundos.
3. Si la lista está vacía, haga clic en **Retry Discovery** y espere un momento.
4. Seleccione su radio en la lista **Available radios**.
5. Haga clic en **Connect Selected Radio**.

La etiqueta de estado se actualiza a medida que avanza la conexión. Cuando muestra el estado conectado, el panadapter de la ventana principal se activa.

### 2. Abrir el applet RX Controls

Haga clic en el botón de bandeja **RX** en la barra lateral derecha para abrir el applet RX Controls. El applet muestra el slice (receptor virtual) **A** de forma predeterminada.

### 3. Elegir un modo

En el cuadro combinado **Mode combo**, seleccione el modo que corresponda al contacto que desea realizar — por ejemplo, **USB** para un QSO de fonía en HF por encima de 10 MHz, o **LSB** por debajo de 10 MHz.

### 4. Sintonizar una frecuencia

1. Haga clic en la etiqueta **Frequency label** (que muestra la lectura actual del VFO, p. ej. `0.000.000`). Se convierte en un campo editable.
2. Escriba la frecuencia en MHz — por ejemplo, `14.225` para fonía SSB en 20 m.
3. Presione **Enter**. El radio se sintoniza y el panadapter se recentra en la nueva frecuencia.

Para incrementar o reducir la frecuencia paso a paso, use los botones de flecha del cuadro **STEP** o desplace la rueda del ratón sobre él. El paso predeterminado es 100 Hz; los pasos disponibles para SSB son 1, 10, 50, 100, 500, 1000, 2000 y 3000 Hz.

### 5. Establecer el ancho de filtro

Haga clic en uno de los botones **Filter width presets** para aplicar una banda de paso estándar. Para USB o LSB, los preajustes disponibles son 1800, 2100, 2400, 2700, 2900 y 3300 Hz. El preajuste **2.7K** es un punto de partida razonable para un QSO de fonía.

### 6. Ajustar el audio de recepción

- Ajuste el deslizador **AF gain** a un nivel de escucha cómodo. El valor predeterminado es 70 (rango 0–100).
- Ajuste el combinado **AGC mode** a **Med** (el valor predeterminado) para operación telefónica típica.
- Si escucha interferencia en un oído, centre el deslizador **L / R pan** en 50. Haga doble clic en el deslizador para restablecerlo al centro de inmediato.

### 7. Escuchar antes de transmitir

Monitoree la frecuencia para detectar actividad. Use el panadapter para observar señales. Si una estación llama CQ o desea responder a una, continúe con el paso siguiente.

### 8. Abrir el applet TX Controls

Haga clic en el botón de bandeja **TX** en la barra lateral derecha para abrir el applet TX Controls.

### 9. Establecer la potencia de transmisión

Mueva el deslizador **RF Power** al nivel de salida deseado. El valor predeterminado es 100 (rango 0–100). Observe el medidor **RF Pwr** y el medidor **SWR** al transmitir; el SWR debe mantenerse claramente por debajo de 2.5 para una operación normal.

### 10. Seleccionar un perfil TX

Si tiene perfiles de transmisión configurados, elija uno del cuadro combinado **TX Profile** que corresponda a su modo de operación (por ejemplo, un perfil configurado para fonía SSB).

### 11. Confirmar el slice TX

En el applet RX Controls, compruebe que la insignia **TX** esté iluminada en el slice **A** (o el slice que esté usando). Si no lo está, haga clic en la insignia **TX** para establecer ese slice como el slice de transmisión.

### 12. Transmitir

Active su micrófono y haga clic en **MOX** en el applet TX Controls. El botón MOX se vuelve rojo durante la transmisión. Observe que el medidor **RF Pwr** confirme la potencia de salida. Haga clic en **MOX** nuevamente para volver a recepción cuando termine de hablar.

### 13. Completar el QSO

Vuelva a recepción, copie el reporte de la otra estación e intercambie reportes de señal como de costumbre. Cuando finalice el contacto, haga clic en **MOX** si necesita transmitir de nuevo, o simplemente permanezca en recepción.

## Consejos

- Si el medidor SWR muestra un valor superior a 2.5, deje de transmitir y revise su sistema de antena antes de continuar. La zona roja del indicador SWR comienza en 2.5.
- El deslizador **Tune Pwr** (predeterminado 10, rango 0–100) controla la potencia de portadora durante el ajuste de antena. Úselo junto con el botón **TUNE** para verificar el SWR a potencia reducida antes de un QSO.
- Si mueve accidentalmente el VFO, haga clic en el botón de alternancia 🔓 en el applet RX Controls para bloquear el slice e impedir una resintonización no deseada.
- Hacer doble clic en el deslizador **L / R pan** lo restablece al centro (50).

## Solución de problemas

- **Aparece "No local radios found yet" y la lista permanece vacía** — Verifique que el radio esté encendido y en el mismo segmento de red. Haga clic en **Retry Discovery**. Si el problema persiste, haga clic en **Open Network Diagnostics** para obtener más detalles.
- **MOX se vuelve rojo pero el medidor RF Pwr no muestra salida** — Confirme que la antena TX correcta esté seleccionada en el cuadro combinado **ANT1 (TX antenna)** del applet RX Controls. Verifique también que el dispositivo de entrada de audio esté activo en su sistema operativo.
- **El audio recibido es muy bajo o está ausente** — Compruebe el deslizador **AF gain** (predeterminado 70) y confirme que el slice no esté silenciado (el botón de alternancia 🔊 / 🔇 debe mostrar 🔊).

## Relacionados

- [Conectarse a un radio en la LAN local](../setup/connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en la lectura)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Establecer la potencia de salida de RF](../../features/tx/set-rf-output-power.md)
- [Iniciar una portadora de ajuste para verificar el SWR](../../features/tx/start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar el transmisor manualmente](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Seleccionar la antena RX o TX para este slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Entender los slices y los VFOs](../concepts/understanding-slices.md)

# Realice su primer QSO con AetherSDR

Esta página lo guía paso a paso para conectarse a su FLEX-8600, sintonizar una frecuencia y realizar un contacto de voz con AetherSDR por primera vez.

## Antes de comenzar

- Su FLEX-8600 está encendido y conectado a la misma LAN que su computadora, o dispone de credenciales SmartLink para acceso remoto.
- AetherSDR está instalado y en ejecución.
- El micrófono y el audio de auriculares/altavoz están configurados en los ajustes de audio del radio.

## Pasos

### 1. Conectarse al radio

1. El ConnectionPanel aparece en la ventana principal cuando no hay ningún radio conectado. Si no está visible, haga clic en `Settings > Connect to Radio...`.
2. Haga clic en `Local` para buscar radios en su LAN. Espere unos segundos a que la lista `Available radios` se llene.
3. Si la lista permanece vacía y aparece el indicador `No local radios found yet`, haga clic en `Retry Discovery`.
4. Haga clic en su FLEX-8600 en la lista `Available radios` para seleccionarlo.
5. Haga clic en `Connect Selected Radio`.

La etiqueta de estado en la parte inferior del ConnectionPanel cambia de "searching" a "connecting" y finalmente a "connected" cuando se establece el enlace. El panadapter de la ventana principal se activa.

### 2. Abrir el applet RX Controls

1. Haga clic en el botón de bandeja `RX` en la barra lateral derecha para abrir el applet RX Controls.
2. Si el radio tiene más de un slice (canal de recepción) configurado, haga clic en la pestaña del slice (`A`, `B`, etc.) que desea utilizar. El Slice A es el slice de inicio predeterminado.

### 3. Establecer el modo

1. En el applet RX Controls, localice el `Mode combo`.
2. Haga clic en él y seleccione `USB` para un contacto SSB telefónico típico (o `LSB` para 40 m y bandas inferiores).

### 4. Sintonizar una frecuencia

1. Haga clic en el `Frequency label` en el applet RX Controls. El campo se vuelve editable.
2. Escriba la frecuencia en MHz — por ejemplo:
   ```
   14.225
   ```
3. Presione `Enter`. El radio se sintoniza en esa frecuencia y el panadapter se recentra.

### 5. Elegir el ancho de filtro

1. Observe los botones de preajuste de ancho de filtro en el applet RX Controls.
2. Haga clic en `2700` (2700 Hz) para una banda de paso SSB estándar, o elija un preajuste más estrecho si la banda está congestionada. El indicador `2.7K` se actualiza para confirmar el ancho activo.

### 6. Ajustar el nivel de audio de recepción

1. Compruebe que el interruptor de silencio muestre 🔊 (sin silencio).
2. Ajuste el control deslizante `AF gain` de modo que el audio entrante sea cómodo. El valor predeterminado es 70 (rango 0–100).

### 7. Abrir el applet TX Controls

1. Haga clic en el botón de bandeja `TX` en la barra lateral derecha para abrir el applet TX Controls.

### 8. Establecer la potencia de transmisión

1. Ajuste el control deslizante `RF Power` al nivel de salida deseado. El valor predeterminado es 100 (rango 0–100).
2. Compruebe el control deslizante `Tune Pwr` — el valor predeterminado es 10 (rango 0–100). Déjelo en 10 para una sintonización breve del ATU si es necesario.

### 9. Verificar la antena

1. En el applet RX Controls, confirme que el selector de antena TX (el selector de antena con etiqueta roja) muestra el puerto de antena correcto para su banda.
2. En el applet TX Controls, observe el medidor `SWR` cuando transmita. Una lectura superior a 2.5 ilumina la zona roja; utilice el ATU si es necesario.

### 10. Realizar el contacto

1. Para activar el transmisor manualmente, haga clic en `MOX` en el applet TX Controls. El botón se pone rojo mientras la transmisión está activa. Hable por su micrófono.
2. Haga clic en `MOX` nuevamente para volver a recepción.
3. Observe el medidor `RF Pwr` para confirmar que la potencia llega a la antena mientras transmite.

## Consejos

- El control giratorio `STEP` en el applet RX Controls determina cuánto se desplaza el VFO con cada clic o movimiento de la rueda del ratón. Para SSB, 100 Hz (el valor predeterminado) es un buen paso inicial.
- El control deslizante `L / R pan` tiene un valor predeterminado de 50 (centro). Haga doble clic en él para restablecer el centro si lo ha movido.
- Si mueve la frecuencia accidentalmente, haga clic en el interruptor 🔓 / 🔒 en el applet RX Controls para bloquear el slice contra resintonizaciones involuntarias.
- El selector `AGC mode` tiene como valor predeterminado `Med`. Si las señales son muy fuertes y causan distorsión, pruebe con `Slow`.

## Solución de problemas

- **`No local radios found yet` y `Retry Discovery` no ayuda** — Verifique que el radio y la computadora estén en la misma subred. Haga clic en `Open Network Diagnostics` en el ConnectionPanel para obtener más detalles.
- **MOX activa el radio pero el medidor `RF Pwr` permanece en cero** — Confirme que el selector de antena TX en el applet RX Controls no esté configurado en un puerto solo de recepción (los puertos con el prefijo "RX" se excluyen de la lista TX, pero verifique que la selección sea correcta para su configuración).
- **El SWR muestra un valor muy alto inmediatamente al transmitir** — Ejecute el ATU interno antes de realizar el contacto. Haga clic en `ATU` en el applet TX Controls y espere a que el indicador `Success` se ilumine en verde.

## Relacionados

- [Conectarse a un radio local en LAN](../setup/connect-to-a-local-lan-radio.md)
- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](../../features/rx/tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](../../features/rx/change-mode-usb-lsb-cw-am-fm-etc.md)
- [Seleccionar un preajuste de ancho de filtro para el modo actual](../../features/rx/pick-a-filter-width-preset-for-the-current-mode.md)
- [Seleccionar la antena RX o TX para este slice](../../features/rx/select-the-rx-or-tx-antenna-for-this-slice.md)
- [Ajustar la potencia de salida de RF](../../features/tx/set-rf-output-power.md)
- [Ejecutar el ATU interno](../../features/tx/run-the-internal-atu.md)
- [Activar MOX para transmitir manualmente](../../features/tx/toggle-mox-to-manually-key-the-transmitter.md)
- [Bloquear el slice para evitar resintonizaciones accidentales](../../features/rx/lock-the-slice-to-prevent-accidental-retuning.md)
- [Conectarse a un radio remoto mediante SmartLink](../setup/connect-to-a-remote-radio-through-smartlink.md)

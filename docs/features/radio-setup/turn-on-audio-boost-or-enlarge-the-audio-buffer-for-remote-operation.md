# Activar el aumento de audio o ampliar el búfer de audio para operación remota

Use estos ajustes para compensar un volumen de recepción bajo o interrupciones de audio al operar AetherSDR a través de una conexión VPN o SmartLink. Audio Boost agrega ganancia adicional en la ruta de audio del cliente; un Audio Buffer mayor absorbe la fluctuación de red (jitter) a costa de una mayor latencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles no están disponibles cuando no hay ninguna radio conectada.
- Abra `Settings > Radio Setup...` y seleccione la pestaña **Audio** antes de seguir los pasos a continuación.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el volumen de recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra su estado activo cuando está habilitado.
4. Para reducir las interrupciones o caídas de audio, haga clic en el cuadro numérico **Audio Buffer:** e ingrese un valor entre 50 y 1000 ms. Los valores más altos añaden más almacenamiento en búfer a costa de mayor latencia.
5. Cierre el cuadro de diálogo. Los ajustes surten efecto de inmediato.

## Qué hace cada control

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | On / Off |
| **Audio Buffer:** | Establece el búfer de audio del lado del cliente para absorber la fluctuación de red. Auméntelo cuando use conexiones VPN o SmartLink con latencia inestable. | 50–1000 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto / Uncompressed / Opus |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. | On / Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. | On / Off |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0 = menor latencia, 3 = máxima nitidez) por modo; el control se deshabilita cuando Auto está activado. | 0–3 |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | On / Off |
| **Connect / Disconnect (TGXL)** | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciarse. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que dejó de funcionar en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere keying del lado del cliente. Si el campo de IP está vacío y la radio ya detectó el TGXL, la IP detectada se completa automáticamente. | — |
| **Connect / Disconnect (PGXL)** | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| **Connect / Disconnect (Antenna Genius)** | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | — |

## Pestaña RX — calibración de frecuencia

En la versión v0.9.2.1 se revisó la sección de calibración de la pestaña **RX**. El campo **Cal Frequency (MHz):** y el botón **Start** ahora son siempre visibles, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado lo confirma en verde; cuando no hay GPSDO instalado, la etiqueta aparece en ámbar. En ambos casos se permite la calibración manual de desplazamiento de frecuencia.

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz que se usará para la calibración. El campo no debe estar vacío antes de hacer clic en Start. |
| **Start** | Inicia la secuencia de calibración de frecuencia. AetherSDR restablece el error de frecuencia a 0 ppb y luego envía `radio pll_start` a la radio. El botón se deshabilita y muestra la etiqueta **Busy** mientras la calibración está en curso. Una etiqueta de estado junto al botón informa el progreso (Starting… y los estados subsiguientes). |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desplazamiento de frecuencia actual en partes por billón. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en tiempo real junto al control. |

### Cómo ejecutar una calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**. El botón cambia a **Busy** y la etiqueta de estado muestra **Starting…**.
5. Espere a que la etiqueta de estado indique la finalización. El botón se vuelve a habilitar automáticamente.
6. Si es necesario, revise el valor resultante en **Freq Offset (ppb):**.

> **Nota:** Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la secuencia no se ejecuta.

## Consejos

- Comience con un aumento moderado del búfer (200–300 ms) antes de incrementarlo más. Los valores muy grandes hacen que el audio sea notablemente lento durante los QSO.
- Si la calidad de audio es deficiente a través de SmartLink, revise también la configuración del códec (**Audio Compression (SmartLink):**). Cambiar de Auto a Opus puede reducir el ancho de banda y mejorar la estabilidad en conexiones lentas.

## Solución de problemas

- **Los controles Audio Boost y Audio Buffer aparecen atenuados o no están visibles** — Estos controles se encuentran en la pestaña **Audio**. Confirme que ha seleccionado esa pestaña y no otra, como **RX** o **Phone/CW**.
- **Aumentar el Audio Buffer no tiene efecto en las caídas de audio** — El búfer absorbe la fluctuación de red, pero no puede compensar la pérdida sostenida de paquetes. Verifique la ruta de red; consulte también [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md).
- **El botón Start permanece deshabilitado después de la calibración** — Si la radio no responde a `radio pll_start`, verifique que la radio esté conectada y no esté transmitiendo, luego intente de nuevo.

## Relacionados

- [Elegir Opus versus audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)

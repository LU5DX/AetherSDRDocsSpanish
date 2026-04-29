# Seleccionar Opus o audio sin comprimir para SmartLink

Seleccione el códec de audio que AetherSDR utiliza en las conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña compresión; el PCM sin comprimir preserva la fidelidad total cuando el ancho de banda lo permite. Auto deja que el radio elija.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Audio** no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Audio Compression (SmartLink):**, haga clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto** — el radio negocia el códec automáticamente (valor predeterminado).
   - **Uncompressed** — envía audio PCM sin procesar; utiliza más ancho de banda.
   - **Opus** — envía audio codificado con Opus; menor ancho de banda, leve compresión.
4. Cierre el cuadro de diálogo. El ajuste entra en vigor de inmediato y se guarda.

## Qué hace cada control

| Control | Predeterminado | Valores válidos |
|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Auto | Auto, Uncompressed, Opus |
| **Audio Boost:** | — | Enabled / Disabled |
| **Audio Buffer:** | 200 ms | 50–1000 ms |
| **Recording:** Radio Side / Client Side | Radio Side | Radio Side, Client Side |
| **Save to:** | — | Ruta de carpeta |
| **Auto-record on TX** | — | Checked / Unchecked |
| **Idle timeout:** | 120 sec | 10–3600 sec |
| **TX Follows Active Slice** | False | TX sigue el slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | False | Cambia el slice activo cuando TX se mueve de forma externa (por ejemplo, WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | — | 0–3. Establece la nitidez del filtro (0 = menor latencia, 3 = mayor nitidez) por modo. El control deslizante se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | — | Enabled / Disabled. Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Connect | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecta automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón **TUNE** envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que está rota en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de enclavamiento de hardware; no se requiere manipulación del lado del cliente. Si el campo IP está vacío y el radio ha detectado el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Connect | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Connect | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |
| **Cal Frequency (MHz):** | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| **Start** | — | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 y luego inicia el barrido de calibración del PLL del radio. El botón se deshabilita y muestra **Busy** mientras la calibración está en curso. |
| **Freq Offset (ppb):** | — | Desplazamiento de frecuencia manual en partes por mil millones. |

## Pestaña RX — cambios en la calibración de frecuencia en v0.9.2.1

En versiones anteriores, el campo **Cal Frequency (MHz):** y el botón **Start** solo se mostraban cuando no había un GPSDO instalado. A partir de v0.9.2.1, esos controles son siempre visibles en la pestaña **RX**. El banner de estado en la parte superior del grupo sigue indicando si hay un GPSDO presente (texto en verde) o no (texto en ámbar).

Al hacer clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, aparece un mensaje de advertencia junto al botón y la calibración no continúa.
2. El desplazamiento de frecuencia se restablece a 0 (`radio set freq_error_ppb=0`) y la frecuencia de calibración se envía al radio (`radio set cal_freq=<value>`).
3. El barrido de calibración del PLL del radio comienza (`radio pll_start`).
4. El botón **Start** se deshabilita y muestra **Busy** durante el barrido.
5. Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido y muestra el resultado al finalizar.

## Consejos

- En una LAN local rápida, **Uncompressed** evita cualquier artefacto del códec y es la mejor opción para escucha crítica o decodificación de modos digitales.
- En un enlace lento o congestionado (VPN, SmartLink celular), **Opus** reduce los cortes de audio. Combínelo con un valor mayor en **Audio Buffer:** (50–1000 ms) para absorber el jitter.
- Si el audio suena delgado o bajo de nivel a través de SmartLink, intente habilitar **Audio Boost:** junto con Opus.
- Si hay un GPSDO instalado, la calibración de frecuencia rara vez es necesaria, pero los controles siguen disponibles si desea verificar o ajustar manualmente el desplazamiento.

## Solución de problemas

- **Los botones de Audio Compression aparecen en gris o no están visibles** — la pestaña **Audio** solo se construye después de hacer clic en ella y únicamente cuando hay un radio conectado. Verifique la conexión y luego haga clic de nuevo en la pestaña **Audio**.
- **La calidad de audio es deficiente incluso con Uncompressed seleccionado** — compruebe el ancho de banda y la latencia de la red. Considere aumentar **Audio Buffer:** para reducir las interrupciones. Consulte [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).
- **El botón Start muestra "Busy" y no regresa** — si el barrido del PLL no concluye, cierre y vuelva a abrir el cuadro de diálogo Radio Setup para restablecer el estado del botón y luego inténtelo de nuevo.
- **Aparece la advertencia "Enter cal frequency" al hacer clic en Start** — escriba una frecuencia válida (en MHz) en el campo **Cal Frequency (MHz):** antes de hacer clic en **Start**.

## Temas relacionados

- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir los dispositivos de audio de entrada y salida del PC](choose-pc-input-output-audio-devices.md)
- [Habilitar la grabación automática en TX y elegir una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Cambiar el MTU de red para configuraciones VPN o remotas](change-network-mtu-for-vpn-remote-setups.md)

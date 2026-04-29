# Configurar las funciones de los pines del puerto serie de FlexControl

Use esta página para asignar una función y polaridad a los pines de salida DTR y RTS del puerto serie conectado a su FlexControl u otro dispositivo serie. Esto permite que AetherSDR controle hardware externo — como líneas PTT o entradas de manipulador — a través de las señales de control del puerto serie.

## Antes de comenzar

- El radio debe estar conectado. La pestaña **Serial** requiere una conexión activa con el radio.
- La pestaña **Serial** solo está presente cuando AetherSDR fue compilado con soporte de puerto serie (`HAVE_SERIALPORT`). Si no ve una pestaña **Serial** ni el elemento de menú `Settings > FlexControl...`, su versión no incluye esta función.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...` — esto lo lleva directamente a la pestaña **Serial** de Radio Setup. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para volver a escanear si su dispositivo no aparece, o escriba la ruta directamente en el campo **Path**.
3. Configure los parámetros de línea serie usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con los requisitos de su dispositivo.
4. Para el pin **DTR**, seleccione la función deseada en el cuadro combinado de función **DTR** y, a continuación, seleccione la polaridad activa en el cuadro combinado **Polarity** adyacente.
5. Para el pin **RTS**, repita las mismas dos selecciones — función y polaridad — usando los cuadros combinados de función **RTS** y **Polarity**.
6. Si las conexiones de su manipulador están invertidas, marque **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto automáticamente cada vez que inicie, marque **Auto-open serial port on startup**.
8. Si está conectando un mando giratorio de sintonía FlexControl, haga clic en **Detect** bajo **FlexControl Tuning Knob** para identificar el dispositivo. Haga clic en **Close** para liberarlo.
9. Para que AetherSDR detecte el mando FlexControl automáticamente al iniciar, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango / valores válidos |
|---|---|---|---|
| **Port** | Selecciona o introduce la ruta del dispositivo serie. | — | Puertos serie del sistema |
| **Refresh** | Vuelve a escanear los puertos serie disponibles. | — | — |
| **Path** | Campo editable que muestra la ruta del puerto seleccionado. | — | Cualquier ruta de dispositivo válida |
| **Baud** | Velocidad en baudios del puerto serie. | — | Según las opciones del cuadro combinado |
| **Data** | Número de bits de datos. | — | Según las opciones del cuadro combinado |
| **Parity** | Configuración de paridad. | — | Según las opciones del cuadro combinado |
| **Stop** | Número de bits de parada. | — | Según las opciones del cuadro combinado |
| **DTR: Function** | Asigna una función de señal al pin de salida DTR. | — | Según las opciones del cuadro combinado |
| **DTR: Polarity** | Establece la polaridad activa alta o activa baja para DTR. | — | Según las opciones del cuadro combinado |
| **RTS: Function** | Asigna una función de señal al pin de salida RTS. | — | Según las opciones del cuadro combinado |
| **RTS: Polarity** | Establece la polaridad activa alta o activa baja para RTS. | — | Según las opciones del cuadro combinado |
| **Paddle Swap (swap dit/dah)** | Invierte las entradas dit y dah del manipulador. | Sin marcar | Marcado / Sin marcar |
| **Auto-open serial port on startup** | Vuelve a abrir el puerto configurado cuando AetherSDR inicia. | Sin marcar | Marcado / Sin marcar |
| **FlexControl Tuning Knob: Detect** | Detecta un mando FlexControl conectado. | — | — |
| **FlexControl Tuning Knob: Close** | Libera la conexión con el mando FlexControl. | — | — |
| **Auto-detect on startup** | Detecta automáticamente el mando FlexControl al iniciar. | Sin marcar | Marcado / Sin marcar |
| **Invert tuning direction** | Invierte la dirección de sintonía del FlexControl. | Sin marcar | Marcado / Sin marcar |

## Cambios en la calibración de frecuencia en la versión v0.9.2.1

La sección de calibración de frecuencia de la pestaña **RX** ha sido revisada. Anteriormente, el campo **Cal Frequency (MHz)** y el botón **Start** solo se mostraban cuando no se detectaba un GPSDO. A partir de la versión v0.9.2.1, esos controles son siempre visibles independientemente de si hay un GPSDO instalado.

El mensaje de estado en la parte superior del grupo de calibración cambia según el hardware:

- GPSDO instalado — mostrado en verde: *GPSDO installed. Manual frequency offset calibration available.*
- Sin GPSDO — mostrado en ámbar: *Manual frequency offset calibration available.*

El botón **Start** ahora muestra retroalimentación de estado en línea junto al botón. Mientras una calibración está en curso, el botón se deshabilita y su etiqueta cambia a **Busy**. La etiqueta de estado muestra la etapa actual (por ejemplo, *Starting…*) y se actualiza a medida que avanza la calibración. El botón se vuelve a habilitar cuando la calibración finaliza o falla.

Antes de iniciar la calibración, AetherSDR ahora restablece el error de frecuencia almacenado a cero (`radio set freq_error_ppb=0`) antes de enviar `radio pll_start`. Si el campo **Cal Frequency (MHz)** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no se inicia.

### Controles de calibración actualizados en la pestaña RX

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | Ahora siempre visible, con o sin GPSDO. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Se deshabilita y se etiqueta como **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración antes de continuar. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. | Se restablece a 0 automáticamente al hacer clic en **Start**. |

## Consejos

- Si abre Radio Setup a través de `Settings > Radio Setup...` en lugar de `Settings > FlexControl...`, la pestaña **Serial** aparece en el extremo derecho de la barra de pestañas. Desplácese o amplíe el diálogo si la pestaña no es visible.
- La pestaña **Serial** se construye de forma diferida — no se crea hasta que usted haga clic en ella por primera vez, por lo que hay una breve pausa la primera vez que la selecciona.
- En la pestaña **RX**, si tiene un GPSDO instalado, puede ejecutar una calibración manual de todas formas. Ingrese la frecuencia de referencia en **Cal Frequency (MHz)** y haga clic en **Start**.

## Solución de problemas

- **La pestaña Serial no aparece** — AetherSDR fue compilado sin `HAVE_SERIALPORT`. El elemento de menú `Settings > FlexControl...` también estará ausente. Use una versión que incluya soporte de puerto serie.
- **El puerto no aparece en la lista** — Haga clic en **Refresh** para volver a escanear. En Linux, confirme que su cuenta de usuario tiene permiso de lectura/escritura sobre el nodo de dispositivo (normalmente el grupo `dialout` o `uucp`).
- **El mando FlexControl no es detectado** — Confirme que el puerto correcto está seleccionado y que la velocidad en baudios coincide con la del dispositivo FlexControl. Haga clic en **Detect** nuevamente después de verificar la conexión.
- **El botón Start permanece deshabilitado tras un intento de calibración** — Compruebe que el campo **Cal Frequency (MHz)** contiene una frecuencia válida. Un campo vacío impide que la calibración se inicie y el botón no se volverá a habilitar hasta que cierre y vuelva a abrir el diálogo, o hasta que la calibración anterior finalice.

## Relacionado

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Seleccionar el modo iámbico A o B para el manipulador del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)

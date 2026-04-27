# Configurar las funciones de los pines del puerto serie de FlexControl

Use esta página para asignar una función y polaridad a los pines de salida DTR y RTS del puerto serie conectado a su FlexControl u otro dispositivo serie. Esto permite que AetherSDR controle hardware externo — como líneas de PTT o entradas de manipulador — a través de las señales de control del puerto serie.

## Antes de comenzar

- El radio debe estar conectado. La pestaña **Serial** requiere una conexión de radio activa.
- La pestaña **Serial** solo está presente cuando AetherSDR fue compilado con soporte de puerto serie (`HAVE_SERIALPORT`). Si no ve una pestaña **Serial** ni el elemento de menú `Settings > FlexControl...`, su versión no incluye esta función.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...` — esto lleva directamente a la pestaña **Serial** de Radio Setup. Como alternativa, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para reescanear si su dispositivo no aparece, o escriba la ruta directamente en el campo **Path**.
3. Configure los parámetros de la línea serie usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con los requisitos de su dispositivo.
4. Para el pin **DTR**, seleccione la función deseada en el cuadro combinado de función **DTR**, luego seleccione la polaridad activa en el cuadro combinado **Polarity** adyacente.
5. Para el pin **RTS**, repita las mismas dos selecciones — función y polaridad — usando los cuadros combinados de función **RTS** y **Polarity**.
6. Si las conexiones de su paleta están invertidas, active **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto automáticamente cada vez que inicie, active **Auto-open serial port on startup**.
8. Si está conectando un mando de sintonía FlexControl, haga clic en **Detect** bajo **FlexControl Tuning Knob** para identificar el dispositivo. Haga clic en **Close** para liberarlo.
9. Para que AetherSDR detecte el mando FlexControl automáticamente al iniciar, active **Auto-detect on startup**. Para invertir la dirección de sintonía, active **Invert tuning direction**.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango / valores válidos |
|---|---|---|---|
| **Port** | Selecciona o introduce la ruta del dispositivo serie. | — | Puertos serie del sistema |
| **Refresh** | Reescanea los puertos serie disponibles. | — | — |
| **Path** | Campo editable que muestra la ruta del puerto seleccionado. | — | Cualquier ruta de dispositivo válida |
| **Baud** | Velocidad en baudios del puerto serie. | — | Según las opciones del cuadro combinado |
| **Data** | Número de bits de datos. | — | Según las opciones del cuadro combinado |
| **Parity** | Configuración de paridad. | — | Según las opciones del cuadro combinado |
| **Stop** | Número de bits de parada. | — | Según las opciones del cuadro combinado |
| **DTR: Function** | Asigna una función de señal al pin de salida DTR. | — | Según las opciones del cuadro combinado |
| **DTR: Polarity** | Establece la polaridad activa-alta o activa-baja para DTR. | — | Según las opciones del cuadro combinado |
| **RTS: Function** | Asigna una función de señal al pin de salida RTS. | — | Según las opciones del cuadro combinado |
| **RTS: Polarity** | Establece la polaridad activa-alta o activa-baja para RTS. | — | Según las opciones del cuadro combinado |
| **Paddle Swap (swap dit/dah)** | Invierte las entradas de paleta dit y dah. | Sin marcar | Marcado / Sin marcar |
| **Auto-open serial port on startup** | Reabre el puerto configurado cuando AetherSDR se inicia. | Sin marcar | Marcado / Sin marcar |
| **FlexControl Tuning Knob: Detect** | Detecta un mando FlexControl conectado. | — | — |
| **FlexControl Tuning Knob: Close** | Libera la conexión con el mando FlexControl. | — | — |
| **Auto-detect on startup** | Detecta automáticamente el mando FlexControl al iniciar. | Sin marcar | Marcado / Sin marcar |
| **Invert tuning direction** | Invierte la dirección de sintonía del FlexControl. | Sin marcar | Marcado / Sin marcar |

## Consejos

- Si abre Radio Setup mediante `Settings > Radio Setup...` en lugar de `Settings > FlexControl...`, la pestaña **Serial** aparece en el extremo derecho de la barra de pestañas. Desplace o amplíe el diálogo si la pestaña no es visible.
- La pestaña **Serial** se construye de forma diferida — no se crea hasta que la selecciona por primera vez, por lo que hay una breve pausa la primera vez que la abre.

## Solución de problemas

- **La pestaña Serial no aparece** — AetherSDR fue compilado sin `HAVE_SERIALPORT`. El elemento de menú `Settings > FlexControl...` también estará ausente. Use una versión que incluya soporte de puerto serie.
- **El puerto no aparece en la lista** — Haga clic en **Refresh** para reescanear. En Linux, confirme que su cuenta de usuario tiene permisos de lectura/escritura sobre el nodo del dispositivo (normalmente el grupo `dialout` o `uucp`).
- **El mando FlexControl no es detectado** — Confirme que el puerto correcto está seleccionado y que la velocidad en baudios coincide con la del dispositivo FlexControl. Haga clic en **Detect** nuevamente después de verificar la conexión.

## Relacionado

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Seleccionar el modo iámbico A o B para el manipulador del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)

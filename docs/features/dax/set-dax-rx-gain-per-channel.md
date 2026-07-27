# Establecer la ganancia de RX de DAX por canal

Cada canal de RX de DAX (1–4) tiene un control de ganancia independiente en el applet de audio DAX. Ajustarlos le permite igualar el nivel de audio entregado al software de modo digital u otras aplicaciones que reciben audio de DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El applet de audio DAX debe estar abierto. Si no está visible, haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para mostrarlo.
- DAX debe estar habilitado. Si el botón **Enable** muestra **Disabled**, haga clic en **Enable** en el applet de audio DAX antes de ajustar la ganancia.
- **Usuarios de Windows:** AetherSDR no incluye un controlador DAX integrado en Windows. El applet de audio DAX muestra una nota: "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." DAX funciona en Windows utilizando los controladores SmartSDR DAX de FlexRadio. Todos los controles del applet están inactivos en Windows. Para obtener orientación sobre la configuración, consulte Help → Configuring Data Modes.

## Pasos

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha para abrir el applet de audio DAX.
2. Localice la fila del canal que desea ajustar: **DAX 1:**, **DAX 2:**, **DAX 3:** o **DAX 4:**.
3. Arrastre el medidor/deslizador combinado de ese canal hacia la izquierda o derecha para disminuir o aumentar la ganancia de RX.
4. Suelte el arrastre. El nuevo valor se guarda inmediatamente.

Repita el proceso para cualquier otro canal que necesite ajuste.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| DAX Enable | off (Disabled) | — | `AutoStartDAX` |
| Ganancia+medidor DAX 1 | 0,5 | 0,0–1,0 | `DaxRxGain1` |
| Ganancia+medidor DAX 2 | 0,5 | 0,0–1,0 | `DaxRxGain2` |
| Ganancia+medidor DAX 3 | 0,5 | 0,0–1,0 | `DaxRxGain3` |
| Ganancia+medidor DAX 4 | 0,5 | 0,0–1,0 | `DaxRxGain4` |
| Ganancia+medidor TX | 0,5 | 0,0–1,0 | `DaxTxGain` |

**DAX Enable:** Un botón de alternancia etiquetado **Disabled** o **Enabled** que sirve como interruptor maestro para todos los flujos de RX y TX de DAX. Haga clic para alternar. Cuando está habilitado, el texto del botón cambia a **Enabled**; cuando está deshabilitado, muestra **Disabled**. La configuración se persiste como `AutoStartDAX`.

Cada ganancia+medidor de RX es un medidor de nivel y deslizador de ganancia combinados. La barra de fondo muestra el nivel de señal post-fader suavizado en tiempo real. La línea vertical del control marca la posición de ganancia actual. Arrastrar el control emite la nueva ganancia y la persiste inmediatamente.

Cada deslizador tiene un nombre de accesibilidad establecido como "DAX RX 1 gain", "DAX RX 2 gain", "DAX RX 3 gain" o "DAX RX 4 gain" respectivamente para el soporte de lectores de pantalla.

El indicador de asignación de segmento a la izquierda de cada deslizador (que muestra **—** o **Slice A**–**Slice H**) es de solo lectura y refleja qué segmento está enrutado actualmente a ese canal DAX.

## Consejos

- El relleno del medidor de nivel refleja el nivel de salida post-fader, es decir, el audio entrante multiplicado por la ganancia actual. Mover el deslizador proporciona una retroalimentación visual inmediata sobre la salida efectiva.
- Los valores de ganancia se almacenan como números flotantes con dos decimales (por ejemplo, `0,75`). Se restauran desde `DaxRxGain1`–`DaxRxGain4` cada vez que se inicia AetherSDR.
- Si un canal muestra **—** en el indicador de asignación de segmento, ningún segmento está enrutado a él y el medidor no mostrará actividad independientemente de la configuración de ganancia.
- En Linux, el puente de audio DAX utiliza una ruta de origen de flujo PipeWire nativa, lo que reduce la latencia de RX de aproximadamente 400 ms a aproximadamente 200 ms en comparación con el cliente PulseAudio anterior.

## Solución de problemas

- **El medidor no muestra actividad aunque la ganancia esté configurada por encima de 0,0** — Verifique el indicador de asignación de segmento para esa fila. Si muestra **—**, no hay ningún segmento asignado a ese canal DAX. Asigne un segmento al canal en la configuración de su radio, luego verifique que el botón **Enable** muestre **Enabled**.
- **La ganancia se restablece a 0,5 después de reiniciar** — La configuración no se guardó. Confirme que el arrastre se completó antes de cerrar AetherSDR. El guardado ocurre al soltar el deslizador.
- **El botón DAX Enable no funciona en Windows** — Esto es esperado. AetherSDR no incluye un controlador DAX integrado en Windows. Utilice los controladores SmartSDR DAX de FlexRadio.

## Relacionado

- [Resumen de audio DAX](overview.md)
- [Habilitar DAX para enrutar audio de segmento a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Establecer ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué segmento está usando actualmente cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Iniciar DAX automáticamente al inicio](autostart-dax-on-launch.md)

# Establecer la ganancia de RX de DAX por canal

Cada canal de RX de DAX (1–8) tiene un control de ganancia independiente en el applet DAX Audio. Ajustarlos le permite igualar el nivel de audio entregado al software de modos digitales u otras aplicaciones que reciben audio de DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El applet DAX Audio debe estar abierto. Si no está visible, haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para mostrarlo.
- DAX debe estar habilitado. Si el botón **Enable** muestra **Disabled**, haga clic en **Enable** en el applet DAX Audio antes de ajustar la ganancia.
- **Usuarios de Windows:** AetherSDR no incluye un controlador DAX integrado en Windows. El applet DAX Audio muestra una nota: "No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX." DAX funciona en Windows utilizando los controladores SmartSDR DAX propios de FlexRadio. Todos los controles del applet están inactivos en Windows. Para obtener orientación sobre la configuración, consulte Help → Configuring Data Modes.

## Pasos

1. Haga clic en el botón de la bandeja **DAX** en la barra lateral derecha para abrir el applet DAX Audio.
2. Localice la fila del canal que desea ajustar: **DAX 1:** hasta **DAX 8:**. Las filas visibles dependen de la capacidad de slices de la radio conectada; una radio con menos slices no muestra controles deslizantes de ganancia vacíos para canales más allá de su capacidad.
3. Arrastre el control combinado de medidor/deslizador de ese canal hacia la izquierda o la derecha para disminuir o aumentar la ganancia de RX.
4. Suelte el arrastre. El nuevo valor se guarda inmediatamente.

Repita el proceso para cualquier otro canal que necesite ajuste.

## Qué hace cada control

| Control               | Valor predeterminado                                                                                                      | Rango válido                                                                                                                             |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| DAX Enable            | Inicia el puente de audio DAX; emite daxToggled.                                                                           | La etiqueta del botón es 'Enable'/'Disabled'; interruptor maestro para todas las corrientes de RX y TX de DAX. No está integrado en Windows (#4112). |
| DAX 1 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 2 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 3 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 4 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 5 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 6 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 7 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| DAX 8 gain+meter      | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| TX gain+meter         | 0.5                                                                                                                       | 0.0–1.0                                                                                                                                  |
| Windows note          | En las compilaciones de Windows, el applet muestra solo la nota 'No built-in DAX driver on Windows. Use TCI, or SmartSDR DAX.' (#4112). | Windows no tiene un puente DAX integrado (sin controlador de audio en modo kernel); todos los demás controles se omiten y sus definidores están protegidos contra valores nulos. |

**DAX Enable:** Un botón de alternancia etiquetado como **Disabled** o **Enabled** que sirve como interruptor maestro para todas las corrientes de RX y TX de DAX. Haga clic para alternar. Cuando está habilitado, el texto del botón cambia a **Enabled**; cuando está deshabilitado, muestra **Disabled**. La configuración se guarda como `AutoStartDAX`.

Cada medidor de ganancia de RX es un medidor de nivel y un control deslizante de ganancia combinados. La barra de fondo muestra el nivel de señal posterior al atenuador suavizado en tiempo real. La línea vertical del pulgar marca la posición de ganancia actual. Arrastrar el pulgar emite el nuevo valor de ganancia y lo guarda inmediatamente. Los niveles del medidor de RX utilizan suavizado exponencial con un ataque rápido y una caída lenta, de modo que los picos de nivel aparecen rápidamente y disminuyen de forma más gradual.

Cada control deslizante tiene un nombre de accesibilidad establecido como "DAX RX 1 gain", "DAX RX 2 gain", "DAX RX 3 gain" hasta "DAX RX 8 gain", respectivamente, para soporte de lectores de pantalla.

El indicador de asignación de slice a la izquierda de cada control deslizante (que muestra **—** o **Slice A**–**Slice H**) es de solo lectura y refleja qué slice está enrutado actualmente a ese canal de DAX.

## Consejos

- El relleno del medidor de nivel refleja el nivel de salida posterior al atenuador, es decir, el audio entrante multiplicado por la ganancia actual. Mover el control deslizante proporciona retroalimentación visual inmediata sobre la salida efectiva.
- Los valores de ganancia se almacenan como números de punto flotante con dos decimales (por ejemplo, `0.75`). Se restauran desde `DaxRxGain1`–`DaxRxGain8` cada vez que se inicia AetherSDR.
- Si un canal muestra **—** en el indicador de asignación de slice, ningún slice está enrutado a él y el medidor no mostrará actividad independientemente de la configuración de ganancia.
- Las filas de los canales de DAX más allá de la capacidad de slices de la radio conectada se ocultan por completo. Por ejemplo, una radio con 4 slices muestra solo los canales de DAX 1–4. La ganancia de TX permanece disponible en todas las radios.
- En Linux, el puente de audio DAX utiliza una ruta nativa de fuente de flujo PipeWire, lo que reduce la latencia de RX de aproximadamente 400 ms a aproximadamente 200 ms en comparación con el cliente PulseAudio anterior.

## Solución de problemas

- **El medidor no muestra actividad aunque la ganancia esté establecida por encima de 0.0** — Verifique el indicador de asignación de slice en esa fila. Si muestra **—**, ningún slice está asignado a ese canal de DAX. Asigne un slice al canal en la configuración de su radio y luego verifique que el botón **Enable** muestre **Enabled**.
- **La ganancia se restablece a 0.5 después del reinicio** — La configuración no se guardó. Confirme que el arrastre se completó antes de cerrar AetherSDR. El guardado ocurre al soltar el control deslizante.
- **El botón DAX Enable no hace nada en Windows** — Esto es lo esperado. AetherSDR no incluye un controlador DAX integrado en Windows. Utilice en su lugar los controladores SmartSDR DAX de FlexRadio.
- **Faltan algunas filas de canales de DAX** — Esto es normal cuando la radio conectada tiene menos slices que el máximo. Por ejemplo, una radio con 4 slices muestra solo los canales de DAX 1–4. Las filas ocultas no tienen efecto en los canales restantes.

## Relacionado

- [Información general de DAX Audio](overview.md)
- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Establecer ganancia de TX de DAX](set-dax-tx-gain.md)
- [Ver qué slice está usando actualmente cada canal de DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Iniciar DAX automáticamente al arrancar](autostart-dax-on-launch.md)

# Trabajar con un repetidor de FM usando tono CTCSS y desplazamiento +/- 

Configure un slice para operación FM en dúplex con desplazamiento de repetidor y un tono de acceso CTCSS para poder escuchar la salida del repetidor y activarlo correctamente al transmitir.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600.
- El applet Controles RX está visible en la barra lateral derecha. Si no lo está, haga clic en el botón de la bandeja RX en la barra lateral derecha.
- Conoce la frecuencia de salida del repetidor, la dirección del desplazamiento, la magnitud del desplazamiento y la frecuencia del tono CTCSS.

## Pasos

1. En el applet Controles RX, haga clic en el combo Modo y seleccione **FM** (o **NFM** para FM estrecha).
2. Haga clic en la etiqueta Frecuencia para abrir el campo de edición de Frecuencia. Escriba la frecuencia de **salida** (recepción) del repetidor en MHz y pulse Enter.
3. En el cuadro de giro **Desplazamiento (FM)**, ajuste la magnitud del desplazamiento en MHz. Use las flechas del cuadro de giro o escriba un valor directamente. El rango válido es 0.0–100.0 MHz en pasos de 0.1 MHz. El valor predeterminado es 0.0 MHz.
4. Ajuste la dirección del desplazamiento haciendo clic en uno de los tres botones de alternancia:
   - **−** — La frecuencia TX está por debajo de la frecuencia RX.
   - **Símplex** — La frecuencia TX es igual a la frecuencia RX (predeterminado).
   - **+** — La frecuencia TX está por encima de la frecuencia RX.
5. Haga clic en el combo **Modo de tono (FM)** (predeterminado: **Apagado**) y seleccione **CTCSS TX**.
6. Haga clic en el combo **Valor del tono CTCSS** y seleccione la frecuencia de tono requerida por el repetidor. Los tonos disponibles siguen el estándar de 41 tonos EIA/TIA-603, desde 67.0 Hz hasta 254.1 Hz.
7. Confirme que el squelch esté ajustado apropiadamente para la banda. Consulte [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md) si es necesario.

## Qué hace cada control

| Control                | Predeterminado | Rango válido / opciones                     |
|------------------------|----------------|---------------------------------------------|
| Combo Modo             | USB            | FM, NFM, DFM (entre otros)                  |
| Modo de tono (FM)      | Apagado        | Apagado, CTCSS TX                           |
| Valor del tono CTCSS   | —              | 67.0 Hz – 254.1 Hz (41 tonos EIA/TIA-603)  |
| Desplazamiento (FM)    | 0.0 MHz        | 0.0 – 100.0 MHz, paso 0.1                  |
| − (desplazamiento abajo) | —            | alternancia                                 |
| Símplex                | marcado        | alternancia                                 |
| + (desplazamiento arriba) | —           | alternancia                                 |
| REV                    | —              | alternancia                                 |

## Consejos

- Si necesita escuchar en la frecuencia de entrada del repetidor para verificar si el canal está ocupado antes de transmitir, haga clic en **REV** para intercambiar temporalmente la dirección del desplazamiento.
- Los modos de la familia FM ocultan los botones de preselección de ancho de filtro. Esto es esperado; el ancho de filtro para FM está fijado por el modo en sí.
- Los botones de la pestaña del slice y la insignia del slice tienen código de colores por slice usando SliceColorManager (v0.9.3+). Los colores persisten entre sesiones y se reflejan en las pestañas del slice, la insignia del slice, los widgets VFO y las barras de medidores.
- Cuando la radio informa un número diferente de slices disponibles del que se creó para la fila de pestañas, AetherSDR ahora elimina los botones de pestaña del slice existentes y los reconstruye para la nueva cantidad antes de reconectar los manejadores de clic (v0.9.5.1, #2254). Esto evita que aparezcan botones obsoletos después de una reconexión o un cambio en la configuración del hardware.
- Los valores preestablecidos de ancho de filtro se almacenan en el formato `lo:hi` (bordes de la banda de paso en Hz) o como un valor de ancho simple, dependiendo de si el valor preestablecido se guardó con posiciones de borde explícitas. Ambos formatos se leen correctamente cuando vuelve a abrir el applet o cambia de modo (#2259).
- El indicador de ancho de filtro se comparte con el panel VFO a través de `RxApplet::formatFilterWidth()`. En v0.9.8+, este método ahora es una función estática pública para que ambos widgets produzcan un formato idéntico y consciente del modo para modos SSB, digital y AM (#2197).
- Los atajos de ampliar/reducir (por ejemplo, Ctrl+Shift+W, Ctrl+Shift+N) llaman a `stepFilterWidth(int direction)`, que recorre la lista de preselecciones de filtro por modo para encontrar el siguiente ancho válido y lo aplica con la geometría de borde correcta para el modo actual (#2208).
- La insignia del slice ahora admite formato de texto enriquecido (HTML) para la visualización de la letra del slice (#2606).
- La selección de antena tanto para RX como para TX ahora prioriza la propia lista de antenas del slice cuando está disponible. El menú muestra las etiquetas de las antenas con información sobre herramientas y sugerencias de estado, con los datos reales de la antena almacenados por separado del texto mostrado. Los menús de antena TX filtran los puertos con el prefijo "RX" e incluyen solo antenas que coinciden con patrones como "ANT", "TX" o "XVTR".
- De forma predeterminada, AetherSDR utiliza un algoritmo de squelch Automático que sobrescribe el squelchLevel del slice con valores sugeridos por el algoritmo. El último umbral de squelch Manual elegido por el usuario ahora se guarda en el lado del cliente en la configuración `LastManualSquelchLevel` y se restaura entre sesiones y ciclos de modo.

## Solución de problemas

- **El repetidor no responde a sus transmisiones** — Confirme que el valor del tono CTCSS coincida con el que espera el repetidor y que el Modo de tono esté configurado en **CTCSS TX** en lugar de **Apagado**.
- **La frecuencia TX parece incorrecta** — Verifique que el botón de dirección del desplazamiento (**−**, **Símplex** o **+**) coincida con la dirección de desplazamiento publicada del repetidor y que el valor de Desplazamiento (FM) esté configurado con la magnitud correcta (por ejemplo, 0.6 MHz para un repetidor típico de 2 m).
- **Los controles Modo de tono y CTCSS no son visibles** — El modo del slice debe ser **FM**, **NFM** o **DFM**. Estos controles están ocultos en todos los demás modos.
- **Los controles de squelch están atenuados** — El squelch se desactiva automáticamente cuando el modo del slice es **DIGU**, **DIGL**, **NT**, **RTTY**, **CW** o **CWL**. Cambie a un modo FM o SSB para habilitar los controles de squelch.
- **Los botones de la pestaña del slice aparecen incorrectos después de reconectar** — Si la fila de pestañas del slice muestra la cantidad incorrecta de botones o un diseño obsoleto después de que la radio se reconecte, desconéctese y reconéctese manualmente. En v0.9.5.1 esto se corrige automáticamente: el applet llama a `clearSliceButtons()` para eliminar los botones antiguos y restaurar la insignia estática del slice antes de reconstruir la fila de pestañas para la nueva cantidad de slices (#2254).
- **El botón de preselección de filtro no cambia la banda de paso** — Si el ancho actual no es un valor preestablecido estándar, el paso de ampliar/reducir puede no cambiar la banda de paso. Este comportamiento es esperado; haga clic en un botón de preselección de filtro específico o escriba una frecuencia para cambiar la banda de paso, luego los atajos de ampliar/reducir funcionarán desde el nuevo ancho.

## Notas sobre el modo NT y el modo RTTY

Los modos **NT** y **RTTY** se tratan como modos digitales en el applet Controles RX (v0.9.3+ para NT, v26.5.1 para RTTY). Esto tiene los siguientes efectos:

- NT y RTTY usan los mismos valores preestablecidos de ancho de filtro y tamaños de paso que DIGU y DIGL.
- El indicador de ancho de filtro calcula el ancho de banda de la misma manera que USB (usando el borde superior de la banda de paso).
- El squelch está desactivado mientras NT o RTTY están activos. Si el squelch estaba encendido cuando cambió a NT o RTTY, se apaga automáticamente y se restaura cuando sale del modo.
- Para el modo RTTY específicamente, el squelch está desactivado porque eliminaría los caracteres FSK e interrumpiría la decodificación (#2504).

## Relacionados

- [Cambiar modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Sintonizar la radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Activar el squelch y ajustar su umbral](turn-on-the-squelch-and-set-its-threshold.md)
- [Seleccionar la antena RX o TX para este slice](select-the-rx-or-tx-antenna-for-this-slice.md)

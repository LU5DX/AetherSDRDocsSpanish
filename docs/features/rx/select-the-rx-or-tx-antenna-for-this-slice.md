# Applet de controles RX

El applet de controles RX proporciona controles de recepción por slice: modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia de AF/pan, squelch, RIT/XIT, configuración de dúplex para repetidoras FM y el demodulador de software WFM. Un clic en el botón de silencio silencia este slice; un doble clic silencia/activa el sonido de todos los slices propios.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se completa a partir de la configuración de puertos del propio radio. Confirme que sus antenas estén conectadas y reconocidas por el radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet de controles RX. Si no está visible, haga clic en el botón de bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A a H) que desea cambiar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, p. ej. **ANT1**). Aparece un menú que lista todos los puertos de antena disponibles y cualquier perfil de antena virtual KiwiSDR. Haga clic en el puerto o perfil que desee. Una marca de verificación muestra la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, p. ej. **ANT1**). Aparece un menú que lista los puertos de antena con capacidad TX. Haga clic en el puerto que desee.
5. **Para habilitar WFM:** Haga clic en el botón **WFM**. Esto activa un demodulador FM por software mediante DAX IQ → Hi-Fi Cable. El botón se ilumina en verde cuando está activo. Cambiar el combo de modo (USB, LSB, etc.) apaga WFM automáticamente.
6. **Para calibrar AGC-T:** Haga clic derecho en el deslizador de umbral de AGC y seleccione **Calibrate AGC-T against noise floor…** en el menú contextual. Esto abre el panel de calibración de AGC-T para el slice actual.

## Qué hace cada control

| Control                           | Valor predeterminado | Valores válidos                                                              |
|-----------------------------------|---------------------|------------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1             | Puertos de antena de ant_list del radio, rxAntennaList del propio slice, o tokens de antena virtual KiwiSDR |
| **ANT1** (antena TX, etiqueta roja) | ANT1            | Puertos con capacidad TX de ant_list del radio                               |
| **Pestañas de slice (A..H)**      | Ninguno              | 1–8 botones (limitados por el máximo de slices del hardware)                 |
| **Insignia de slice**             | A                    | A/B/C/D/E/F/G/H (representado como texto enriquecido HTML)                   |
| **🔓 / 🔒**                         | 🔓                   | Desbloqueado / bloqueado                                                     |
| **WFM**                           | Apagado              | Botón de alternancia; verde cuando está activo                               |
| **Combo de modo**                 | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY, WFM (+ RADE si se compiló con HAVE_RADE) |
| **Etiqueta de frecuencia**        | 0.000.000            | 0.001–54.000 MHz (hasta 50000 MHz en XVTR)                                   |
| **Campo de edición de frecuencia**| Ninguno              | 0.001–54.000 MHz (hasta 50000 MHz en XVTR); acepta autoescalado de kHz/Hz    |
| **STEP**                          | 100 Hz               | Lista de tamaños de paso por modo                                            |
| **Valores preestablecidos de ancho de filtro** | Ninguno        | Anchuras preestablecidas por modo                                            |
| **Widget de banda de paso del filtro** | Ninguno           | Arrastre los bordes lo/hi para ajustar la banda de paso                      |
| **Modo de tono (FM)**             | Apagado              | Apagado, CTCSS TX                                                            |
| **Valor de tono CTCSS**           | Ninguno              | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz)                                |
| **Offset (FM)**                   | 0.0 MHz              | 0.0–100.0 MHz (paso 0.1)                                                     |
| **− (offset hacia abajo)**        | Ninguno              | Alternancia                                                                  |
| **Simplex**                       | Marcado              | Alternancia                                                                  |
| **+ (offset hacia arriba)**       | Ninguno              | Alternancia                                                                  |
| **REV / XFC**                     | Ninguno              | REV (alternancia) o XFC (momentáneo)                                         |
| **🔊 / 🔇 (silencio)**              | 🔊                   | Con sonido / silenciado                                                      |
| **Ganancia de AF**                | 70                   | 0–100                                                                        |
| **Pan L / R**                     | 50                   | 0–100                                                                        |
| **SQL / AUTO**                    | Apagado              | Apagado, SQL (Manual), AUTO                                                  |
| **Nivel de squelch**              | 20                   | Manual: 0–100 (o 0–99 en recepción de reemplazo Kiwi); Auto: margen de 5–20 dB |
| **Modo de AGC**                   | Med                  | Apagado, Lento, Med, Rápido                                                  |
| **Umbral de AGC**                 | 65                   | 0–100                                                                        |
| **RIT**                           | Ninguno              | Alternancia                                                                  |
| **RIT 0**                         | Ninguno              | Botón pulsador                                                               |
| **Offset de RIT**                 | +0 Hz                | Paso de 10 Hz                                                                |
| **XIT**                           | Ninguno              | Alternancia                                                                  |
| **XIT 0**                         | Ninguno              | Botón pulsador                                                               |
| **Offset de XIT**                 | +0 Hz                | Paso de 10 Hz                                                                |
| **TX (insignia)**                 | Ninguno              | Haga clic para establecer como slice de TX                                   |
| **QSK**                           | Ninguno              | Ámbar cuando el break-in de CW está activo (solo lectura)                    |
| **Ancho de filtro (indicador)**   | 2.7K                 | Ancho de banda de filtro actual                                              |

## Qué muestra cada indicador

| Indicador        | Estados                                       | Significado                                   |
|------------------|-----------------------------------------------|-----------------------------------------------|
| Ancho de filtro  | p. ej. '2.7K', '3.3K', '500', '6.0K'          | Ancho de banda de filtro del slice actual     |
| QSK              | apagado (gris), encendido (ámbar)             | Estado de break-in total de CW reflejado desde el applet de CW |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen lado a lado en la fila de encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Aún aparecerán en el menú de antena RX. El menú de antena TX también incluye puertos cuyos nombres comienzan con `ANT`, `TX` o `XVTR`.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- Desde v0.9.3, los botones de pestaña de slice y la insignia de slice usan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets de VFO y las tiras de medidor. Los colores no son configurables desde la página de controles de antena; se aplican en todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato sensible al modo con el panel de VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas coherentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preestablecidos de filtro por modo para que los atajos de teclado de ensanchar/estrechar produzcan geometría de bordes correcta según el modo (#2208). Por ejemplo, ensanchar desde un filtro USB de 2.7 kHz selecciona el siguiente preestablecido más grande (p. ej. 2.9 kHz) con la colocación de bordes adecuada para modo USB en lugar de una banda de paso simétrica.
- Desde v26.5.2.1, la insignia de slice admite representación de texto enriquecido HTML (#2606). Esto permite que la letra del slice se estilice con formato HTML si es necesario.
- Desde v26.6.1, los botones de preestablecidos de filtro (1.8K, 2.1K, etc.) usan estilo consciente del tema mediante `kButtonBase()`, que resuelve tokens a través del ThemeManager. Estos botones ahora se re-tematizan junto con el resto de la interfaz cuando cambia el tema de la aplicación. Los tokens de tema utilizados son `{{color.background.1}}`, `{{color.background.2}}` y `{{color.text.primary}}`.
- Desde v26.6.3, el campo de edición de frecuencia usa `FreqLineEdit` (una subclase de `QLineEdit`) para mejorar el manejo de entrada. Muestra "MHz" como texto de sugerencia en lugar de texto de marcador de posición.
- Desde v26.6.3, el cuadro de giro **STEP** emite `stepSizeChangedByUser` además de `stepSizeChanged` cuando el usuario cambia manualmente el tamaño de paso. Esto permite que otros componentes distingan cambios de paso programáticos de los iniciados por el usuario.
- Desde v26.6.3, el deslizador de umbral de AGC tiene un menú contextual de clic derecho con la opción **Calibrate AGC-T against noise floor…**. La información sobre herramientas ahora incluye la pista "Right-click to calibrate against the noise floor" para su descubrimiento.
- Desde v26.7.4, la lista de preestablecidos de filtro CW se ha ampliado de 4 a 6 preestablecidos: 50, 100, 250, 400, 500 y 600 Hz.
- Desde v26.8.4, el squelch es autoritativo del radio según la Política de Ajustes Autoritativos del Radio (#4592). El nivel de squelch manual NO se persiste en el cliente; el radio es la fuente de verdad para el estado del squelch. El valor del lado del cliente es solo un respaldo cuando no hay ningún slice adjunto.
- Desde v26.8.4, la lista de tonos CTCSS ahora incluye tonos EIA/TIA-603 adicionales a 69.3, 159.8, 165.5, 171.3, 177.3, 183.5, 189.9, 196.6 y 199.5 Hz. Estos tonos se muestran sin un código de designación estándar (solo se muestra la frecuencia en el cuadro combinado).
- Desde v26.8.4, la detección de modo CW usa un único helper compartido (`isCwMode()`) que reconoce todas las variantes de modo CW, lo que garantiza que los preestablecidos de filtro y los tamaños de paso se apliquen correctamente independientemente del modo CW específico seleccionado.

## Cambios en el menú de antena en v26.5.2.1

Los menús de antena RX y TX se han actualizado para proporcionar una retroalimentación más clara:

- Cada elemento del menú muestra el nombre del puerto de antena tanto como información sobre herramientas como sugerencia de estado.
- Los datos de la acción del menú llevan el identificador de antena sin procesar, en lugar de usar el texto mostrado. Esto significa que los elementos del menú pueden mostrar etiquetas formateadas (p. ej. con indicadores de tipo de puerto) mientras siguen seleccionando el puerto de antena correcto.
- El menú de antena RX ahora prefiere la `rxAntennaList()` del propio slice si no está vacía, recurriendo a la `ant_list` del radio. Esto garantiza que el menú refleje cualquier restricción de antena por slice reportada por el radio.

## Integración de antena virtual KiwiSDR (v26.7.4)

Cuando un gestor KiwiSDR está activo, el menú de antena RX incluye tokens de perfil de antena virtual del gestor KiwiSDR. Estos perfiles aparecen como entradas adicionales en el menú de antena RX.

- Los perfiles de antena virtual se identifican por un ID de perfil en lugar de un nombre de puerto físico.
- Cuando selecciona una antena virtual KiwiSDR desde el menú, AetherSDR emite `kiwiRxAntennaSelected(sliceId, profileId)` y no llama a `slice->setRxAntenna()`.
- Cuando selecciona un puerto de antena Flex físico, AetherSDR emite `flexRxAntennaSelected(sliceId)` y llama a `slice->setRxAntenna()` con el puerto seleccionado.
- Cada perfil KiwiSDR se asigna a como máximo un slice a la vez. El menú muestra una marca de verificación junto al perfil asignado al slice actual.
- El menú se reconstruye cada vez que se abre, lo que garantiza que los perfiles disponibles estén actualizados.

## Demodulador de software WFM (v26.6.3)

El botón **WFM** proporciona un demodulador FM por software que utiliza audio DAX IQ enrutado a través del dispositivo de audio virtual Hi-Fi Cable de su sistema.

- **Para habilitar WFM:** Haga clic en el botón **WFM**. Se ilumina en verde cuando está activo. El botón se encuentra a la derecha del combo de modo en la fila de frecuencia.
- **Para deshabilitar WFM:** Haga clic en el botón **WFM** nuevamente, o seleccione cualquier modo de radio real desde el combo de modo (USB, LSB, CW, etc.). Cambiar de modo desactiva automáticamente WFM para ese slice.
- **Comportamiento por slice:** Cada slice tiene su propio estado de WFM. Habilitar WFM en un slice no afecta a otros slices.
- **Gestión de estado:** AetherSDR emite `wfmActivated(true, sliceId)` cuando WFM se enciende, y `wfmActivated(false, sliceId)` cuando WFM se apaga (ya sea al hacer clic en el botón o al cambiar el combo de modo). El método `setWfmActive()` permite que otros componentes sincronicen el estado del botón WFM programáticamente.
- **Interacción con el combo de modo:** Cuando selecciona un modo de radio real desde el combo de modo mientras WFM está activo en ese slice, AetherSDR emite automáticamente `wfmActivated(false, sliceId)` para desmontar la superposición de WFM. Seleccionar "WFM" desde el combo de modo no está soportado; WFM se controla exclusivamente mediante el botón dedicado.

## Cambios en el modo RADE

La lógica de activación del modo RADE se ha actualizado para reflejar el hecho de que "RADE" es un modo solo del cliente:

- Cuando selecciona RADE desde el combo de modo, el cliente establece el modo del slice en "RADE" y emite `radeActivated(true, sliceId)`. El radio mismo devuelve inmediatamente el modo subyacente real (típicamente DIGL o DIGU).
- AetherSDR ya no establece el modo del slice en el radio cuando se selecciona RADE. La retroalimentación de modo del radio

# Applet de controles de RX

El applet de controles de RX proporciona controles de recepción por slice: modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia/panorama de AF, squelch, RIT/XIT, configuración de dúplex para repetidores de FM y el demodulador WFM por software. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/activa el sonido de todos los slices propios.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos de la radio. Confirme que sus antenas estén conectadas y reconocidas por la radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet de controles de RX. Si no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A a H) para el slice que desea modificar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, p. ej., **ANT1**). Aparece un menú que lista todos los puertos de antena disponibles y cualquier perfil de antena virtual de KiwiSDR. Haga clic en el puerto o perfil que desee. Una marca de verificación muestra la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, p. ej., **ANT1**). Aparece un menú que lista los puertos de antena con capacidad TX. Haga clic en el puerto que desee.
5. **Para habilitar WFM:** Haga clic en el botón **WFM**. Esto activa un demodulador FM por software a través de DAX IQ → Hi-Fi Cable. El botón se ilumina en verde cuando está activo. Cambiar el combo de modo (USB, LSB, etc.) desactiva automáticamente WFM.
6. **Para calibrar AGC-T:** Haga clic derecho en el deslizador de umbral AGC y seleccione **Calibrar AGC-T contra el piso de ruido…** en el menú contextual. Esto abre el panel de calibración de AGC-T para el slice actual.

## Qué hace cada control

| Control                           | Por defecto | Valores válidos                                                              |
|-----------------------------------|-------------|------------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul)| ANT1        | Puertos de antena de ant_list de la radio, rxAntennaList del slice o tokens de antena virtual KiwiSDR |
| **ANT1** (antena TX, etiqueta roja)| ANT1        | Puertos con capacidad TX de ant_list de la radio                             |
| **Pestañas de slice (A..H)**      | Ninguno     | 1–8 botones (limitado por el máximo de slices del hardware)                  |
| **Insignia de slice**             | A           | A/B/C/D/E/F/G/H (renderizado como texto enriquecido HTML)                   |
| **🔓 / 🔒**                         | 🔓           | Desbloqueado / Bloqueado                                                     |
| **WFM**                           | Apagado     | Botón de alternancia; verde cuando está activo                               |
| **Combo de modo**                 | USB         | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY, WFM (+ RADE si HAVE_RADE) |
| **Etiqueta de frecuencia**        | 0.000.000   | 0.001–54.000 MHz (450.000 MHz en XVTR)                                      |
| **Edición de frecuencia**         | Ninguno     | 0.001–54.000 MHz (450.000 MHz en XVTR); acepta escalado automático kHz/Hz    |
| **STEP**                          | 100 Hz      | Lista de tamaños de paso por modo                                            |
| **Preajustes de ancho de filtro** | Ninguno     | Anchuras preajustadas por modo                                               |
| **Widget de banda de paso de filtro**| Ninguno  | Arrastre los bordes lo/hi para ajustar la banda de paso                      |
| **Modo de tono (FM)**             | Apagado     | Apagado, CTCSS TX                                                            |
| **Valor de tono CTCSS**           | Ninguno     | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz)                               |
| **Offset (FM)**                   | 0.0 MHz     | 0.0–100.0 MHz (paso 0.1)                                                    |
| **− (desplazamiento hacia abajo)**| Ninguno     | Alternancia                                                                  |
| **Simplex**                       | Marcado     | Alternancia                                                                  |
| **+ (desplazamiento hacia arriba)**| Ninguno    | Alternancia                                                                  |
| **REV**                           | Ninguno     | Alternancia                                                                  |
| **🔊 / 🔇 (silencio)**              | 🔊           | Sin silencio / Silenciado                                                    |
| **Ganancia AF**                   | 70          | 0–100                                                                        |
| **Panorama L / R**                | 50          | 0–100                                                                        |
| **SQL**                           | Ninguno     | Alternancia                                                                  |
| **Nivel de squelch**              | 20          | 0–100 (persistido en el cliente como `LastManualSquelchLevel`)               |
| **Modo AGC**                      | Med         | Apagado, Lento, Medio, Rápido                                                |
| **Umbral AGC**                    | 65          | 0–100                                                                        |
| **RIT**                           | Ninguno     | Alternancia                                                                  |
| **RIT 0**                         | Ninguno     | Botón pulsador                                                               |
| **Offset RIT**                    | +0 Hz       | Paso 10 Hz                                                                   |
| **XIT**                           | Ninguno     | Alternancia                                                                  |
| **XIT 0**                         | Ninguno     | Botón pulsador                                                               |
| **Offset XIT**                    | +0 Hz       | Paso 10 Hz                                                                   |
| **TX (insignia)**                 | Ninguno     | Haga clic para establecer como slice TX                                      |
| **QSK**                           | Ninguno     | Ámbar cuando el break-in de CW está activo (solo lectura)                    |
| **Ancho de filtro (indicador)**   | 2.7K        | Ancho de banda actual del filtro del slice                                   |

## Qué muestra cada indicador

| Indicador        | Estados                                     | Significado                                    |
|------------------|---------------------------------------------|------------------------------------------------|
| Ancho de filtro  | p. ej., '2.7K', '3.3K', '500', '6.0K'       | Ancho de banda actual del filtro del slice       |
| QSK              | apagado (gris), encendido (ámbar)            | Estado de break-in completo de CW reflejado desde el applet CW |

## Consejos

- La etiqueta de la antena RX se muestra en azul; la etiqueta de la antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX. El menú de antena TX también incluye puertos cuyos nombres comienzan con `ANT`, `TX` o `XVTR`.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- Desde la v0.9.3, los botones de pestaña de slice y la insignia de slice usan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidores. Los colores no son configurables desde la página de controles de antena; se aplican a todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato sensible al modo con el panel VFO (`RxApplet::formatFilterWidth`), asegurando lecturas consistentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo, de modo que los atajos de teclado de ampliar/reducir produzcan una geometría de bordes correcta según el modo (#2208). Por ejemplo, ampliar desde un filtro USB de 2.7 kHz selecciona el siguiente preajuste más grande (p. ej., 2.9 kHz) con la ubicación de bordes adecuada para el modo USB, en lugar de una banda de paso simétrica.
- Desde la v26.5.2.1, la insignia de slice admite renderizado de texto enriquecido HTML (#2606). Esto permite que la letra del slice se estilice con formato HTML si es necesario.
- El nivel manual de squelch se persiste en el cliente como la configuración `LastManualSquelchLevel`. Esto preserva su preferencia manual de squelch a través de ciclos de modo, reconexiones de radio y reinicios de la aplicación. El algoritmo automático de squelch de la radio puede modificar el nivel de squelch del slice, pero AetherSDR restaura el último nivel manual elegido por el usuario cuando el modo Auto no está activo.
- Desde la v26.6.1, los botones de preajuste de filtro (1.8K, 2.1K, etc.) utilizan estilo sensible al tema a través de `kButtonBase()`, que resuelve tokens mediante el ThemeManager. Estos botones ahora se re-tematizan junto con el resto de la interfaz cuando cambia el tema de la aplicación. Los tokens de tema utilizados son `{{color.background.1}}`, `{{color.background.2}}` y `{{color.text.primary}}`.
- Desde la v26.6.3, el campo de edición de frecuencia usa `FreqLineEdit` (una subclase de `QLineEdit`) para una mejor gestión de la entrada. Muestra "MHz" como texto de sugerencia en lugar de texto de marcador de posición.
- Desde la v26.6.3, el cuadro de giro **STEP** emite `stepSizeChangedByUser` además de `stepSizeChanged` cuando el usuario cambia manualmente el tamaño de paso. Esto permite que otros componentes distingan los cambios de paso programáticos de los iniciados por el usuario.
- Desde la v26.6.3, el deslizador de umbral AGC tiene un menú contextual con clic derecho con una opción **Calibrar AGC-T contra el piso de ruido…**. La información sobre herramientas ahora incluye la sugerencia "Haga clic derecho para calibrar contra el piso de ruido" para facilitar su descubrimiento.
- Desde la v26.7.4, la lista de preajustes de filtro CW se ha ampliado de 4 a 6 preajustes: 50, 100, 250, 400, 500 y 600 Hz.

## Cambios en el menú de antena en v26.5.2.1

Los menús de antena RX y TX se han actualizado para proporcionar una retroalimentación más clara:

- Cada elemento del menú muestra el nombre del puerto de antena como información sobre herramientas y sugerencia de estado.
- Los datos de la acción del menú llevan el identificador de antena sin procesar, en lugar de usar el texto mostrado. Esto significa que los elementos del menú pueden mostrar etiquetas con formato (p. ej., con indicadores de tipo de puerto) mientras siguen seleccionando el puerto de antena correcto.
- El menú de antena RX ahora prefiere la `rxAntennaList()` del slice si no está vacía, recurriendo a la `ant_list` de la radio. Esto asegura que el menú refleje cualquier restricción de antena por slice informada por la radio.

## Integración de antena virtual KiwiSDR (v26.7.4)

Cuando un gestor de KiwiSDR está activo, el menú de antena RX incluye tokens de perfil de antena virtual del gestor de KiwiSDR. Estos perfiles aparecen como entradas adicionales en el menú de antena RX.

- Los perfiles de antena virtual se identifican por un ID de perfil en lugar de un nombre de puerto físico.
- Cuando selecciona una antena virtual KiwiSDR del menú, AetherSDR emite `kiwiRxAntennaSelected(sliceId, profileId)` y no llama a `slice->setRxAntenna()`.
- Cuando selecciona un puerto de antena Flex físico, AetherSDR emite `flexRxAntennaSelected(sliceId)` y llama a `slice->setRxAntenna()` con el puerto seleccionado.
- Cada perfil de KiwiSDR se asigna a como máximo un slice a la vez. El menú muestra una marca de verificación junto al perfil asignado al slice actual.
- El menú se reconstruye cada vez que se abre, asegurando que los perfiles disponibles estén actualizados.

## Demodulador WFM por software (v26.6.3)

El botón **WFM** proporciona un demodulador FM por software que utiliza audio DAX IQ enrutado a través del dispositivo de audio virtual Hi-Fi Cable de su sistema.

- **Para habilitar WFM:** Haga clic en el botón **WFM**. Se ilumina en verde cuando está activo. El botón se encuentra a la derecha del combo de modo en la fila de frecuencia.
- **Para deshabilitar WFM:** Vuelva a hacer clic en el botón **WFM**, o seleccione cualquier modo de radio real del combo de modo (USB, LSB, CW, etc.). Cambiar de modo desactiva automáticamente WFM para ese slice.
- **Comportamiento por slice:** Cada slice tiene su propio estado WFM. Habilitar WFM en un slice no afecta a otros slices.
- **Gestión de estado:** AetherSDR emite `wfmActivated(true, sliceId)` cuando WFM se activa, y `wfmActivated(false, sliceId)` cuando WFM se desactiva (ya sea haciendo clic en el botón o cambiando el combo de modo). El método `setWfmActive()` permite que otros componentes sincronicen el estado del botón WFM mediante programación.
- **Interacción con el combo de modo:** Cuando selecciona un modo de radio real del combo de modo mientras WFM está activo en ese slice, AetherSDR emite automáticamente `wfmActivated(false, sliceId)` para desmontar la superposición de WFM. No se admite la selección de "WFM" desde el combo de modo; WFM se controla exclusivamente mediante el botón dedicado.

## Cambios en el modo RADE

La lógica de activación del modo RADE se ha actualizado para reflejar que "RADE" es solo un modo del lado del cliente:

- Cuando selecciona RADE del combo de modo, el cliente establece el modo del slice en "RADE" y emite `radeActivated(true, sliceId)`. La radio en sí misma devuelve inmediatamente el modo subyacente real (típicamente DIGL o DIGU).
- AetherSDR ya no establece el modo del slice en la radio cuando se selecciona RADE. En su lugar, se utiliza la retroalimentación del modo de la radio.
- En la v26.5.3, `radeActivated(false)` se emite solo al cambiar de RADE en un slice que estaba genuinamente en modo RADE (#2376). Esto evita señales de desactivación obsoletas al cambiar de modo en un slice que no es RADE.
- Si necesita desactivar explícitamente el modo RADE en un slice, cambie el modo a un modo que no sea RADE usando el combo de modo.

## Comportamiento de las pestañas de slice

En la v0.9.5.1, la fila de pestañas de slice obtuvo una gestión del ciclo de vida más robusta para solucionar problemas observados en reconexiones de radio (#2254).

- Cuando la radio informa un número diferente de slices del que contiene la fila de pestañas actual, AetherSDR destruye todos los botones de pestaña existentes (`clearSlice

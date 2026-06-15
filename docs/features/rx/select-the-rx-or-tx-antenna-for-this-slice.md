# Aplicación de Controles RX

La aplicación de Controles RX proporciona controles de recepción por slice: modo, sintonización de frecuencia, selección de antena RX/TX, ancho de filtro, AGC, ganancia AF/paneo, silenciador, RIT/XIT, configuración de dúplex para repetidores FM y el nuevo demodulador de software WFM. Un solo clic en el botón de silencio silencia este slice; un doble clic silencia/restaura el sonido de todos los slices que posea.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se completa a partir de la configuración de puertos de la propia radio. Confirme que sus antenas estén conectadas y sean reconocidas por la radio antes de cambiar estos ajustes.

## Pasos

1. Abra la aplicación Controles RX. Si no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A a H) para el slice que desea cambiar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior de la aplicación (muestra la antena RX actual, p. ej. **ANT1**). Aparece un menú que lista todos los puertos de antena disponibles. Haga clic en el puerto que desee. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, p. ej. **ANT1**). Aparece un menú que lista los puertos de antena con capacidad TX. Haga clic en el puerto que desee.
5. **Para habilitar WFM:** Haga clic en el botón **WFM**. Esto activa un demodulador FM por software a través de DAX IQ → Cable Hi-Fi. El botón se ilumina en verde cuando está activo. Al cambiar el modo (USB, LSB, etc.), WFM se desactiva automáticamente.
6. **Para calibrar AGC-T:** Haga clic derecho en el deslizador del umbral AGC y seleccione **Calibrar AGC-T contra el piso de ruido…** en el menú contextual. Esto abre el panel de calibración AGC-T para el slice actual.

## Qué hace cada control

| Control                           | Valor predeterminado | Valores válidos                                                               |
|-----------------------------------|----------------------|--------------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1               | Puertos de antena de la ant_list de la radio o de la propia rxAntennaList del slice |
| **ANT1** (antena TX, etiqueta roja) | ANT1               | Puertos con capacidad TX de la ant_list de la radio                           |
| **Pestañas de slice (A..H)**      | Ninguno              | 1–8 botones (limitado por el máximo de slices del hardware)                   |
| **Insignia de slice**             | A                   | A/B/C/D/E/F/G/H (representado como texto enriquecido HTML)                    |
| **🔓 / 🔒**                        | 🔓                   | Desbloqueado / Bloqueado                                                      |
| **WFM**                           | Desactivado          | Botón de alternancia; verde cuando está activo                                |
| **Combo de modo**                 | USB                 | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY, WFM (+ RADE si HAVE_RADE) |
| **Etiqueta de frecuencia**        | 0.000.000           | 0.001–54.000 MHz (450.000 MHz en XVTR)                                        |
| **Edición de frecuencia**         | Ninguno             | 0.001–54.000 MHz (450.000 MHz en XVTR); acepta auto-escalado kHz/Hz           |
| **PASO**                          | 100 Hz              | Lista de tamaños de paso por modo                                             |
| **Preajustes de ancho de filtro** | Ninguno             | Anchuras preajustadas por modo                                                |
| **Widget de banda de paso del filtro** | Ninguno         | Arrastre los bordes lo/hi para ajustar la banda de paso                       |
| **Modo de tono (FM)**             | Desactivado          | Desactivado, TX CTCSS                                                         |
| **Valor del tono CTCSS**          | Ninguno             | 41 tonos EIA/TIA-603 estándar (67.0–254.1 Hz)                                 |
| **Desplazamiento (FM)**           | 0.0 MHz             | 0.0–100.0 MHz (paso 0.1)                                                      |
| **− (desplazamiento hacia abajo)** | Ninguno            | Alternancia                                                                   |
| **Simplex**                       | Marcado             | Alternancia                                                                   |
| **+ (desplazamiento hacia arriba)** | Ninguno           | Alternancia                                                                   |
| **REV**                           | Ninguno             | Alternancia                                                                   |
| **🔊 / 🔇 (silencio)**             | 🔊                   | Sin silencio / Silenciado                                                     |
| **Ganancia AF**                   | 70                  | 0–100                                                                         |
| **Paneo L / R**                   | 50                  | 0–100                                                                         |
| **SQL**                           | Ninguno             | Alternancia                                                                   |
| **Nivel de silenciador**          | 20                  | 0–100 (persistido en el cliente como `LastManualSquelchLevel`)                 |
| **Modo AGC**                      | Med                 | Desactivado, Lento, Medio, Rápido                                             |
| **Umbral AGC**                    | 65                  | 0–100                                                                         |
| **RIT**                           | Ninguno             | Alternancia                                                                   |
| **RIT 0**                         | Ninguno             | Botón pulsador                                                                |
| **Desplazamiento RIT**            | +0 Hz               | Paso 10 Hz                                                                    |
| **XIT**                           | Ninguno             | Alternancia                                                                   |
| **XIT 0**                         | Ninguno             | Botón pulsador                                                                |
| **Desplazamiento XIT**            | +0 Hz               | Paso 10 Hz                                                                    |
| **TX (insignia)**                 | Ninguno             | Haga clic para establecer como slice TX                                       |
| **QSK**                           | Ninguno             | Ámbar cuando el break-in CW está activo (solo lectura)                        |
| **Ancho de filtro (indicador)**   | 2.7K                | Ancho de banda del filtro actual                                              |

## Qué muestra cada indicador

| Indicador        | Estados                                       | Significado                                        |
|------------------|-----------------------------------------------|----------------------------------------------------|
| Ancho de filtro | p. ej. '2.7K', '3.3K', '500', '6.0K'          | Ancho de banda del filtro del slice actual         |
| QSK              | desactivado (gris), activado (ámbar)           | Estado de break-in completo CW reflejado desde la aplicación CW |

## Consejos

- La etiqueta de la antena RX se muestra en azul; la etiqueta de la antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX. El menú de antena TX también incluye puertos cuyos nombres comienzan con `ANT`, `TX` o `XVTR`.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- Desde la versión v0.9.3, los botones de pestaña de slice y la insignia de slice utilizan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidor. Los colores no son configurables desde la página de controles de antena; se aplican en toda la aplicación.
- El indicador de ancho de filtro comparte la lógica de formato sensible al modo con el panel VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas consistentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para que los atajos de teclado de ampliar/reducir produzcan una geometría de bordes correcta según el modo (#2208). Por ejemplo, al ampliar desde un filtro USB de 2.7 kHz, se selecciona el siguiente preajuste más grande (p. ej. 2.9 kHz) con la colocación de bordes adecuada para el modo USB, en lugar de una banda de paso simétrica.
- Desde la versión v26.5.2.1, la insignia de slice admite la representación de texto enriquecido HTML (#2606). Esto permite que la letra del slice se estilice con formato HTML si es necesario.
- El nivel manual del silenciador se persiste en el cliente como el ajuste `LastManualSquelchLevel`. Esto preserva su preferencia de silenciador manual entre ciclos de modo, reconexiones de radio y reinicios de la aplicación. El algoritmo de silenciador automático de la propia radio puede modificar el nivel de silenciador del slice, pero AetherSDR restaura el último nivel manual elegido por el usuario cuando el modo Auto no está activo.
- Desde la versión v26.6.1, los botones de preajuste de filtro (1.8K, 2.1K, etc.) utilizan estilo sensible al tema mediante `kButtonBase()`, que resuelve tokens a través de ThemeManager. Estos botones ahora se re-tematizan junto con el resto de la interfaz de usuario cuando cambia el tema de la aplicación. Los tokens de tema utilizados son `{{color.background.1}}`, `{{color.background.2}}` y `{{color.text.primary}}`.
- Desde la versión v26.6.3, el campo de edición de frecuencia utiliza `FreqLineEdit` (una subclase de `QLineEdit`) para mejorar el manejo de entrada. Muestra "MHz" como texto de sugerencia en lugar de texto de marcador de posición.
- Desde la versión v26.6.3, el spinbox **PASO** emite `stepSizeChangedByUser` además de `stepSizeChanged` cuando el usuario cambia manualmente el tamaño del paso. Esto permite que otros componentes distingan los cambios de paso programáticos de los iniciados por el usuario.
- Desde la versión v26.6.3, el deslizador del umbral AGC tiene un menú contextual con clic derecho con una opción **Calibrar AGC-T contra el piso de ruido…**. La información sobre herramientas ahora incluye la pista "Haga clic derecho para calibrar contra el piso de ruido" para facilitar su descubrimiento.

## Cambios en el menú de antena en v26.5.2.1

Los menús de antena RX y TX se han actualizado para proporcionar una retroalimentación más clara:

- Cada elemento del menú muestra el nombre del puerto de antena tanto como información sobre herramientas como información de estado.
- Los datos de la acción del menú llevan el identificador de antena sin procesar, en lugar de utilizar el texto mostrado. Esto significa que los elementos del menú pueden mostrar etiquetas formateadas (p. ej., con indicadores de tipo de puerto) mientras siguen seleccionando el puerto de antena correcto.
- El menú de antena RX ahora prefiere la propia `rxAntennaList()` del slice si no está vacía, recurriendo a la `ant_list` de la radio. Esto garantiza que el menú refleje cualquier restricción de antena por slice informada por la radio.

## Demodulador de software WFM (v26.6.3)

El botón **WFM** proporciona un demodulador FM por software que utiliza audio DAX IQ enrutado a través del dispositivo de audio virtual Cable Hi-Fi de su sistema.

- **Para habilitar WFM:** Haga clic en el botón **WFM**. Se ilumina en verde cuando está activo. El botón se encuentra a la derecha del combo de modo en la fila de frecuencia.
- **Para deshabilitar WFM:** Vuelva a hacer clic en el botón **WFM**, o seleccione cualquier modo de radio real del combo de modo (USB, LSB, CW, etc.). Al cambiar de modo se desactiva automáticamente WFM para ese slice.
- **Comportamiento por slice:** Cada slice tiene su propio estado WFM. Habilitar WFM en un slice no afecta a otros slices.
- **Gestión de estado:** AetherSDR emite `wfmActivated(true, sliceId)` cuando WFM se activa, y `wfmActivated(false, sliceId)` cuando WFM se desactiva (ya sea haciendo clic en el botón o cambiando el combo de modo). El método `setWfmActive()` permite que otros componentes sincronicen el estado del botón WFM mediante programación.
- **Interacción con el combo de modo:** Cuando selecciona un modo de radio real del combo de modo mientras WFM está activo en ese slice, AetherSDR emite automáticamente `wfmActivated(false, sliceId)` para desmontar la superposición WFM. No se admite seleccionar "WFM" del combo de modo; WFM se controla exclusivamente mediante el botón dedicado.

## Cambios en el modo RADE

La lógica de activación del modo RADE se ha actualizado para reflejar que "RADE" es un modo solo del lado del cliente:

- Cuando selecciona RADE del combo de modo, el cliente establece el modo del slice en "RADE" y emite `radeActivated(true, sliceId)`. La propia radio devuelve inmediatamente el modo subyacente real (normalmente DIGL o DIGU).
- AetherSDR ya no establece el modo del slice en la radio cuando se selecciona RADE. Se utiliza la retroalimentación del modo de la radio.
- En v26.5.3, `radeActivated(false)` se emite solo al cambiar de RADE en un slice que estaba genuinamente en modo RADE (#2376). Esto evita señales de desactivación obsoletas al cambiar de modo en un slice que no es RADE.
- Si necesita desactivar explícitamente el modo RADE en un slice, cambie el modo a un modo que no sea RADE usando el combo de modo.

## Comportamiento de las pestañas de slice

En v0.9.5.1, la fila de pestañas de slice obtuvo una gestión del ciclo de vida más robusta para corregir problemas observados durante las reconexiones de radio (#2254).

- Cuando la radio informa un número diferente de slices al que contiene la fila de pestañas actual, AetherSDR destruye todos los botones de pestaña existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestaña generados, oculta la fila de pestañas y restaura la insignia de slice estática. Este es también el estado que se muestra cuando la radio está desconectada.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea solo una vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados a través de reconexiones. Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados a través de reconexiones.

## Formato de almacenamiento de preajustes de filtro

Desde v0.9.5.1, los preajustes de filtro guardados al hacer clic derecho en un botón de **Preajustes de ancho de filtro** pueden almacenar una anchura simple o un par de bordes de banda de paso específico (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **anchura simple** se almacena como un solo entero (p. ej. `2700`). Al aplicarla, la radio coloca la banda de paso simétricamente según el modo actual.
- Una entrada de **borde lo:hi** se almacena como dos enteros separados por dos puntos (p. ej. `300:3000`). Al aplicarla, AetherSDR establece los bordes de banda de paso bajo y alto exactamente como se guardaron.

Ambos formatos pueden coexistir en la misma lista de preajustes

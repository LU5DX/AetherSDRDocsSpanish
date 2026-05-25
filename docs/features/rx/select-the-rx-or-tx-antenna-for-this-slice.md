# Seleccione la antena de RX o TX para este segmento

El applet de Controles de RX le permite elegir qué puerto de antena utiliza la FLEX-8600 para recibir y transmitir en cada segmento de forma independiente. Utilícelo cuando tenga múltiples antenas conectadas y necesite enrutar un segmento específico a un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos de la radio. Confirme que sus antenas estén conectadas y reconocidas por la radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet de Controles de RX. Si no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un segmento, haga clic en la pestaña del segmento (A a H) para el segmento que desea cambiar.
3. **Para cambiar la antena de RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena de RX actual, p. ej., **ANT1**). Aparece un menú que enumera todos los puertos de antena disponibles. Haga clic en el puerto que desee. Una marca de verificación muestra la selección actual.
4. **Para cambiar la antena de TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena de RX (también muestra la antena de TX actual, p. ej., **ANT1**). Aparece un menú que enumera los puertos de antena con capacidad de TX. Haga clic en el puerto que desee.

## Qué hace cada control

| Control                           | Valor predeterminado | Valores válidos                                                                |
|-----------------------------------|----------------------|--------------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1               | Puertos de antena de ant_list de la radio o rxAntennaList del propio segmento    |
| **ANT1** (antena TX, etiqueta roja) | ANT1               | Puertos con capacidad TX de ant_list de la radio                                  |
| **Pestañas de segmento (A..H)**   | Ninguno             | 1–8 botones (limitado por el máximo de segmentos del hardware)                    |
| **Distintivo de segmento**        | A                   | A/B/C/D/E/F/G/H (renderizado como texto HTML enriquecido)                         |
| **🔓 / 🔒**                         | 🔓                  | Desbloqueado / Bloqueado                                                          |
| **Combo de modo**                 | USB                 | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE)       |
| **Etiqueta de frecuencia**        | 0.000.000           | 0.001–54.000 MHz (450.000 MHz en XVTR)                                            |
| **Edición de frecuencia**         | Ninguno             | 0.001–54.000 MHz (450.000 MHz en XVTR); acepta autoescalado de kHz/Hz              |
| **STEP**                          | 100 Hz              | Lista de tamaños de paso por modo                                                  |
| **Preajustes de ancho de filtro**  | Ninguno             | Anchuras preajustadas por modo                                                     |
| **Widget de banda de paso del filtro** | Ninguno          | Arrastre los bordes lo/hi para ajustar la banda de paso                            |
| **Modo de tono (FM)**             | Desactivado         | Desactivado, CTCSS TX                                                              |
| **Valor de tono CTCSS**           | Ninguno             | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz)                                     |
| **Offset (FM)**                   | 0.0 MHz             | 0.0–100.0 MHz (paso 0.1)                                                           |
| **− (offset hacia abajo)**        | Ninguno             | Alternar                                                                           |
| **Simplex**                       | Marcado             | Alternar                                                                           |
| **+ (offset hacia arriba)**       | Ninguno             | Alternar                                                                           |
| **REV**                           | Ninguno             | Alternar                                                                           |
| **🔊 / 🔇 (silencio)**              | 🔊                  | Con sonido / Silenciado                                                            |
| **Ganancia de AF**                | 70                  | 0–100                                                                              |
| **Pan L / R**                     | 50                  | 0–100                                                                              |
| **SQL**                           | Ninguno             | Alternar                                                                           |
| **Nivel de squelch**              | 20                  | 0–100 (persistido en el cliente como `LastManualSquelchLevel`)                     |
| **Modo AGC**                      | Med                 | Desactivado, Slow, Med, Fast                                                       |
| **Umbral AGC**                    | 65                  | 0–100                                                                              |
| **RIT**                           | Ninguno             | Alternar                                                                           |
| **RIT 0**                         | Ninguno             | Pulsador                                                                           |
| **Offset RIT**                    | +0 Hz               | Paso 10 Hz                                                                         |
| **XIT**                           | Ninguno             | Alternar                                                                           |
| **XIT 0**                         | Ninguno             | Pulsador                                                                           |
| **Offset XIT**                    | +0 Hz               | Paso 10 Hz                                                                         |
| **TX (distintivo)**               | Ninguno             | Haga clic para establecer como segmento TX                                         |
| **QSK**                           | Ninguno             | Ámbar cuando el break-in de CW está activo (solo lectura)                          |
| **Ancho de filtro (indicador)**   | 2.7K                | Ancho de banda actual del filtro                                                   |

## Qué muestra cada indicador

| Indicador        | Estados                                       | Significado                                        |
|------------------|-----------------------------------------------|----------------------------------------------------|
| Ancho de filtro | p. ej., '2.7K', '3.3K', '500', '6.0K'        | Ancho de banda actual del filtro del segmento       |
| QSK              | desactivado (gris), activado (ámbar)          | Estado de break-in completo de CW reflejado desde el applet de CW |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX. El menú de antena TX también incluye puertos cuyos nombres comienzan con `ANT`, `TX` o `XVTR`.
- Cada segmento tiene su propia asignación de antena RX y TX independiente. Cambiar la antena en el segmento A no afecta al segmento B.
- Desde v0.9.3, los botones de pestaña de segmento y el distintivo de segmento utilizan colores por segmento gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets de VFO y las tiras de medidores. Los colores no se pueden configurar desde la página de controles de antena; se aplican en todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato sensible al modo con el panel de VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas consistentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para que los atajos de teclado de ampliar/reducir produzcan una geometría de borde correcta para el modo (#2208). Por ejemplo, al ampliar desde un filtro USB de 2.7 kHz, se selecciona el siguiente preajuste más grande (p. ej., 2.9 kHz) con la ubicación de borde adecuada para el modo USB en lugar de una banda de paso simétrica.
- Desde v26.5.2.1, el distintivo de segmento admite renderizado de texto HTML enriquecido (#2606). Esto permite que la letra del segmento se estilice con formato HTML si es necesario.
- El nivel manual de squelch se persiste en el cliente como el ajuste `LastManualSquelchLevel`. Esto preserva su preferencia de squelch manual entre ciclos de modo, reconexiones de radio y reinicios de la aplicación. El algoritmo automático de squelch de la radio puede modificar el nivel de squelch del segmento, pero AetherSDR restaura el último nivel manual elegido por el usuario cuando el modo Auto no está activo.

## Cambios en el menú de antena en v26.5.2.1

Los menús de antena RX y TX se han actualizado para proporcionar una retroalimentación más clara:

- Cada elemento del menú muestra el nombre del puerto de antena como información sobre herramientas y sugerencia de estado.
- Los datos de acción del menú contienen el identificador de antena sin procesar, en lugar de utilizar el texto mostrado. Esto significa que los elementos del menú pueden mostrar etiquetas formateadas (p. ej., con indicadores de tipo de puerto) mientras siguen seleccionando el puerto de antena correcto.
- El menú de antena RX ahora prefiere `rxAntennaList()` del propio segmento si no está vacío, recurriendo a `ant_list` de la radio. Esto garantiza que el menú refleje cualquier restricción de antena por segmento informada por la radio.

## Cambios en el modo RADE

La lógica de activación del modo RADE se ha actualizado para reflejar que "RADE" es solo un modo del lado del cliente:

- Cuando selecciona RADE en el combo de modo, el cliente establece el modo del segmento en "RADE" y emite `radeActivated(true, sliceId)`. La radio misma devuelve inmediatamente el modo real subyacente (normalmente DIGL o DIGU).
- AetherSDR ya no establece el modo del segmento en la radio cuando se selecciona RADE. Se utiliza la retroalimentación del modo de la radio.
- En v26.5.3, `radeActivated(false)` se emite solo al cambiar del modo RADE en un segmento que estaba genuinamente en modo RADE (#2376). Esto evita señales de desactivación obsoletas al cambiar de modo en un segmento que no está en RADE.
- Si necesita desactivar explícitamente el modo RADE en un segmento, cambie el modo a un modo que no sea RADE usando el combo de modo.

## Comportamiento de las pestañas de segmento

En v0.9.5.1, la fila de pestañas de segmento obtuvo una gestión del ciclo de vida más robusta para solucionar problemas observados durante las reconexiones de radio (#2254).

- Cuando la radio informa un número diferente de segmentos del que contiene la fila de pestañas actual, AetherSDR elimina todos los botones de pestaña existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestaña generados, oculta la fila de pestañas y restaura el distintivo de segmento estático. Este es también el estado que se muestra cuando la radio está desconectada.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea solo una vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados durante las reconexiones. Las conexiones de clic de los botones de segmento están protegidas contra manejadores de señal duplicados durante las reconexiones.

## Formato de almacenamiento de preajustes de filtro

Desde v0.9.5.1, los preajustes de filtro guardados al hacer clic derecho en un botón de **Preajustes de ancho de filtro** pueden almacenar un ancho simple o un par de bordes de banda de paso específico (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **ancho simple** se almacena como un solo entero (p. ej., `2700`). Al aplicarlo, la radio coloca la banda de paso simétricamente según el modo actual.
- Una entrada de **borde lo:hi** se almacena como dos enteros separados por dos puntos (p. ej., `300:3000`). Al aplicarlo, AetherSDR establece los bordes de banda de paso bajo y alto exactamente como se guardaron.

Ambos formatos pueden coexistir en la misma lista de preajustes para un modo dado. La clave de ajuste es `FilterPresets_<mode>` (p. ej., `FilterPresets_USB`). Se muestran hasta seis preajustes en el applet de Controles de RX para cada modo.

Si una entrada guardada tiene un formato incorrecto o tiene un borde alto que no supera al borde bajo, AetherSDR omite esa entrada silenciosamente al cargar los preajustes.

## Comportamiento del modo NT y modo RTTY

NT y RTTY son modos digitales. Su comportamiento dentro del applet de Controles de RX coincide con otros modos digitales (DIGU/DIGL) en los siguientes aspectos:

- **Preajustes de filtro** — NT y RTTY utilizan las mismas anchuras de preajuste de filtro que DIGU y DIGL (100–2000 Hz).
- **Visualización del ancho de filtro** — El indicador de ancho de filtro obtiene su valor del borde alto de la banda de paso, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Squelch** — El botón **SQL** y el control deslizante de nivel de squelch están deshabilitados en el modo NT y el modo RTTY. Si el squelch estaba activo cuando cambió al modo NT o RTTY, AetherSDR desactiva el squelch automáticamente y lo restaura cuando vuelve a cambiar. Esto coincide con el comportamiento de DIGU y DIGL; el modo CW se maneja de manera diferente porque la radio gestiona su estado de squelch directamente. La desactivación del squelch en RTTY evita el enmascaramiento de señales FSK débiles que de otro modo serían eliminadas (#2504).

## Comportamiento del botón de silencio en v26.5.3

El botón de silencio (🔊/🔇) se ha actualizado para un comportamiento más fiable con acciones de un solo clic y doble clic:

- **Un solo clic** — Silencia o reactiva el sonido del segmento actual. La acción se difiere por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla.
- **Doble clic** — Silencia o reactiva el sonido de todos los segmentos propietarios simultáneamente.
- **Actualizaciones de icono** — El icono visual (🔊/🔇) ya no se actualiza inmediatamente al hacer clic. En su lugar, el icono se actualiza cuando la radio confirma el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto garantiza que el icono refleje siempre el estado real de la radio.
- **Según la Política de Ajustes Autoritativos de la Radio (#2489)** — El estado de silencio NO se guarda ni se restaura al reconectar. La radio es la fuente de verdad para el estado de silencio de audio.
- El `muteClickTimer` maneja el diferimiento del clic único. Si llega un segundo clic antes de que se active el temporizador, el temporizador se detiene y el manejador de doble clic silencia todos los segmentos en su lugar.

## Ingreso de frecuencia en v26.5.3

El campo de ingreso de frecuencia ahora utiliza `FrequencyEntryParser` para el análisis de texto MHz normalizado, y tiene soporte mejorado para ingresos de alta frecuencia:

- **Autoescalado de MHz** — Ingresar un valor superior a 54 MHz aplica autoescalado: los valores superiores a 54.000 se dividen por 1e6 (se asumen Hz), los valores superiores a 54 se dividen por 1e3 (se asumen kHz), y los ingresos explícitos de MHz por encima de 54 MHz se aceptan para operación tipo XVTR.
- **Ingresos explícitos de MHz por encima de 54 MHz** — Si ingresa una frecuencia con un punto decimal en un formato que `Frequency

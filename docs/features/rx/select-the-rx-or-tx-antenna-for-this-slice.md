# Seleccione la antena RX o TX para este slice

El applet de controles RX le permite seleccionar qué puerto de antena utiliza la FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Utilícelo cuando tenga varias antenas conectadas y necesite enrutar un slice específico a un puerto determinado.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos de la radio. Verifique que sus antenas estén conectadas y sean reconocidas por la radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet **RX Controls**. Si no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A a la H) correspondiente al slice que desea cambiar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, por ejemplo, **ANT1**). Aparece un menú que lista todos los puertos de antena disponibles. Haga clic en el puerto deseado. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, por ejemplo, **ANT1**). Aparece un menú que lista los puertos de antena con capacidad TX. Haga clic en el puerto deseado.

## Qué hace cada control

| Control                           | Valor predeterminado | Valores válidos                                                              |
|-----------------------------------|----------------------|------------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1                 | Puertos de antena de ant_list de la radio o de rxAntennaList del slice       |
| **ANT1** (antena TX, etiqueta roja) | ANT1                 | Puertos con capacidad TX de ant_list de la radio                             |
| **Pestañas de slice (A..H)**      | Ninguno              | Botones 1–8 (limitado por el máximo de slices del hardware)                  |
| **Distintivo de slice**           | A                    | A/B/C/D/E/F/G/H (representado como texto enriquecido HTML)                  |
| **🔓 / 🔒**                       | 🔓                    | Desbloqueado / Bloqueado                                                     |
| **Combo de modo**                 | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si se compila con HAVE_RADE) |
| **Etiqueta de frecuencia**        | 0.000.000            | 0.001–54.000 MHz (450.000 MHz en XVTR)                                       |
| **Edición de frecuencia**         | Ninguno              | 0.001–54.000 MHz (450.000 MHz en XVTR); acepta autoescala kHz/Hz             |
| **STEP**                          | 100 Hz               | Lista de tamaños de paso por modo                                             |
| **Preajustes de ancho de filtro** | Ninguno              | Anchuras preajustadas por modo                                                |
| **Widget de banda pasante**       | Ninguno              | Arrastre los bordes lo/hi para ajustar la banda pasante                      |
| **Modo de tono (FM)**             | Off                  | Off, CTCSS TX                                                                |
| **Valor del tono CTCSS**          | Ninguno              | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz)                                |
| **Offset (FM)**                   | 0.0 MHz              | 0.0–100.0 MHz (paso 0.1)                                                     |
| **− (desplazamiento hacia abajo)**| Ninguno              | Alternar                                                                    |
| **Simplex**                       | Marcado              | Alternar                                                                    |
| **+ (desplazamiento hacia arriba)**| Ninguno             | Alternar                                                                    |
| **REV**                           | Ninguno              | Alternar                                                                    |
| **🔊 / 🔇 (mute/silencio)**       | 🔊                    | Sin silenciar / Silenciado                                                    |
| **Ganancia AF**                   | 70                   | 0–100                                                                        |
| **Pan L / R**                     | 50                   | 0–100                                                                        |
| **SQL**                           | Ninguno              | Alternar                                                                    |
| **Nivel de squelch**              | 20                   | 0–100 (persistido en el cliente como `LastManualSquelchLevel`)                |
| **Modo AGC**                      | Med                  | Off, Slow, Med, Fast                                                          |
| **Umbral AGC**                    | 65                   | 0–100                                                                        |
| **RIT**                           | Ninguno              | Alternar                                                                    |
| **RIT 0**                         | Ninguno              | Botón pulsador                                                              |
| **Offset RIT**                    | +0 Hz                | Paso 10 Hz                                                                   |
| **XIT**                           | Ninguno              | Alternar                                                                    |
| **XIT 0**                         | Ninguno              | Botón pulsador                                                              |
| **Offset XIT**                    | +0 Hz                | Paso 10 Hz                                                                   |
| **TX (distintivo)**               | Ninguno              | Haga clic para establecer como slice TX                                      |
| **QSK**                           | Ninguno              | Ámbar cuando el break-in de CW está activo (solo lectura)                     |
| **Ancho de filtro (indicador)**   | 2.7K                 | Ancho de banda del filtro actual                                              |

## Qué muestra cada indicador

| Indicador        | Estados                                    | Significado                                       |
|------------------|--------------------------------------------|---------------------------------------------------|
| Ancho de filtro  | p. ej., '2.7K', '3.3K', '500', '6.0K'      | Ancho de banda del filtro del slice actual         |
| QSK              | apagado (gris), encendido (ámbar)           | Estado de break-in completo de CW reflejado desde el applet CW |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única diferencia visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX. El menú de antena TX también incluye puertos cuyos nombres comienzan con `ANT`, `TX` o `XVTR`.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- Desde la versión 0.9.3, los botones de pestaña de slice y el distintivo de slice utilizan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets VFO y las tiras de medidores. Los colores no son configurables desde la página de controles de antena; se aplican a todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato sensible al modo con el panel VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas coherentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para que los atajos de teclado de ampliar/reducir produzcan una geometría de bordes correcta para el modo (#2208). Por ejemplo, al ampliar desde un filtro USB de 2.7 kHz se selecciona el siguiente preajuste más grande (p. ej., 2.9 kHz) con la colocación de borde adecuada para el modo USB en lugar de una banda pasante simétrica.
- Desde la versión 26.5.2.1, el distintivo de slice admite representación de texto enriquecido HTML (#2606). Esto permite que la letra del slice se pueda estilizar con formato HTML si es necesario.
- El nivel manual de squelch se persiste en el cliente como el ajuste `LastManualSquelchLevel`. Esto preserva su preferencia de squelch manual en ciclos de modo, reconexiones de radio y reinicios de la aplicación. El algoritmo automático de squelch de la radio puede modificar el nivel de squelch del slice, pero AetherSDR restaura el último nivel manual elegido por el usuario cuando el modo Auto no está activo.
- Desde la versión 26.6.1, los botones de preajuste de filtro (1.8K, 2.1K, etc.) utilizan un estilo sensible al tema mediante `kButtonBase()`, que resuelve tokens a través de ThemeManager. Estos botones ahora cambian de tema junto con el resto de la interfaz de usuario cuando el tema de la aplicación cambia. Los tokens de tema utilizados son `{{color.background.1}}`, `{{color.background.2}}` y `{{color.text.primary}}`.

## Cambios en el menú de antena en la versión 26.5.2.1

Los menús de antena RX y TX se han actualizado para proporcionar una retroalimentación más clara:

- Cada elemento del menú muestra el nombre del puerto de antena como tooltip y status tip.
- Los datos de acción del menú llevan el identificador de antena sin procesar, en lugar de utilizar el texto mostrado. Esto significa que los elementos del menú pueden mostrar etiquetas formateadas (p. ej., con indicadores de tipo de puerto) mientras seleccionan el puerto de antena correcto.
- El menú de antena RX ahora prefiere la `rxAntennaList()` del slice si no está vacía, recurriendo a la `ant_list` de la radio en caso contrario. Esto asegura que el menú refleje cualquier restricción de antena por slice informada por la radio.

## Cambios en el modo RADE

La lógica de activación del modo RADE se ha actualizado para reflejar que "RADE" es un modo solo del lado del cliente:

- Cuando selecciona RADE en el combo de modo, el cliente establece el modo del slice en "RADE" y emite `radeActivated(true, sliceId)`. La radio misma devuelve inmediatamente el modo real subyacente (normalmente DIGL o DIGU).
- AetherSDR ya no establece el modo del slice en la radio cuando se selecciona RADE. Se utiliza la retroalimentación del modo de la radio en su lugar.
- En la versión 26.5.3, `radeActivated(false)` se emite solo al cambiar fuera de RADE en un slice que estaba genuinamente en modo RADE (#2376). Esto evita señales de desactivación obsoletas al cambiar de modo en un slice que no está en RADE.
- Si necesita desactivar explícitamente el modo RADE en un slice, cambie el modo a un modo que no sea RADE usando el combo de modo.

## Comportamiento de las pestañas de slice

En la versión 0.9.5.1, la fila de pestañas de slice obtuvo una gestión del ciclo de vida más robusta para solucionar problemas observados en reconexiones de radio (#2254).

- Cuando la radio informa un número diferente de slices del que contiene la fila de pestañas actual, AetherSDR destruye todos los botones de pestaña existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestaña generados, oculta la fila de pestañas y restaura el distintivo de slice estático. Este es también el estado que se muestra cuando la radio está desconectada.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea solo una vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de manejadores de señal duplicados en las reconexiones. Las conexiones de clic de los botones de slice están protegidas contra manejadores de señal duplicados en las reconexiones.

## Formato de almacenamiento de preajustes de filtro

Desde la versión 0.9.5.1, los preajustes de filtro guardados al hacer clic derecho en un botón de **Preajustes de ancho de filtro** pueden almacenar un ancho simple o un par específico de bordes de banda pasante (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **ancho simple** se almacena como un solo entero (p. ej., `2700`). Al aplicarse, la radio coloca la banda pasante simétricamente según el modo actual.
- Una entrada de **borde lo:hi** se almacena como dos enteros separados por dos puntos (p. ej., `300:3000`). Al aplicarse, AetherSDR establece los bordes de banda pasante bajo y alto exactamente como se guardaron.

Ambos formatos pueden coexistir en la misma lista de preajustes para un modo dado. La clave del ajuste es `FilterPresets_<modo>` (p. ej., `FilterPresets_USB`). Se muestran hasta seis preajustes en el applet de controles RX para cada modo.

Si una entrada guardada tiene un formato incorrecto o tiene un borde alto que no supera al borde bajo, AetherSDR omite esa entrada silenciosamente al cargar los preajustes.

## Comportamiento de los modos NT y RTTY

NT y RTTY son modos digitales. Su comportamiento dentro del applet de controles RX coincide con otros modos digitales (DIGU/DIGL) en los siguientes aspectos:

- **Preajustes de filtro** — NT y RTTY utilizan las mismas anchuras de preajuste de filtro que DIGU y DIGL (100–2000 Hz).
- **Visualización del ancho de filtro** — El indicador de ancho de filtro obtiene su valor del borde alto de la banda pasante, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Squelch** — El botón **SQL** y el deslizador de nivel de squelch están deshabilitados en modo NT y modo RTTY. Si el squelch estaba activo cuando cambió al modo NT o RTTY, AetherSDR desactiva el squelch automáticamente y lo restaura cuando vuelve a cambiar. Esto coincide con el comportamiento para DIGU y DIGL; el modo CW se maneja de manera diferente porque la radio gestiona su estado de squelch directamente. La desactivación del squelch en RTTY evita el bloqueo de señales FSK débiles que de otro modo serían eliminadas (#2504).

## Comportamiento del botón de silencio (mute) en la versión 26.5.3

El botón de silencio (🔊/🔇) se ha actualizado para un comportamiento más fiable con acciones de un solo clic y doble clic:

- **Un solo clic** — Silencia o reactiva el slice actual. La acción se difiere por el intervalo de doble clic de la plataforma (típicamente ~400 ms) para que un doble clic pueda anularla.
- **Doble clic** — Silencia o reactiva todos los slices propietarios simultáneamente.
- **Actualizaciones de icono** — El icono visual (🔊/🔇) ya no se actualiza inmediatamente al hacer clic. En su lugar, el icono se actualiza cuando la radio reconoce el cambio de estado de silencio a través de `SliceModel::audioMuteChanged`. Esto asegura que el icono refleje siempre el estado real de la radio.
- **Según la política de ajustes con autoridad en la radio (#2489)** — El estado de silencio NO se guarda ni restaura al reconectar. La radio es la fuente de verdad para el estado de silencio de audio.
- El `muteClickTimer` gestiona el diferimiento del clic único. Si llega un segundo clic antes de que se active el temporizador, el temporizador se detiene y el manejador de doble clic silencia todos los slices en su lugar.

## Ingreso de frecuencia en la versión 26.5.3

El campo de ingreso de frecuencia ahora utiliza `FrequencyEntryParser` para el análisis normalizado de texto en MHz, y tiene soporte mejorado para entradas de alta frecuencia:

- **Autoescala en MHz** — Ingresar un valor superior a 54 MHz aplica autoescala: los valores superiores a 54,000 se dividen por 1e

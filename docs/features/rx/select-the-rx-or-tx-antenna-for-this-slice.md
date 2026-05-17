# Seleccionar la antena de RX o TX para un slice

El applet de Controles de RX le permite elegir qué puerto de antena utiliza el FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Utilícelo cuando tenga varias antenas conectadas y necesite encaminar un slice específico a un puerto concreto.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos del propio equipo. Confirme que sus antenas están conectadas y reconocidas por el equipo antes de cambiar estos ajustes.

## Pasos

1. Abra el applet de Controles de RX. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A a H) correspondiente al slice que desea cambiar.
3. **Para cambiar la antena de RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena de RX actual, p. ej., **ANT1**). Aparece un menú que enumera todos los puertos de antena disponibles. Haga clic en el puerto deseado. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena de TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena de RX (también muestra la antena de TX actual, p. ej., **ANT1**). Aparece un menú que enumera los puertos de antena con capacidad de TX. Haga clic en el puerto deseado.

## Función de cada control

| Control                           | Valor predeterminado | Valores válidos                                                             |
|-----------------------------------|----------------------|-----------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1               | Puertos de antena de ant_list del equipo o de rxAntennaList del slice       |
| **ANT1** (antena TX, etiqueta roja) | ANT1               | Puertos con capacidad TX de ant_list del equipo                             |
| **Pestañas de slice (A..H)**      | Ninguno              | Botones 1–8 (limitados por el máximo de slices del hardware)                |
| **Insignia de slice**             | A                    | A/B/C/D/E/F/G/H (representado como texto enriquecido HTML)                 |
| **🔓 / 🔒**                         | 🔓                   | Desbloqueado / Bloqueado                                                    |
| **Combo de modo**                 | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE)|
| **Etiqueta de frecuencia**        | 0.000.000            | 0.001–54.000 MHz (450.000 MHz en XVTR)                                     |
| **Edición de frecuencia**         | Ninguno              | 0.001–54.000 MHz (450.000 MHz en XVTR)                                     |
| **PASO**                          | 100 Hz               | Lista de tamaños de paso por modo                                           |
| **Preajustes de ancho de filtro** | Ninguno              | Anchuras preajustadas por modo                                              |
| **Widget de banda pasante del filtro** | Ninguno          | Arrastre los bordes lo/hi para ajustar la banda pasante                     |
| **Modo de tono (FM)**             | Desactivado          | Desactivado, CTCSS TX                                                       |
| **Valor de tono CTCSS**           | Ninguno              | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz)                               |
| **Desplazamiento (FM)**           | 0.0 MHz              | 0.0–100.0 MHz (paso 0.1)                                                    |
| **− (desplazamiento hacia abajo)** | Ninguno              | Alternar                                                                     |
| **Simplex**                       | Marcado              | Alternar                                                                     |
| **+ (desplazamiento hacia arriba)** | Ninguno             | Alternar                                                                     |
| **REV**                           | Ninguno              | Alternar                                                                     |
| **🔊 / 🔇 (silencio)**              | 🔊                    | Sin silenciar / Silenciado                                                  |
| **Ganancia AF**                   | 70                   | 0–100                                                                       |
| **Panorámica L / R**              | 50                   | 0–100                                                                       |
| **SQL**                           | Ninguno              | Alternar                                                                     |
| **Nivel de silenciador**          | 20                   | 0–100 (conservado en el cliente como `LastManualSquelchLevel`)              |
| **Modo CAG**                      | Med                  | Off, Slow, Med, Fast                                                        |
| **Umbral CAG**                    | 65                   | 0–100                                                                       |
| **RIT**                           | Ninguno              | Alternar                                                                     |
| **RIT 0**                         | Ninguno              | Pulsador                                                                     |
| **Desplazamiento RIT**            | +0 Hz                | Paso 10 Hz                                                                  |
| **XIT**                           | Ninguno              | Alternar                                                                     |
| **XIT 0**                         | Ninguno              | Pulsador                                                                     |
| **Desplazamiento XIT**            | +0 Hz                | Paso 10 Hz                                                                  |
| **TX (insignia)**                 | Ninguno              | Haga clic para establecer como slice de TX                                  |
| **QSK**                           | Ninguno              | Ámbar cuando el break-in de CW está activo (solo lectura)                   |
| **Ancho de filtro (indicador)**   | 2.7K                 | Ancho de banda del filtro actual                                            |

## Consejos

- La etiqueta de la antena de RX se muestra en azul; la etiqueta de la antena de TX se muestra en rojo. Esta es la única diferencia visual entre ambos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena de TX. Seguirán apareciendo en el menú de antena de RX. El menú de antena de TX también incluye puertos cuyos nombres comienzan con `ANT`, `TX` o `XVTR`.
- Cada slice tiene su propia asignación independiente de antena de RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- Desde la versión v0.9.3, los botones de pestaña de slice y la insignia de slice utilizan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets de VFO y las tiras de medidores. Los colores no se pueden configurar desde la página de controles de antena; se aplican a todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato según el modo con el panel VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas coherentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preajustes de filtro por modo para que los atajos de teclado de ampliar/reducir produzcan una geometría de bordes correcta según el modo (#2208). Por ejemplo, al ampliar desde un filtro USB de 2.7 kHz, se selecciona el siguiente preajuste más grande (p. ej., 2.9 kHz) con la colocación de bordes adecuada para el modo USB, en lugar de una banda pasante simétrica.
- Desde la versión v26.5.2.1, la insignia de slice admite representación de texto enriquecido HTML (#2606). Esto permite aplicar formato HTML a la letra del slice si es necesario.
- El nivel manual de silenciador se conserva en el cliente como el ajuste `LastManualSquelchLevel`. Esto preserva su preferencia de silenciador manual entre ciclos de modo, reconexiones de radio y reinicios de la aplicación. El algoritmo automático de silenciador del equipo puede modificar el nivel de silenciador del slice, pero AetherSDR restaura el último nivel manual elegido por el usuario cuando el modo Auto no está activo.

## Cambios en el menú de antena en v26.5.2.1

Los menús de antena de RX y TX se han actualizado para proporcionar una retroalimentación más clara:

- Cada elemento del menú muestra el nombre del puerto de antena como información sobre herramientas y sugerencia de estado.
- Los datos de la acción del menú contienen el identificador de antena sin procesar, en lugar de utilizar el texto mostrado. Esto significa que los elementos del menú pueden mostrar etiquetas con formato (p. ej., con indicadores de tipo de puerto) y al mismo tiempo seleccionar el puerto de antena correcto.
- El menú de antena de RX ahora prefiere `rxAntennaList()` del slice si no está vacío, y recurre a `ant_list` del equipo en caso contrario. Esto garantiza que el menú refleje cualquier restricción de antena por slice que informe el equipo.

## Cambios en el modo RADE en v26.5.2.1

La lógica de activación del modo RADE se ha actualizado para reflejar que "RADE" es un modo solo de cliente:

- Cuando selecciona RADE en el combo de modo, el cliente establece el modo del slice en "RADE" y emite `radeActivated(true)`. El equipo inmediatamente repite el modo real subyacente (normalmente DIGL o DIGU).
- AetherSDR ya no emite una señal `radeActivated(false)` al salir del modo RADE. Debido a que el equipo informa el modo real (DIGL/DIGU) inmediatamente después de la activación de RADE, la condición `m_slice->mode() == "RADE"` nunca es verdadera en el momento del cambio de modo. La señal de desactivación ahora se maneja de manera diferente; el cambio de selección del combo de modo lleva toda la información necesaria.
- Si necesita desactivar explícitamente el modo RADE en un slice, cambie el modo a un modo que no sea RADE usando el combo de modo.

## Comportamiento de las pestañas de slice

En la versión v0.9.5.1, la fila de pestañas de slice obtuvo una gestión del ciclo de vida más robusta para solucionar problemas observados durante las reconexiones del equipo (#2254).

- Cuando el equipo informa un número de slices diferente al que contiene la fila de pestañas actual, AetherSDR elimina todos los botones de pestaña existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestaña generados, oculta la fila de pestañas y restaura la insignia de slice estática. Este es también el estado que se muestra cuando el equipo está desconectado.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea solo una vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de controladores de señal duplicados a través de reconexiones.

## Formato de almacenamiento de preajustes de filtro

Desde la versión v0.9.5.1, los preajustes de filtro guardados al hacer clic derecho en un botón de **Preajustes de ancho de filtro** pueden almacenar una anchura simple o un par específico de bordes de banda pasante (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **anchura simple** se almacena como un solo entero (p. ej., `2700`). Al aplicarla, el equipo coloca la banda pasante simétricamente según el modo actual.
- Una entrada de **borde lo:hi** se almacena como dos enteros separados por dos puntos (p. ej., `300:3000`). Al aplicarla, AetherSDR establece los bordes inferior y superior de la banda pasante exactamente como se guardaron.

Ambos formatos pueden coexistir en la misma lista de preajustes para un modo determinado. La clave de ajuste es `FilterPresets_<mode>` (p. ej., `FilterPresets_USB`). Se muestran hasta seis preajustes en el applet de Controles de RX para cada modo.

Si una entrada guardada tiene un formato incorrecto o tiene un borde superior que no supera al borde inferior, AetherSDR omite esa entrada silenciosamente al cargar los preajustes.

## Comportamiento del modo NT y modo RTTY

NT y RTTY son modos digitales. Su comportamiento dentro del applet de Controles de RX coincide con otros modos digitales (DIGU/DIGL) en los siguientes aspectos:

- **Preajustes de filtro** — NT y RTTY utilizan las mismas anchuras de preajuste de filtro que DIGU y DIGL (100–2000 Hz).
- **Visualización del ancho de filtro** — El indicador de ancho de filtro obtiene su valor del borde superior de la banda pasante, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Silenciador** — El botón **SQL** y el control deslizante de nivel de silenciador están desactivados en el modo NT y en el modo RTTY. Si el silenciador estaba activo al cambiar al modo NT o RTTY, AetherSDR lo desactiva automáticamente y lo restaura al volver a cambiar. Esto coincide con el comportamiento para DIGU y DIGL; el modo CW se maneja de manera diferente porque el equipo gestiona su estado de silenciador directamente. La desactivación del silenciador en RTTY evita el bloqueo de señales FSK débiles que de otro modo serían eliminadas (#2504).

## Solución de problemas

- **Un puerto de antena esperado no aparece en el menú** — La lista proviene directamente de ant_list del equipo o de rxAntennaList del slice. Verifique que el puerto esté configurado y reconocido en la configuración del propio equipo. AetherSDR no puede agregar puertos que el equipo no haya informado.
- **Al menú de antena de TX le falta un puerto que aparece en el menú de antena de RX** — Los puertos cuyos nombres comienzan con `RX` están excluidos intencionalmente del menú de antena de TX porque el equipo los trata como solo recepción. Solo se incluyen en el menú de TX los puertos que comienzan con `ANT`, `TX` o `XVTR`.
- **Ambas etiquetas están atenuadas o no responden** — AetherSDR no está conectado al equipo. Vuelva a conectarse mediante `Settings > Connect to Radio...`.
- **El botón SQL está atenuado después de cambiar al modo NT o RTTY** — NT y RTTY son modos digitales. AetherSDR desactiva el silenciador en todos los modos digitales (DIGU, DIGL, NT, RTTY) porque el audio se encamina a través de DAX y el silenciador no tiene un efecto significativo. Cambie a un modo no digital para reactivar el silenciador.
- **La fila de pestañas de slice muestra pestañas incorrectas después de reconectar** — En versiones anteriores, la fila de pestañas se construía solo una vez y podía quedar obsoleta después de una reconexión. Desde la versión v0.9.5.1, AetherSDR reconstruye la fila de pestañas cada vez que cambia el número de slices. Si la fila sigue pareciendo incorrecta, desconéctese y vuelva a conectarse mediante `Settings > Connect to Radio...`.
- **Un preajuste de filtro aplica una banda pasante diferente a la esperada** — Los preajustes guardados antes de la versión v0.9.5.1 se almacenan como anchuras simples y siguen siendo válidos. Los preajustes guardados desde la versión v0.9.5.1 en adelante pueden almacenar bordes lo:hi exactos. Si un preajuste se comporta de manera inesperada, haga clic derecho en el botón de preajuste para sobrescribirlo con la banda pasante actual.
- **El nivel de silenciador se restablece después de un cambio de modo** — Desde la versión v26.5.2.1, AetherSDR conserva su nivel de silenciador manual en el lado del cliente como `LastManualSquelchLevel`. Cuando el silenciador automático sobrescribe el nivel del slice, AetherSDR restaura el último valor manual. Si el nivel aún se restablece inesperadamente, verifique si el modo de silenciador automático

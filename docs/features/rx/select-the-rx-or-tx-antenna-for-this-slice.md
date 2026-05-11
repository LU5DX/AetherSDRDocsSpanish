# Seleccionar la antena de RX o TX para este slice

El applet de Controles de RX permite elegir qué puerto de antena utiliza la FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Úselo cuando tenga múltiples antenas conectadas y necesite dirigir un slice específico a un puerto determinado.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo de radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos del propio equipo de radio. Confirme que sus antenas estén conectadas y reconocidas por el equipo antes de cambiar estos ajustes.

## Pasos

1. Abra el applet de Controles de RX. Si no es visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (de la A a la H) para el slice que desea modificar.
3. **Para cambiar la antena de RX:** haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, por ejemplo, **ANT1**). Aparece un menú con todos los puertos de antena disponibles. Haga clic en el puerto que desee. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena de TX:** haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, por ejemplo, **ANT1**). Aparece un menú con los puertos de antena con capacidad de transmisión. Haga clic en el puerto que desee.

## Función de cada control

| Control                           | Valor predeterminado | Valores válidos                                                             |
|-----------------------------------|----------------------|-----------------------------------------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1               | Puertos de antena de la ant_list del equipo de radio                        |
| **ANT1** (antena TX, etiqueta roja) | ANT1               | Puertos con capacidad TX de la ant_list del equipo de radio                |
| **Pestañas de slice (A..H)**      | Ninguno              | Botones de 1 a 8 (limitado por el máximo de slices del hardware)            |
| **Distintivo de slice**           | A                    | A/B/C/D/E/F/G/H                                                             |
| **🔓 / 🔒**                         | 🔓                    | Desbloqueado / bloqueado                                                    |
| **Combo de modo**                 | USB                  | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE) |
| **Etiqueta de frecuencia**        | 0.000.000            | 0.001–54.000 MHz (450.000 MHz en XVTR)                                     |
| **Edición de frecuencia**         | Ninguno              | 0.001–54.000 MHz (450.000 MHz en XVTR)                                     |
| **PASO**                          | 100 Hz               | Lista de tamaños de paso según el modo                                      |
| **Valores predefinidos de ancho de filtro** | Ninguno              | Anchuras predefinidas según el modo                                        |
| **Widget de banda pasante del filtro** | Ninguno              | Arrastre los bordes inferior/superior para ajustar la banda pasante         |
| **Modo de tono (FM)**             | Desactivado          | Desactivado, CTCSS TX                                                       |
| **Valor de tono CTCSS**           | Ninguno              | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz)                               |
| **Desplazamiento (FM)**           | 0.0 MHz              | 0.0–100.0 MHz (paso 0.1)                                                   |
| **− (desplazamiento hacia abajo)** | Ninguno              | Conmutación                                                                 |
| **Simplex**                       | Marcado              | Conmutación                                                                 |
| **+ (desplazamiento hacia arriba)** | Ninguno              | Conmutación                                                                 |
| **REV**                           | Ninguno              | Conmutación                                                                 |
| **🔊 / 🔇 (silencio)**              | 🔊                    | Con sonido / silenciado                                                     |
| **Ganancia de AF**                | 70                   | 0–100                                                                       |
| **Panorámica L / R**              | 50                   | 0–100                                                                       |
| **SQL**                           | Ninguno              | Conmutación                                                                 |
| **Nivel de silenciador**          | 20                   | 0–100                                                                       |
| **Modo CAG**                      | Medio                | Desactivado, Lento, Medio, Rápido                                           |
| **Umbral de CAG**                 | 65                   | 0–100                                                                       |
| **RIT**                           | Ninguno              | Conmutación                                                                 |
| **RIT 0**                         | Ninguno              | Botón pulsador                                                              |
| **Desplazamiento de RIT**         | +0 Hz                | Paso de 10 Hz                                                               |
| **XIT**                           | Ninguno              | Conmutación                                                                 |
| **XIT 0**                         | Ninguno              | Botón pulsador                                                              |
| **Desplazamiento de XIT**         | +0 Hz                | Paso de 10 Hz                                                               |
| **TX (distintivo)**               | Ninguno              | Haga clic para establecer como slice TX                                     |
| **QSK**                           | Ninguno              | Ámbar cuando el break-in de CW está activo (solo lectura)                   |
| **Ancho de filtro (indicador)**   | 2.7K                 | Ancho de banda actual del filtro                                            |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- A partir de v0.9.3, los botones de pestañas de slice y el distintivo de slice utilizan colores por slice administrados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets de VFO y las barras de medidores. Los colores no son configurables desde la página de controles de antena; se aplican a todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato según el modo con el panel de VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas coherentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de valores predefinidos de filtro por modo, de modo que los atajos de teclado para ensanchar/estrechar produzcan una geometría de borde correcta según el modo (#2208). Por ejemplo, al ensanchar desde un filtro USB de 2.7 kHz, se selecciona el siguiente valor predefinido mayor (por ejemplo, 2.9 kHz) con la ubicación de bordes adecuada para el modo USB, en lugar de una banda pasante simétrica.

## Comportamiento de las pestañas de slice

En v0.9.5.1, la fila de pestañas de slice obtuvo una gestión del ciclo de vida más robusta para solucionar problemas observados tras reconexiones del equipo de radio (#2254).

- Cuando el equipo de radio informa una cantidad de slices diferente a la que contiene la fila de pestañas actual, AetherSDR elimina todos los botones de pestañas existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestañas generados, oculta la fila de pestañas y restaura el distintivo de slice estático. Este es también el estado que se muestra cuando el equipo de radio está desconectado.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea solo una vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita que se acumulen manejadores de señal duplicados durante las reconexiones.

## Formato de almacenamiento de valores predefinidos de filtro

A partir de v0.9.5.1, los valores predefinidos de filtro guardados al hacer clic derecho en un botón de **Valores predefinidos de ancho de filtro** pueden almacenar un ancho simple o un par específico de bordes de banda pasante (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **ancho simple** se almacena como un único entero (por ejemplo, `2700`). Al aplicarlo, el equipo de radio coloca la banda pasante simétricamente según el modo actual.
- Una entrada de **borde inf:sup** se almacena como dos enteros separados por dos puntos (por ejemplo, `300:3000`). Al aplicarlo, AetherSDR establece los bordes bajo y alto de la banda pasante exactamente como fueron guardados.

Ambos formatos pueden coexistir en la misma lista de valores predefinidos para un modo determinado. La clave de configuración es `FilterPresets_<modo>` (por ejemplo, `FilterPresets_USB`). Se muestran hasta seis valores predefinidos en el applet de Controles de RX para cada modo.

Si una entrada guardada tiene un formato incorrecto o tiene un borde superior que no excede al borde inferior, AetherSDR omite esa entrada silenciosamente al cargar los valores predefinidos.

## Comportamiento del modo NT y del modo RTTY

NT y RTTY son modos digitales. Su comportamiento dentro del applet de Controles de RX coincide con otros modos digitales (DIGU/DIGL) en los siguientes aspectos:

- **Valores predefinidos de filtro** — NT y RTTY usan las mismas anchuras de filtro predefinidas que DIGU y DIGL (100–2000 Hz).
- **Visualización del ancho de filtro** — El indicador de ancho de filtro obtiene su valor a partir del borde superior de la banda pasante, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Silenciador** — El botón **SQL** y el control deslizante de nivel de silenciador están deshabilitados en el modo NT y en el modo RTTY. Si el silenciador estaba activo al cambiar al modo NT o RTTY, AetherSDR lo desactiva automáticamente y lo restaura al volver al modo anterior. Esto coincide con el comportamiento de DIGU y DIGL; el modo CW se maneja de forma diferente porque el equipo de radio gestiona directamente su estado de silenciador. La desactivación del silenciador en RTTY evita el bloqueo de señales FSK débiles que de otro modo serían eliminadas (#2504).

## Activación del modo RADE

A partir de v26.5.1, la lógica de activación y desactivación del modo RADE se ha mejorado para evitar señales de desactivación espurias en ciertos escenarios:

- Al cambiar al modo RADE desde cualquier otro modo, se activa correctamente RADE en el slice actual.
- Al cambiar desde el modo RADE, AetherSDR solo emite una señal de desactivación de RADE si el slice estaba realmente en modo RADE antes del cambio. Esto evita desactivaciones espurias cuando:
  - Se cambia de modo en un slice que no está en RADE.
  - Se reasigna un slice mediante las pestañas de slice.
  - Se cargan perfiles que establecen un modo que no es RADE.
- El comportamiento anterior podía emitir señales de desactivación falsas en configuraciones con múltiples paneles o al cambiar de modo rápidamente, lo cual ha sido resuelto.

## Solución de problemas

- **Un puerto de antena esperado no aparece en el menú** — La lista proviene directamente de la ant_list del equipo de radio. Verifique que el puerto esté configurado y reconocido en los ajustes del propio equipo. AetherSDR no puede añadir puertos que el equipo no haya informado.
- **Al menú de antena TX le falta un puerto que aparece en el menú de antena RX** — Los puertos cuyos nombres comienzan con `RX` se excluyen intencionalmente del menú de antena TX porque el equipo de radio los trata como de solo recepción.
- **Ambas etiquetas están atenuadas o no responden** — AetherSDR no está conectado al equipo de radio. Reconéctese mediante `Settings > Connect to Radio...`.
- **El botón SQL está atenuado después de cambiar al modo NT o RTTY** — NT y RTTY son modos digitales. AetherSDR deshabilita el silenciador en todos los modos digitales (DIGU, DIGL, NT, RTTY) porque el audio se enruta a través de DAX y el silenciador no tiene un efecto significativo. Cambie a un modo no digital para volver a habilitar el silenciador.
- **La fila de pestañas de slice muestra pestañas incorrectas después de reconectar** — En versiones anteriores, la fila de pestañas se construía solo una vez y podía quedar desactualizada tras una reconexión. A partir de v0.9.5.1, AetherSDR reconstruye la fila de pestañas cada vez que cambia el número de slices. Si la fila sigue pareciendo incorrecta, desconecte y reconecte mediante `Settings > Connect to Radio...`.
- **Un valor predefinido de filtro aplica una banda pasante diferente a la esperada** — Los valores predefinidos guardados antes de v0.9.5.1 se almacenan como anchos simples y siguen siendo válidos. Los valores predefinidos guardados desde v0.9.5.1 en adelante pueden almacenar bordes inf:sup exactos. Si un valor predefinido se comporta de forma inesperada, haga clic derecho en el botón de valor predefinido para sobrescribirlo con la banda pasante actual.

## Relacionados

- [Descripción general de Controles de RX](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)

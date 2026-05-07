# Seleccione la antena de RX o TX para este slice

El applet de Controles RX le permite elegir qué puerto de antena utiliza la FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Utilícelo cuando tenga varias antenas conectadas y necesite enrutar un slice específico a un puerto específico.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos de la propia radio. Confirme que sus antenas estén conectadas y reconocidas por la radio antes de cambiar estas configuraciones.

## Pasos

1. Abra el applet Controles RX. Si no está visible, haga clic en el botón de la bandeja **RX** en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A a H) correspondiente al slice que desea cambiar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, por ejemplo **ANT1**). Aparece un menú con todos los puertos de antena disponibles. Haga clic en el puerto que desee. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, por ejemplo **ANT1**). Aparece un menú con los puertos de antena con capacidad TX. Haga clic en el puerto que desee.

## Qué hace cada control

| Control                           | Valor predeterminado | Valores válidos                               |
|-----------------------------------|----------------------|-----------------------------------------------|
| **ANT1** (antena RX, etiqueta azul) | ANT1               | Puertos de antena de ant_list de la radio    |
| **ANT1** (antena TX, etiqueta roja) | ANT1              | Puertos con capacidad TX de ant_list de la radio |
| **Pestañas de slice (A..H)**       | Ninguno             | 1–8 botones (limitado por el máximo de slices del hardware)|
| **Insignia de slice**             | A                   | A/B/C/D/E/F/G/H                              |
| **🔓 / 🔒**                       | 🔓                   | Desbloqueado / Bloqueado                     |
| **Combo de modo**                 | USB                 | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY (+ RADE si HAVE_RADE) |
| **Etiqueta de frecuencia**        | 0.000.000           | 0.001–54.000 MHz (450.000 MHz en XVTR)      |
| **Editor de frecuencia**          | Ninguno             | 0.001–54.000 MHz (450.000 MHz en XVTR)      |
| **STEP**                          | 100 Hz              | Lista de tamaños de paso según el modo       |
| **Preajustes de ancho de filtro** | Ninguno             | Anchuras predefinidas según el modo          |
| **Widget de banda pasante**       | Ninguno             | Arrastre los bordes inferior/superior para ajustar la banda pasante |
| **Modo de tono (FM)**             | Off                 | Off, CTCSS TX                                |
| **Valor de tono CTCSS**           | Ninguno             | 41 tonos estándar EIA/TIA-603 (67.0–254.1 Hz) |
| **Desplazamiento (FM)**           | 0.0 MHz             | 0.0–100.0 MHz (paso 0.1)                    |
| **− (desplazamiento hacia abajo)**| Ninguno             | Alternar                                    |
| **Simplex**                       | Activado            | Alternar                                    |
| **+ (desplazamiento hacia arriba)**| Ninguno            | Alternar                                    |
| **REV**                           | Ninguno             | Alternar                                    |
| **🔊 / 🔇 (silencio)**           | 🔊                   | Sin silenciar / Silenciado                   |
| **Ganancia AF**                   | 70                  | 0–100                                       |
| **Paneo L / R**                   | 50                  | 0–100                                       |
| **SQL**                           | Ninguno             | Alternar                                    |
| **Nivel de squelch**              | 20                  | 0–100                                       |
| **Modo AGC**                      | Med                 | Off, Slow, Med, Fast                        |
| **Umbral AGC**                    | 65                  | 0–100                                       |
| **RIT**                           | Ninguno             | Alternar                                    |
| **RIT 0**                         | Ninguno             | Botón pulsador                              |
| **Desplazamiento RIT**            | +0 Hz               | Paso de 10 Hz                               |
| **XIT**                           | Ninguno             | Alternar                                    |
| **XIT 0**                         | Ninguno             | Botón pulsador                              |
| **Desplazamiento XIT**            | +0 Hz               | Paso de 10 Hz                               |
| **TX (insignia)**                 | Ninguno             | Haga clic para establecer como slice TX     |
| **QSK**                           | Ninguno             | Ámbar cuando el break-in CW está activo (solo lectura) |
| **Ancho de filtro (indicador)**   | 2.7K                | Ancho de banda actual del filtro            |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se filtran del menú de antena TX. Seguirán apareciendo en el menú de antena RX.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.
- Desde la v0.9.3, los botones de pestaña de slice y la insignia de slice usan colores por slice gestionados por SliceColorManager. Estos colores persisten entre sesiones y también se reflejan en los widgets VFO y las barras de medidores. Los colores no son configurables desde la página de controles de antena; se aplican en todo el applet.
- El indicador de ancho de filtro comparte la lógica de formato según el modo con el panel VFO (`RxApplet::formatFilterWidth`), lo que garantiza lecturas coherentes en ambas ubicaciones (#2197).
- El método `stepFilterWidth()` recorre la lista de preajustes de filtro según el modo para que los atajos de teclado de ampliar/reducir produzcan una geometría de bordes correcta según el modo (#2208). Por ejemplo, al ampliar desde un filtro USB de 2.7 kHz, se selecciona el siguiente preajuste más grande (por ejemplo, 2.9 kHz) con la colocación de bordes adecuada para el modo USB en lugar de una banda pasante simétrica.

## Comportamiento de las pestañas de slice

En la v0.9.5.1, la fila de pestañas de slice obtuvo una gestión del ciclo de vida más robusta para solucionar problemas observados en las reconexiones de la radio (#2254).

- Cuando la radio informa un número diferente de slices del que contiene la fila de pestañas actual, AetherSDR destruye todos los botones de pestaña existentes (`clearSliceButtons()`) antes de reconstruir la fila. Anteriormente, la fila solo se construía una vez por sesión.
- `clearSliceButtons()` elimina todos los botones de pestaña generados, oculta la fila de pestañas y restaura la insignia de slice estática. Este es también el estado que se muestra cuando la radio está desconectada.
- La conexión de señal entre el grupo de botones y `sliceActivationRequested` ahora se crea solo una vez por sesión, independientemente de cuántas veces se reconstruya la fila de pestañas. Esto evita la acumulación de controladores de señal duplicados en las reconexiones.

## Formato de almacenamiento de preajustes de filtro

A partir de la v0.9.5.1, los preajustes de filtro guardados al hacer clic derecho en un botón de **Preajustes de ancho de filtro** pueden almacenar un ancho simple o un par de bordes de banda pasante específicos (#2259). Esto coincide con el formato utilizado por VfoWidget.

- Una entrada de **ancho simple** se almacena como un solo entero (por ejemplo, `2700`). Al aplicarla, la radio coloca la banda pasante simétricamente según el modo actual.
- Una entrada de **borde inferior:superior** se almacena como dos enteros separados por dos puntos (por ejemplo, `300:3000`). Al aplicarla, AetherSDR establece los bordes inferior y superior de la banda pasante exactamente como se guardaron.

Ambos formatos pueden coexistir en la misma lista de preajustes para un modo determinado. La clave de configuración es `FilterPresets_<modo>` (por ejemplo, `FilterPresets_USB`). Se muestran hasta seis preajustes en el applet de Controles RX para cada modo.

Si una entrada guardada tiene un formato incorrecto o tiene un borde superior que no supera al borde inferior, AetherSDR omite esa entrada silenciosamente al cargar los preajustes.

## Comportamiento del modo NT

NT es un modo digital añadido en la v0.9.3. Su comportamiento dentro del applet de Controles RX coincide con otros modos digitales (DIGU/DIGL) en los siguientes aspectos:

- **Preajustes de filtro** — NT utiliza las mismas anchuras de filtro predefinidas que DIGU y DIGL (100–2000 Hz).
- **Visualización del ancho de filtro** — El indicador de ancho de filtro obtiene su valor del borde superior de la banda pasante, el mismo cálculo utilizado para los modos USB, DIGU y FDV.
- **Squelch** — El botón **SQL** y el control deslizante de nivel de squelch están deshabilitados en modo NT. Si el squelch estaba activo al cambiar al modo NT, AetherSDR desactiva el squelch automáticamente y lo restaura al volver. Esto coincide con el comportamiento para DIGU y DIGL; el modo CW se maneja de forma diferente porque la radio gestiona su estado de squelch directamente.

## Solución de problemas

- **Un puerto de antena esperado no aparece en el menú** — La lista proviene directamente de ant_list de la radio. Verifique que el puerto esté configurado y reconocido en la configuración de la propia radio. AetherSDR no puede añadir puertos que la radio no haya informado.
- **Al menú de antena TX le falta un puerto que aparece en el menú de antena RX** — Los puertos cuyos nombres comienzan con `RX` se excluyen intencionalmente del menú de antena TX porque la radio los trata como de solo recepción.
- **Ambas etiquetas están atenuadas o no responden** — AetherSDR no está conectado a la radio. Reconéctese mediante `Settings > Connect to Radio...`.
- **El botón SQL está atenuado después de cambiar al modo NT** — NT es un modo digital. AetherSDR deshabilita el squelch en todos los modos digitales (DIGU, DIGL, NT) porque el audio se enruta a través de DAX y el squelch no tiene un efecto significativo. Cambie a un modo no digital para volver a habilitar el squelch.
- **La fila de pestañas de slice muestra pestañas incorrectas después de reconectar** — En versiones anteriores, la fila de pestañas se construía solo una vez y podía quedar desactualizada después de una reconexión. A partir de la v0.9.5.1, AetherSDR reconstruye la fila de pestañas cada vez que cambia el número de slices. Si la fila sigue pareciendo incorrecta, desconéctese y reconéctese mediante `Settings > Connect to Radio...`.
- **Un preajuste de filtro aplica una banda pasante diferente a la esperada** — Los preajustes guardados antes de la v0.9.5.1 se almacenan como anchos simples y siguen siendo válidos. Los preajustes guardados a partir de la v0.9.5.1 pueden almacenar bordes inferior:superior exactos. Si un preajuste se comporta de forma inesperada, haga clic derecho en el botón de preajuste para sobrescribirlo con la banda pasante actual.

## Relacionado

- [Resumen de Controles RX](overview.md)
- [Cambiar entre varios slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)

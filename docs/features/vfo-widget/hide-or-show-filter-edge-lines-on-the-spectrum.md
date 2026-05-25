# Ocultar o mostrar las líneas de borde del filtro en el espectro

El panel VFO le ofrece una alternancia por porción para ocultar o mostrar las líneas verticales que marcan los bordes de la banda pasante del filtro de recepción en la visualización del espectro. Ocultarlas reduce el desorden visual cuando desea una vista del panadapter más limpia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- La porción que desea ajustar debe tener un marcador VFO visible en la visualización del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para la porción objetivo. Se abre el panel VFO anclado al marcador.
2. Localice el botón **Filter edges button** en el panel VFO.
3. Haga clic en **Filter edges button** para desactivar las líneas de borde del filtro. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando vuelva a abrir AetherSDR, la configuración se restaurará al estado en que la dejó para esa porción.

## Qué hace cada control

| Control                          | Predeterminado                                                                                                                          | Configuración persistida                                                                                             |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **Filter edges button**          | Mostrado (bordes visibles)                                                                                                              | `Slice{N}_FilterEdgesHidden`                                                                                        |
| **RX antenna button**            | Abre el menú de selección de antena para la antena receptora de esta porción. El menú utiliza la lista de antenas RX reportada por la radio cuando está disponible. | No se persiste                                                                                                      |
| **TX antenna button**            | Abre el menú de selección de antena para la antena transmisora de esta porción. Omite automáticamente los puertos de antena solo RX (los que comienzan con "RX") e incluye antenas cuyo nombre comienza con "ANT", "TX" o "XVTR" como alternativa. | No se persiste                                                                                                      |
| **Frequency display**            | Muestra la frecuencia actual de la porción. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, los números enteros simples de 4 o más dígitos con la porción en el rango de 100-999 MHz insertan automáticamente un decimal después del tercer dígito (p. ej., 1446 → 144.6). Por encima de 1000 MHz, los números enteros simples se tratan como el valor directo en MHz. Entrada máxima de frecuencia: 50000 MHz. La visualización de frecuencia muestra una superposición "LOCKED" cuando el VFO de la porción está bloqueado. | No se persiste                                                                                                      |
| **Filter width label**           | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. | No se persiste                                                                                                      |
| **AF Gain slider**               | 100                                                                                                                                    | No se persiste — refleja el estado en vivo de la radio.                                                              |
| **Pan slider**                   | 50                                                                                                                                     | No se persiste                                                                                                      |
| **Mute button**                  | off                                                                                                                                    | No se persiste                                                                                                      |
| **Squelch button + slider**      | off                                                                                                                                    | No se persiste                                                                                                      |
| **AGC combo**                    | FAST                                                                                                                                   | No se persiste                                                                                                      |
| **Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | off                                                                                                                     | No se persiste                                                                                                      |
| **ADSP button**                  | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de alternancia de DSP del lado de la radio pero no es marcable. Al hacer clic, eleva y enfoca el diálogo modal de configuración de AetherDSP. |
| **AetherVoice button**           | Alterna la tira de canales de audio de Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                     | Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| **Mode combo**                   | USB                                                                                                                                    | No se persiste                                                                                                      |
| **Filter preset buttons**        | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura.                | `FilterPresets`                                                                                                     |
| **Botones RIT / XIT + etiquetas** | off                                                                                                                                   | No se persiste                                                                                                      |
| **DAX channel combo**            | Off                                                                                                                                    | No se persiste                                                                                                      |
| **Marker thickness button**      | 1 px                                                                                                                                   | `Slice{N}_MarkerWidth`                                                                                              |
| **Collapse toggle**              | expandido                                                                                                                              | `SliceFlagCollapsed_{N}`                                                                                            |

`{N}` es el número de porción. Cada porción almacena su propio valor de forma independiente.

## Consejos

- La configuración es por porción. Ocultar los bordes del filtro en la porción 0 no afecta a la porción 1 ni a ninguna otra porción.
- Si ha contraído el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la tira contraída para acceder al botón **Filter edges button**.
- En v0.9.8, varios botones de reducción de ruido que antes estaban en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han movido fuera del panel VFO. Esos algoritmos ahora se alternan desde el menú de superposición del espectro y el applet AetherDSP. Si no ve un botón que usaba antes, búsquelo allí.
- En v0.9.8, **Filter width label** ahora utiliza `RxApplet::formatFilterWidth` como fuente única de verdad para formatear el ancho de banda del filtro. Esto corrige un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. El ancho de filtro mostrado ahora coincide exactamente con la lectura del filtro del applet RX.
- En v0.9.8, los botones de alternancia DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora empujan y extraen automáticamente la pila de deslizadores compartidos a nivel DSP cuando llegan cambios de estado desde la radio. Esto asegura que el deslizador esté presente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado de la radio.
- En v26.5.1, el squelch está deshabilitado para modos RTTY, además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.
- En v26.5.2.1, los menús de antena RX y TX ahora utilizan la lista de antenas por porción reportada por la radio cuando está disponible. El menú de antena TX filtra automáticamente los puertos de antena solo RX. El máximo de entrada de frecuencia para bandas XVTR se ha incrementado a 50000 MHz. La insignia de porción ahora admite renderizado HTML (#2606).
- En v26.5.3, el panel VFO utiliza un widget `TabStack` personalizado que reporta solo la sugerencia de tamaño de la pestaña actual, evitando un espacio visual al cambiar entre pestañas de diferentes alturas. La visualización de frecuencia muestra una superposición "LOCKED" cuando el VFO de la porción está bloqueado. La entrada directa de frecuencia se cancela cuando la porción se bloquea. El sintonizador de rueda de desplazamiento en un VFO bloqueado ahora notifica al usuario que la sintonización está bloqueada.

## Relacionado

- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- [VFO Panel overview](overview.md)

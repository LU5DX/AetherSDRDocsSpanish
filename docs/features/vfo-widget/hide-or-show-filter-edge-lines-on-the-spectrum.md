# Ocultar o mostrar las líneas de borde del filtro en el espectro

El panel VFO le ofrece una activación por porción para ocultar o mostrar las líneas verticales que marcan los bordes de la banda pasante del filtro de recepción en la visualización del espectro. Ocultarlas reduce el desorden visual cuando desea una vista del panadapter más limpia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- La porción que desea ajustar debe tener un marcador VFO visible en la visualización del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro de la porción objetivo. El panel VFO se abre anclado al marcador.
2. Localice el botón **Filter edges** en el panel VFO.
3. Haga clic en el botón **Filter edges** para desactivar las líneas de borde del filtro. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando vuelva a abrir AetherSDR, la configuración se restaurará al estado en que la dejó para esa porción.

## Qué hace cada control

| Control                      | Predeterminado                                                                                                                              | Configuración persistida                                                                                                |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **Botón Filter edges**       | Mostrado (bordes visibles)                                                                                                                  | `Slice{N}_FilterEdgesHidden`                                                                                            |
| **Botón RX antenna**         | Abre el menú de selección de antena para la antena de recepción de esta porción. El menú usa la lista de antenas RX reportada por la radio cuando está disponible. | No persistida                                                                                                           |
| **Botón TX antenna**         | Abre el menú de selección de antena para la antena de transmisión de esta porción. Omite automáticamente los puertos de antena solo RX (aquellos que comienzan con "RX") e incluye antenas cuyo nombre comienza con "ANT", "TX" o "XVTR" como respaldo. | No persistida                                                                                                           |
| **Indicador de frecuencia**  | Muestra la frecuencia actual de la porción. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, los enteros simples de 4 o más dígitos con la porción en el rango de 100-999 MHz insertan automáticamente un decimal después del tercer dígito (p. ej., 1446 → 144.6). Por encima de 1000 MHz, los enteros simples se tratan como el valor directo en MHz. Entrada máxima de frecuencia: 50000 MHz. El indicador de frecuencia muestra una superposición "LOCKED" cuando el VFO de la porción está bloqueado. | No persistida                                                                                                           |
| **Etiqueta de ancho de filtro** | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. | No persistida                                                                                                           |
| **Deslizador AF Gain**       | 100                                                                                                                                           | No persistida — refleja el estado activo de la radio.                                                                  |
| **Deslizador Pan**           | 50                                                                                                                                            | No persistida                                                                                                           |
| **Botón Mute**               | off                                                                                                                                          | No persistida                                                                                                           |
| **Botón + deslizador Squelch** | off                                                                                                                                          | No persistida                                                                                                           |
| **Combo AGC**                | FAST                                                                                                                                         | No persistida                                                                                                           |
| **Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | off                                                                                                                         | No persistida                                                                                                           |
| **Botón ADSP**               | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de activación DSP del lado de la radio pero no es marcable. Haga clic para abrir y enfocar el cuadro de diálogo no modal de configuración de AetherDSP. |
| **Botón AetherVoice**        | Activa la Aetherial Audio Channel Strip: el conjunto unificado de DSP TX/RX (v0.9.8).                                                          | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.              |
| **Combo Mode**               | USB                                                                                                                                          | No persistida                                                                                                           |
| **Botones de preestablecidos de filtro** | Aplica un preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura.                                     | `FilterPresets`                                                                                                         |
| **Botones + etiquetas RIT / XIT** | off                                                                                                                                        | No persistida                                                                                                           |
| **Combo DAX channel**        | Off                                                                                                                                          | No persistida                                                                                                           |
| **Botón Marker thickness**   | 1 px                                                                                                                                         | `Slice{N}_MarkerWidth`                                                                                                  |
| **Alternar Collapse**        | expandido                                                                                                                                    | `SliceFlagCollapsed_{N}`                                                                                                |

`{N}` es el número de la porción. Cada porción almacena su propio valor de forma independiente.

## Consejos

- La configuración es por porción. Ocultar los bordes del filtro en la porción 0 no afecta a la porción 1 ni a ninguna otra porción.
- Si ha colapsado el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la tira colapsada para acceder al botón **Filter edges**.
- En v0.9.8, varios botones de reducción de ruido que estaban anteriormente en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han eliminado del panel VFO. Esos algoritmos ahora se activan desde el menú superpuesto del espectro y la aplicación AetherDSP. Si no ve un botón que usaba anteriormente, búsquelo allí.
- En v0.9.8, la **etiqueta de ancho de filtro** ahora usa `RxApplet::formatFilterWidth` como fuente única de verdad para formatear el ancho de banda del filtro. Esto corrige un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. El ancho de filtro mostrado ahora coincide exactamente con la lectura del filtro de la aplicación RX.
- En v0.9.8, los botones de activación DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora insertan y extraen automáticamente la pila compartida de deslizadores a nivel DSP cuando llegan cambios de estado desde la radio. Esto asegura que el deslizador esté presente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado de la radio.
- En v26.5.1, el squelch está deshabilitado para los modos RTTY, además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.
- En v26.5.2.1, los menús de antena RX y TX ahora usan la lista de antenas por porción reportada por la radio cuando está disponible. El menú de antena TX filtra automáticamente los puertos de antena solo RX. El máximo de entrada de frecuencia para bandas XVTR se ha aumentado a 50000 MHz. La insignia de la porción ahora admite renderizado HTML (#2606).
- En v26.5.3, el panel VFO usa un widget `TabStack` personalizado que informa solo la sugerencia de tamaño de la pestaña actual, evitando un espacio visual al cambiar entre pestañas de diferentes alturas. El indicador de frecuencia muestra una superposición "LOCKED" cuando el VFO de la porción está bloqueado. La entrada directa de frecuencia se cancela cuando la porción se bloquea. La sintonización con la rueda de desplazamiento en un VFO bloqueado ahora notifica al usuario que la sintonización está bloqueada.
- En v26.6.1, los controles deslizantes del panel VFO (AF Gain, Pan, umbral de squelch) ahora usan tokens de color conscientes del tema para el diseño de su ranura y controlador, asegurando una apariencia consistente con el espectro y otros elementos temáticos. El **deslizador Pan** usa un relleno anclado al centro que se extiende hacia afuera desde el punto medio, con un pequeño punto de marca central para indicar la posición neutral.
- En v26.6.1, al panel VFO se le ha asignado su propio ámbito de contenedor de tematización (`spectrum/vfo`) que hereda las anulaciones del espectro. Esto mejora la cobertura del inspector de temas: al hacer clic en el fondo del panel VFO, la insignia de la porción o el medidor de señal, ahora se muestran los tokens de tema relevantes en el inspector.

## Relacionado

- [Cambiar el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Colapsar el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)

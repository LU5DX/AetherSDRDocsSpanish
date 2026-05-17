# Ocultar o mostrar las líneas de los bordes del filtro en el espectro

El panel VFO le ofrece una opción por segmento para ocultar o mostrar las líneas verticales que marcan los bordes de la banda pasante del filtro de recepción en la visualización del espectro. Ocultarlas reduce el desorden visual cuando desea una vista del panadapter más limpia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El segmento que desea ajustar debe tener un marcador VFO visible en la visualización del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro del segmento objetivo. El panel VFO se abre anclado al marcador.
2. Localice el botón **Filter edges** en el panel VFO.
3. Haga clic en el botón **Filter edges** para desactivar las líneas de los bordes del filtro. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando vuelva a abrir AetherSDR, la configuración se restaura al estado en que la dejó para ese segmento.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                               | Configuración persistente                                                                                             |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Botón Filter edges**       | Mostrado (bordes visibles)                                                                                                          | `Slice{N}_FilterEdgesHidden`                                                                                         |
| **Botón RX antenna**         | Abre el menú de selección de antena para la antena receptora de este segmento. El menú utiliza la lista de antenas RX informada por la radio cuando está disponible. | No se persiste                                                                                                       |
| **Botón TX antenna**         | Abre el menú de selección de antena para la antena transmisora de este segmento. Omite automáticamente los puertos de antena solo RX (los que comienzan con "RX") e incluye como respaldo antenas cuyo nombre comienza con "ANT", "TX" o "XVTR". | No se persiste                                                                                                       |
| **Visualización de frecuencia** | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, los enteros sin decimales de 4 o más dígitos con el segmento en el rango de 100-999 MHz insertan automáticamente un decimal después del tercer dígito (ej., 1446 → 144.6). Por encima de 1000 MHz, los enteros sin decimales se tratan como el valor directo en MHz. Entrada máxima de frecuencia: 50000 MHz. | No se persiste                                                                                                       |
| **Etiqueta de ancho de filtro** | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales. | No se persiste                                                                                                       |
| **Deslizador AF Gain**       | 100                                                                                                                                 | No se persiste; refleja el estado en vivo de la radio.                                                               |
| **Deslizador Pan**           | 50                                                                                                                                  | No se persiste                                                                                                       |
| **Botón Mute**               | desactivado                                                                                                                         | No se persiste                                                                                                       |
| **Botón + deslizador Squelch** | desactivado                                                                                                                       | No se persiste                                                                                                       |
| **Combinación AGC**          | FAST                                                                                                                               | No se persiste                                                                                                       |
| **Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | desactivado                                                                                         | No se persiste                                                                                                       |
| **Botón ADSP**               | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo modal de AetherDSP Settings. |
| **Botón AetherVoice**        | Activa o desactiva la tira de canales de audio de Aetherial (Aetherial Audio Channel Strip): el conjunto unificado de DSP de TX/RX (v0.9.8). | Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| **Combinación Mode**         | USB                                                                                                                                | No se persiste                                                                                                       |
| **Botones de ajustes preestablecidos de filtro** | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. | `FilterPresets`                                                                                                      |
| **Botones RIT / XIT + etiquetas** | desactivado                                                                                                                       | No se persiste                                                                                                       |
| **Combinación DAX channel**  | Off                                                                                                                                | No se persiste                                                                                                       |
| **Botón Marker thickness**   | 1 px                                                                                                                               | `Slice{N}_MarkerWidth`                                                                                               |
| **Conmutador Collapse**      | expandido                                                                                                                          | `SliceFlagCollapsed_{N}`                                                                                             |

`{N}` es el número del segmento. Cada segmento almacena su propio valor de forma independiente.

## Consejos

- La configuración es por segmento. Ocultar los bordes del filtro en el segmento 0 no afecta al segmento 1 ni a ningún otro segmento.
- Si ha contraído el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la tira contraída para acceder al botón **Filter edges**.
- En v0.9.8, varios botones de reducción de ruido que antes estaban en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han movido fuera del panel VFO. Ahora esos algoritmos se activan desde el menú superpuesto del espectro y desde el applet AetherDSP. Si no ve un botón que usaba antes, búsquelo allí.
- En v0.9.8, la **etiqueta de ancho de filtro** ahora utiliza `RxApplet::formatFilterWidth` como fuente única de verdad para formatear el ancho de banda del filtro. Esto corrige un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales. El ancho de filtro mostrado ahora coincide exactamente con la lectura del filtro del applet RX.
- En v0.9.8, los botones de activación DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora insertan y eliminan automáticamente la pila compartida del deslizador de nivel DSP cuando llegan cambios de estado desde la radio. Esto garantiza que el deslizador esté presente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado de la radio.
- En v26.5.1, el squelch está desactivado para modos RTTY, además de los modos digitales y CW. Esto evita que el squelch bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.
- En v26.5.2.1, los menús de antena RX y TX ahora utilizan la lista de antenas por segmento informada por la radio cuando está disponible. El menú de antena TX filtra automáticamente los puertos de antena solo RX. El máximo de entrada de frecuencia para bandas XVTR se ha incrementado a 50000 MHz. La insignia del segmento ahora admite renderizado HTML (#2606).

## Relacionados

- [Cambiar el grosor de la línea del marcador VFO](change-the-vfo-marker-line-thickness.md)
- [Contraer el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)

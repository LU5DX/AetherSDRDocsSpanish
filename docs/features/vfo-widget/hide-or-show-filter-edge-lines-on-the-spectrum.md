# Ocultar o mostrar las líneas de borde del filtro en el espectro

El panel VFO le ofrece una opción por segmento para ocultar o mostrar las líneas verticales que marcan los bordes del ancho de banda del filtro de recepción en la pantalla del espectro. Ocultarlas reduce el desorden visual cuando desea una vista del panadapter más limpia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio.
- El segmento que desea ajustar debe tener un marcador VFO visible en la pantalla del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento deseado. El panel VFO se abre anclado al marcador.
2. Localice el **Filter edges button** en el panel VFO.
3. Haga clic en **Filter edges button** para desactivar las líneas de borde del filtro. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando reinicie AetherSDR, la configuración se restaurará al estado en que la dejó para ese segmento.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                 | Configuración persistente                                                                                                |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **Filter edges button**      | Mostrado (bordes visibles)                                                                                                            | `Slice{N}_FilterEdgesHidden`                                                                                            |
| **RX antenna button**        | Abre el menú de selección de antena para la antena receptora de este segmento.                                                        | No se persiste                                                                                                          |
| **TX antenna button**        | Abre el menú de selección de antena para la antena transmisora de este segmento.                                                      | No se persiste                                                                                                          |
| **Frequency display**        | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba los MHz y presione Enter o Tab. | No se persiste                                                                                                          |
| **Filter width label**       | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preselección de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital. | No se persiste                                                                                                          |
| **AF Gain slider**           | 100                                                                                                                                    | No se persiste — refleja el estado en vivo de la radio.                                                                |
| **Pan slider**               | 50                                                                                                                                     | No se persiste                                                                                                          |
| **Mute button**              | Desactivado                                                                                                                            | No se persiste                                                                                                          |
| **Squelch button + slider**  | Desactivado                                                                                                                            | No se persiste                                                                                                          |
| **AGC combo**                | RÁPIDO                                                                                                                                 | No se persiste                                                                                                          |
| **Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | Desactivados                                                                                                                     | No se persiste                                                                                                          |
| **ADSP button**              | Abre el cuadro de diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal de Configuración de AetherDSP. |
| **AetherVoice button**       | Conmuta la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8).                                              | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada del menú/cadena existentes para el strip. |
| **Mode combo**               | USB                                                                                                                                   | No se persiste                                                                                                          |
| **Filter preset buttons**    | Aplica un valor preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura.   | `FilterPresets`                                                                                                         |
| **Botones + etiquetas RIT / XIT** | Desactivados                                                                                                                       | No se persiste                                                                                                          |
| **DAX channel combo**        | Desactivado                                                                                                                            | No se persiste                                                                                                          |
| **Marker thickness button**  | 1 px                                                                                                                                  | `Slice{N}_MarkerWidth`                                                                                                  |
| **Collapse toggle**          | Expandido                                                                                                                              | `SliceFlagCollapsed_{N}`                                                                                                |

`{N}` es el número del segmento. Cada segmento almacena su propio valor de forma independiente.

## Consejos

- La configuración es por segmento. Ocultar los bordes del filtro en el segmento 0 no afecta al segmento 1 ni a ningún otro segmento.
- Si ha colapsado el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la franja colapsada para acceder al **Filter edges button**.
- En v0.9.8, varios botones de reducción de ruido que estaban anteriormente en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han eliminado del panel VFO. Esos algoritmos ahora se activan desde el menú superpuesto del espectro y desde el applet AetherDSP. Si no ve un botón que usaba anteriormente, búsquelo allí.
- En v0.9.8, el **Filter width label** ahora usa `RxApplet::formatFilterWidth` como única fuente de verdad para formatear el ancho de banda del filtro. Esto corrige un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital. El ancho de filtro mostrado ahora coincide exactamente con la lectura del filtro del applet de RX.
- En v0.9.8, los botones de conmutación DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora colocan y extraen automáticamente la pila compartida del control deslizante de nivel DSP cuando llegan cambios de estado desde la radio. Esto asegura que el control deslizante esté presente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado de la radio.
- En v26.5.1, el squelch está deshabilitado para los modos RTTY además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.

## Relacionado

- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- [VFO Panel overview](overview.md)

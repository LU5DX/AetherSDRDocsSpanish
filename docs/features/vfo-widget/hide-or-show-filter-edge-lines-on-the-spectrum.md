# Ocultar o mostrar líneas de borde de filtro en el espectro

El panel VFO le proporciona una opción por rebanada para ocultar o mostrar las líneas verticales que marcan los bordes de la banda de paso del filtro de recepción en la visualización del espectro. Ocultarlas reduce el desorden visual cuando desea una vista más limpia del panadapter.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- La rebanada que desea ajustar debe tener un marcador VFO visible en la visualización del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para la rebanada objetivo. El panel VFO se abre anclado al marcador.
2. Localice el **Filter edges button** en el panel VFO.
3. Haga clic en **Filter edges button** para alternar las líneas de borde de filtro desactivadas. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando vuelva a abrir AetherSDR, la configuración se restaura al estado en que la dejó para esa rebanada.

## Qué hace cada control

| Control                      | Predeterminado                                                                                                                        | Configuración persistida                                                                                                |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **Filter edges button**      | Mostrado (bordes visibles)                                                                                                            | `Slice{N}_FilterEdgesHidden`                                                                                            |
| ADSP button (pestaña DSP)    | Abre el cuadro de diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo como un conmutador DSP del lado del radio pero no es marcable. Al hacer clic, eleva y enfoca el cuadro de diálogo AetherDSP Settings no modal. |
| AetherVoice button (pestaña DSP) | Alterna el Aetherial Audio Channel Strip: el conjunto unificado de DSP de TX/RX (v0.9.8).                                             | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

`{N}` es el número de rebanada. Cada rebanada almacena su propio valor de forma independiente.

## Consejos

- La configuración es por rebanada. Ocultar los bordes de filtro en la rebanada 0 no afecta a la rebanada 1 ni a ninguna otra rebanada.
- Si ha colapsado el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la tira colapsada para acceder al **Filter edges button**.
- En v0.9.8, varios botones de reducción de ruido que antes estaban en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han movido fuera del panel VFO. Esos algoritmos ahora se activan desde el menú superpuesto del espectro y el applet AetherDSP. Si no ve un botón que usaba anteriormente, búsquelo allí.
- En v0.9.8, la **Filter width label** ahora usa `RxApplet::formatFilterWidth` como la única fuente de verdad para formatear el ancho de banda del filtro. Esto soluciona un desplazamiento de 0.1 kHz que afectaba las lecturas de modo SSB/digital. El ancho de filtro mostrado ahora coincide exactamente con la lectura de filtro del applet RX.
- En v0.9.8, los botones de conmutación DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora insertan y extraen automáticamente la pila de deslizadores compartida del nivel DSP cuando llegan cambios de estado desde el radio. Esto garantiza que el deslizador esté presente al iniciar para cualquier DSP que estuviera habilitado en el perfil guardado del radio.

## Relacionado

- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- [VFO Panel overview](overview.md)

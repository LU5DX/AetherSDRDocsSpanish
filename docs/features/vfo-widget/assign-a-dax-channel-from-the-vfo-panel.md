# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un slice a un canal de audio con nombre en su computadora. Utilice este procedimiento para asignar o cambiar el canal DAX para cualquier slice directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa a la radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del slice de destino debe estar abierto y expandido. Si está contraído a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la visualización del espectro para el slice que desea configurar. Se abre el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canal DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX para este slice, seleccione **Off**.

## Función de cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Combo de canal DAX            | Off                                                                                                                                  | Off, 1–8                                                                                                                   |
| Botón ADSP (pestaña DSP)       | Abre el cuadro de diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, muestra y enfoca el cuadro de diálogo modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP)| Abre la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX (v0.9.8).                                                   | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

El combo de canal DAX asigna un canal de audio DAX al slice actual. Seleccionar un canal numerado enruta el audio recibido del slice a ese canal DAX. Seleccionar **Off** elimina la asignación. Esta configuración refleja el estado en vivo de la radio y AetherSDR no la conserva localmente.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por la radio y dos botones de lanzamiento del lado del cliente.

### Botones DSP del lado de la radio

Los siguientes botones DSP del lado de la radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Eliminador de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones de lanzamiento del lado del cliente

Dos botones de lanzamiento del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el cuadro de diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Tiene el estilo de un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, muestra y enfoca el cuadro de diálogo modal AetherDSP Settings. |
| **AetherVoice** | Conmuta la Aetherial Audio Channel Strip, el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartida aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP con nivel que se activó más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0–100. Cuando no hay ningún DSP con nivel activo — o cuando solo están activos RNN, ANFT o APF — la fila del deslizador está atenuada y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su objetivo.

Algoritmos que admiten el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

A partir de la v0.9.8, cuando un algoritmo DSP con nivel está habilitado desde el perfil guardado de la radio al inicio, el deslizador de nivel se completa automáticamente sin necesidad de una conmutación manual.

### Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de ajustes preestablecidos de filtro en la pestaña Mode. A partir de la v0.9.8, esta etiqueta utiliza `RxApplet::formatFilterWidth` como fuente única de información, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital.

## Consejos

- Cada canal DAX solo se puede asignar a un slice a la vez. Si asigna un canal que ya está en uso por otro slice, la radio moverá la asignación.
- Si el panel VFO quedara recortado por el borde de la ventana, se voltea automáticamente al lado derecho del marcador.
- Para acceder a NR2, RN2, NR4, MNR, BNR o DFNR, haga clic con el botón derecho en la visualización del espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Solución de problemas

- **El combo de canal DAX no tiene efecto / el audio no aparece en el anfitrión** — Confirme que el puente de audio DAX esté en ejecución. Verifique `Settings > Autostart DAX with AetherSDR`. En sistemas macOS y PipeWire, el puente debe estar activo para que los canales DAX aparezcan como dispositivos de audio.
- **La pestaña DAX no es visible** — El panel VFO puede estar contraído. Haga clic en la tira contraída para expandirlo y luego seleccione la pestaña DAX.
- **El deslizador de nivel DSP está atenuado** — No hay ningún algoritmo DSP con nivel activo actualmente, o solo están habilitados RNN, ANFT o APF. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al inicio** — Si un algoritmo DSP con nivel estaba habilitado en el perfil guardado de la radio, el deslizador ahora se completa automáticamente. Si aún parece faltar, desactive y vuelva a activar el algoritmo.

## Relacionado

- [VFO Panel overview](overview.md)
- [Adjust AF gain and pan from the VFO panel](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Mute audio for a slice from the VFO panel](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)

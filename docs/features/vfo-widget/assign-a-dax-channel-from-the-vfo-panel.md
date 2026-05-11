# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un segmento a un canal de audio designado en su computadora. Use este procedimiento para asignar o cambiar el canal DAX de cualquier segmento directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del segmento objetivo debe estar abierto y expandido. Si está colapsado a la franja de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla de espectro del segmento que desea configurar. Se abrirá el panel VFO, anclado al lado izquierdo del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canales DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX de este segmento, seleccione **Off**.

## Función de cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                            |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Combo de canales DAX         | Off                                                                                                                                   | Off, 1–8                                                                                                                    |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilo similar a un conmutador DSP del radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Abre la tira de canales de audio Aetherial — el conjunto unificado de DSP para TX/RX (v0.9.8).                                       | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.                 |

El combo de canales DAX asigna un canal de audio DAX al segmento actual. Seleccionar un canal numerado enruta el audio recibido del segmento a ese canal DAX. Seleccionar **Off** elimina la asignación. Esta configuración refleja el estado en vivo del radio y AetherSDR no la conserva localmente.

## Comportamiento del squelch según el modo

El botón y el deslizador de squelch se deshabilitan automáticamente en modos donde el squelch no es relevante o no es compatible. A partir de v26.5.1:

- **El squelch está deshabilitado** en los modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio alimenta decodificadores externos a través de DAX; el squelch no es relevante y puede bloquear señales FSK débiles (problema #2504).
  - **CW**: El radio bloquea el squelch en un nivel fijo y rechaza cambios.
- Si el squelch estaba activado al cambiar a uno de estos modos, el radio lo desactiva automáticamente. El estado guardado del squelch se conserva y se restaurará si vuelve a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por el radio y dos botones de inicio del lado del cliente.

### Botones DSP del radio

Los siguientes botones DSP del radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones de inicio del lado del cliente

Dos botones de inicio del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Estilo similar a un conmutador DSP del radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| **AetherVoice** | Alterna la tira de canales de audio Aetherial — el conjunto unificado de DSP para TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

### Deslizador de nivel DSP

Una fila compartida de deslizador de nivel aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP con nivel que se haya activado más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es de 0 a 100. Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila del deslizador se atenúa y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su objetivo.

Algoritmos compatibles con el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

A partir de v0.9.8, cuando un algoritmo DSP con nivel está habilitado desde el perfil guardado del radio al iniciar, el deslizador de nivel se completa automáticamente sin necesidad de una activación manual.

### Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones preestablecidos de filtro en la pestaña Mode. A partir de v0.9.8, esta etiqueta usa `RxApplet::formatFilterWidth` como única fuente de información, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital.

## Consejos

- Cada canal DAX solo se puede asignar a un segmento a la vez. Si asigna un canal que ya está en uso por otro segmento, el radio moverá la asignación.
- Si el panel VFO quedara recortado por el borde de la ventana, se voltea automáticamente al lado derecho del marcador.
- Para acceder a NR2, RN2, NR4, MNR, BNR o DFNR, haga clic derecho en la pantalla de espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Solución de problemas

- **El combo de canales DAX no tiene efecto / el audio no aparece en el host** — Confirme que el puente de audio DAX esté en ejecución. Verifique `Settings > Autostart DAX with AetherSDR`. En sistemas macOS y PipeWire, el puente debe estar activo para que los canales DAX aparezcan como dispositivos de audio.
- **La pestaña DAX no es visible** — El panel VFO puede estar colapsado. Haga clic en la franja colapsada para expandirlo y luego seleccione la pestaña DAX.
- **El deslizador de nivel DSP está atenuado** — No hay ningún algoritmo DSP con nivel activo actualmente, o solo RNN, ANFT o APF están habilitados. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al iniciar** — Si un algoritmo DSP con nivel estaba habilitado en el perfil guardado del radio, el deslizador ahora se completa automáticamente. Si aún parece faltar, desactive y vuelva a activar el algoritmo.
- **El botón de squelch está deshabilitado** — Se encuentra en modo Digital, RTTY o CW. El squelch no está disponible en estos modos (digital y RTTY enrutan audio a través de DAX; CW tiene squelch fijo bloqueado por el radio). Cambie a un modo compatible como USB o AM para habilitar los controles de squelch.

## Relacionado

- [VFO Panel overview](overview.md)
- [Adjust AF gain and pan from the VFO panel](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Mute audio for a slice from the VFO panel](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)

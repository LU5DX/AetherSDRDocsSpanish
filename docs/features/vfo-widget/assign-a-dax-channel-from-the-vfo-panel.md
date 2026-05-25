# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un *slice* a un canal de audio con nombre en su computadora. Utilice este procedimiento para asignar o cambiar el canal DAX para cualquier *slice* directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión activa con la radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, actívelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del *slice* destino debe estar abierto y expandido. Si está colapsado a la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla de espectro para el *slice* que desea configurar. Se abrirá el panel VFO, anclado a la izquierda del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canal DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX para este *slice*, seleccione **Off**.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                   | Valores válidos                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Combo de canal DAX           | Off                                                                                                                                    | Off, 1–8                                                                                                                    |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Abre la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

El combo de canal DAX asigna un canal de audio DAX al *slice* actual. Seleccionar un canal numerado enruta el audio recibido del *slice* a ese canal DAX. Seleccionar **Off** elimina la asignación. Esta configuración refleja el estado en vivo de la radio y no es persistida localmente por AetherSDR.

## Comportamiento del squelch por modo

El botón y el deslizador de squelch se deshabilitan automáticamente en modos donde el squelch no es significativo o no es compatible. A partir de v26.5.1:

- **El squelch está deshabilitado** en modos **Digital**, **RTTY** y **CW**.
  - **Digital / RTTY**: El audio alimenta decodificadores externos a través de DAX; el squelch no es significativo y puede bloquear señales FSK débiles (problema #2504).
  - **CW**: La radio bloquea el squelch activado a un nivel fijo y rechaza los cambios.
- Si el squelch estaba activado al cambiar a uno de estos modos, la radio lo desactiva automáticamente. El estado guardado del squelch se conserva y se restaurará si vuelve a un modo compatible.

## Controles de la pestaña DSP

La pestaña DSP en el panel VFO contiene botones de reducción de ruido proporcionados por la radio y dos botones de lanzamiento del lado del cliente.

### Botones DSP del lado de la radio

Los siguientes botones DSP del lado de la radio aparecen en la cuadrícula de la pestaña DSP:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro espectral de ruido |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botones de lanzamiento del lado del cliente

Dos botones de lanzamiento del lado del cliente aparecen al final de la cuadrícula DSP:

| Botón | Comportamiento |
|---|---|
| **ADSP** | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Con estilo de un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| **AetherVoice** | Alterna la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

### Conmutadores de reducción de ruido del lado del cliente

Los siguientes botones de reducción de ruido del lado del cliente aparecen en la pestaña DSP cuando están habilitados por la serie de radio y la compilación:

| Botón | Algoritmo |
|---|---|
| NR2 | Algoritmo de reducción de ruido del lado del cliente 2 |
| NR4 | Algoritmo de reducción de ruido del lado del cliente 4 |
| RN2 | Algoritmo de reducción de ruido del lado del cliente RN2 |
| MNR | Algoritmo de reducción de ruido del lado del cliente MNR |
| DFNR | Algoritmo de reducción de ruido del lado del cliente DFNR |
| BNR | Algoritmo de reducción de ruido del lado del cliente BNR |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro espectral de ruido |

Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.

### Deslizador de nivel DSP

Una fila de deslizador de nivel compartida aparece debajo de la cuadrícula de botones. El deslizador ajusta la intensidad del botón DSP nivelado que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el destino activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

El rango del deslizador es 0–100. Cuando no hay DSP nivelado activo — o solo cuando RNN, ANFT o APF están encendidos — la fila del deslizador está atenuada y no responde a la entrada. La fila permanece en su lugar en todo momento; no desplaza la cuadrícula de botones cuando cambia su destino.

Algoritmos que admiten el deslizador de nivel: NR, NB, ANF, NRL, NRS, NRF, ANFL.

A partir de v0.9.8, cuando un algoritmo DSP nivelado se habilita desde el perfil guardado de la radio al inicio, el deslizador de nivel se completa automáticamente sin necesidad de una activación manual.

### Etiqueta de ancho de filtro

La etiqueta de ancho de filtro muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. A partir de v0.9.8, esta etiqueta utiliza `RxApplet::formatFilterWidth` como la fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital.

### Menús de antena RX y TX

El **botón de antena RX** abre un menú para seleccionar la antena receptora para este *slice*. El **botón de antena TX** abre un menú para seleccionar la antena transmisora. A partir de v26.5.2, estos menús utilizan la lista de antenas proporcionada por la radio para el *slice* cuando está disponible, recurriendo a la lista de antenas global. Las opciones de antena TX excluyen automáticamente los puertos de antena solo RX. Cada elemento del menú muestra su nombre de antena sin procesar como información sobre herramientas (`tooltip`).

### Controles del marcador

El **botón de grosor del marcador** recorre la línea del marcador VFO entre Off, 1 px y 3 px. La configuración se persiste por *slice* como `Slice{N}_MarkerWidth`.

El **botón de bordes de filtro** alterna las líneas de borde del filtro en la banda de paso del espectro. La configuración se persiste por *slice* como `Slice{N}_FilterEdgesHidden`.

### Conmutador de colapso

El **conmutador de colapso** colapsa el panel VFO a una tira compacta de solo frecuencia. La configuración se persiste por *slice* como `SliceFlagCollapsed_{N}`.

### Insignia del slice

La insignia del *slice* muestra la letra del *slice*. A partir de v26.5.2, la insignia admite formato de texto enriquecido, permitiendo caracteres especiales (problema #2606).

### Entrada de frecuencia

Haga clic en la pantalla de frecuencia para iniciar la entrada directa de frecuencia. Escriba la frecuencia en MHz y presione Enter o Tab. A partir de v26.5.2, en bandas XVTR el rango de frecuencia se extiende a 50000.0 MHz. Para bandas de 2m/70cm (rango de 100-999 MHz), un entero simple como 1446 se interpreta automáticamente como 144.6 MHz insertando un decimal después del tercer dígito. Para bandas de 23cm y microondas, un entero simple representa MHz directamente.

A partir de v26.5.3, el análisis de entrada de frecuencia se mejora con un manejo contextual. Cuando ingresa explícitamente una frecuencia superior a 54 MHz (por ejemplo, escribiendo "144.225"), el analizador la trata correctamente como MHz incluso sin un *slice* XVTR, permitiendo la entrada directa de VHF/UHF. La función `FrequencyEntryParser::normalizedMhzText` normaliza formatos de entrada como "14.225.000" eliminando puntos adicionales. La función `FrequencyEntryParser::isExplicitMhzEntry` detecta cuándo ha escrito un valor MHz explícitamente. En bandas XVTR, la convención de banda de 3 dígitos (entero simple como 1446 = 144.6 MHz) sigue funcionando.

Si intenta una entrada de frecuencia directa mientras el VFO está bloqueado, la entrada se cancela y se muestra la superposición LOCKED en lugar de aceptar la nueva frecuencia (problema #2983). La pantalla de frecuencia también indica cuándo la sintonía está bloqueada por el bloqueo. La sintonización con la rueda del ratón en un VFO bloqueado activa la misma retroalimentación — el modelo del *slice* notifica `tuneBlockedByLock`, lo que cancela cualquier entrada de frecuencia en curso y vuelve a pintar el indicador LOCKED.

### Comportamiento del bloqueo VFO

El **botón Lock VFO** alterna el estado de bloqueo del VFO. Cuando está bloqueado:
- La sintonización con la rueda del ratón está bloqueada — el modelo del *slice* muestra retroalimentación a través de `tuneBlockedByLock`.
- La entrada de frecuencia directa se cancela al intentar iniciarla o durante una entrada activa.
- La pantalla de frecuencia muestra una superposición LOCKED (símbolo 🔒) en lugar del valor de frecuencia durante los intentos de entrada directa.

Desbloquear elimina la superposición LOCKED de forma centralizada en el `SliceModel` (problema #2983).

### Mejora en el diseño de pestañas

A partir de v26.5.3, la pila de pestañas del panel VFO utiliza un widget `TabStack` personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un espacio visual dentro de la pestaña Mode cuando la pestaña DSP es más alta (debido a que el `digContainer` es visible en modos DIGU/DIGL). El contenido de la pestaña ya no asigna altura del máximo de todas las páginas.

## Consejos

- Cada canal DAX solo se puede asignar a un *slice* a la vez. Si asigna un canal que ya está en uso por otro *slice*, la radio moverá la asignación.
- Si el panel VFO fuera recortado por el borde de la ventana, se voltea automáticamente al lado derecho del marcador.
- Para acceder a NR2, RN2, NR4, MNR, BNR o DFNR, haga clic derecho en la pantalla de espectro para abrir el menú superpuesto, o abra el applet AetherDSP.

## Solución de problemas

- **El combo de canal DAX no tiene efecto / el audio no aparece en el host** — Confirme que el puente de audio DAX esté en ejecución. Verifique `Settings > Autostart DAX with AetherSDR`. En sistemas macOS y PipeWire, el puente debe estar activo para que los canales DAX aparezcan como dispositivos de audio.
- **La pestaña DAX no es visible** — El panel VFO puede estar colapsado. Haga clic en la tira colapsada para expandirla, luego seleccione la pestaña DAX.
- **El deslizador de nivel DSP está atenuado** — No hay ningún algoritmo DSP nivelado activo actualmente, o solo RNN, ANFT o APF está habilitado. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al inicio** — Si un algoritmo DSP nivelado estaba habilitado en el perfil guardado de la radio, el deslizador ahora se completa automáticamente. Si aún parece faltar, desactive y reactive el algoritmo.
- **El botón de squelch está deshabilitado** — Está en modo Digital, RTTY o CW. El squelch no está disponible en estos modos (digital y RTTY enrutan audio a través de DAX; CW tiene squelch fijo bloqueado por la radio). Cambie a un modo compatible como USB o AM para habilitar los controles de squelch.
- **La entrada de frecuencia no acepta frecuencias VHF/UHF** — A partir de v26.5.3, escriba la frecuencia explícitamente en formato MHz (por ejemplo, "144.225") y el analizador la aceptará incluso sin un *slice* XVTR.
- **El bloqueo VFO impide el cambio de frecuencia** — Cuando está bloqueado, la sintonización con la rueda del ratón y la entrada de frecuencia directa están bloqueadas. Haga clic en el botón Lock VFO para desbloquear el VFO antes de intentar cambiar la frecuencia. La superposición LOCKED desaparecerá al desbloquear.

## Relacionados

- [Vista general del panel VFO](overview.md)
- [Ajustar la ganancia AF y el balance desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)

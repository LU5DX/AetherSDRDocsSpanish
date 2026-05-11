# Sintonice la radio escribiendo una frecuencia en el panel VFO

La entrada directa de frecuencia le permite saltar a una frecuencia exacta sin hacer clic en el panadapter. Escriba un valor en MHz en la pantalla de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO para el slice de destino debe estar abierto. Si no está visible, haga clic en el indicador VFO de ese slice en la pantalla del espectro.

## Pasos

1. Haga clic una vez en la **pantalla de frecuencia**. La pantalla entra en modo de entrada directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicarla. El slice se resintoniza inmediatamente.

## Función de cada control

| Control                      | Comportamiento                                                                                                                                                                                                                         |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Botón de antena RX**       | Abre el menú de selección de antena para la antena receptora de este slice.                                                                                                                                                            |
| **Botón de antena TX**       | Abre el menú de selección de antena para la antena transmisora de este slice.                                                                                                                                                          |
| **Pantalla de frecuencia**   | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa; escriba el valor en MHz y presione Enter o Tab para aplicarlo. Gire la rueda del ratón sobre la pantalla para sintonizar hacia arriba o hacia abajo en incrementos del paso de sintonización actual. |
| **Etiqueta de ancho de filtro** | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Deslizador de ganancia AF (pestaña Audio)** | Establece el nivel de salida de audio para este slice. Valor predeterminado: 100. Rango: 0-100. No se conserva; refleja el estado en vivo de la radio.                                                                                  |
| **Deslizador de paneo (pestaña Audio)** | Establece el paneo estéreo izquierdo/derecho para este slice. Valor predeterminado: 50. Rango: 0-100. 50 = centro.                                                                                                                     |
| **Botón de silencio (pestaña Audio)** | Botón de alternancia. Silencia la salida de audio de este slice sin cambiar la configuración de ganancia AF. Valor predeterminado: desactivado.                                                                                        |
| **Botón + deslizador de squelch (pestaña Audio)** | Botón de alternancia. Activa el squelch para este slice. El deslizador adyacente establece el umbral. Valor predeterminado: desactivado. Rango: 0-100. El squelch está desactivado en modo digital, RTTY y CW.                        |
| **Combo AGC (pestaña Audio)** | Establece la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. Valor predeterminado: FAST.                                                                                                      |
| **Combo de modo (pestaña Mode)** | Establece el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. Valor predeterminado: USB.                                                                                   |
| **Botones de filtro preestablecido (pestaña Mode)** | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se pueden establecer bordes inferior/superior personalizados por ranura mediante clic derecho. Se conserva en `FilterPresets`. |
| **Botones + etiquetas RIT / XIT (pestaña X/RIT)** | Botones de alternancia. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: desactivado.    |
| **Combo de canal DAX (pestaña DAX)** | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. Valor predeterminado: Off.                                                                                                                                             |
| **Botón de grosor del indicador** | Cambia la línea del indicador VFO entre Off, 1 px y 3 px. Se conserva por slice en `Slice{N}_MarkerWidth`.                                                                                                                           |
| **Botón de bordes de filtro** | Botón de alternancia. Alterna la visibilidad de las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice en `Slice{N}_FilterEdgesHidden`. Valor predeterminado: mostrado.                                 |
| **Alternancia de colapso**   | Colapsa el panel VFO a una tira compacta que solo muestra la frecuencia. En modo colapsado, desplazarse sobre cualquier parte de la tira sintoniza según el paso de sintonización actual. Se conserva por slice en `SliceFlagCollapsed_{N}`. |

## Controles de la pestaña DSP

La pestaña DSP contiene botones de alternancia para algoritmos de reducción de ruido y filtrado proporcionados por la radio, además de botones de lanzamiento del lado del cliente. Los siguientes botones están disponibles en la cuadrícula DSP del panel VFO:

| Botón | Descripción |
|---|---|
| **NR** | Reducción de ruido. |
| **NB** | Supresor de ruido. |
| **ANF** | Filtro de muesca automático. |
| **APF** | Filtro de pico de audio. Visible solo cuando el slice está en modo CW. |
| **NRL** | Nivel de reducción de ruido. |
| **NRS** | Sustracción espectral. |
| **RNN** | Reducción de ruido RNN. |
| **NRF** | Filtro de ruido espectral. |
| **ANFL** | Filtro de muesca LMS. |
| **ANFT** | Filtro de muesca FFT. |
| **ADSP** | Botón pulsador. Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú de configuración (v0.9.8). Tiene el estilo de un botón de alternancia DSP del lado de la radio, pero no es seleccionable. |
| **AetherVoice** | Botón pulsador. Alterna la tira de canales de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

Todos los botones DSP del lado de la radio están desactivados de forma predeterminada.

Los módulos de reducción de ruido del lado del cliente (NR2, NR4, MNR, BNR, DFNR y RN2) ya no se muestran en la cuadrícula DSP del panel VFO. Acceda a estos algoritmos desde el menú superpuesto del espectro, el diálogo de configuración de AetherDSP (a través del botón ADSP) o el applet de AetherDSP.

### Deslizador de nivel DSP

Cuando uno o más algoritmos DSP del lado de la radio que admiten un control de nivel están activos, aparece un deslizador de nivel debajo de la cuadrícula de botones DSP. La etiqueta del deslizador muestra el nombre del algoritmo habilitado más recientemente que admite niveles (por ejemplo, **NR**, **NB**, **ANF**, **NRL**, **NRS**, **NRF** o **ANFL**). La lectura numérica adyacente muestra el valor actual.

- Arrastre el deslizador para establecer el nivel del algoritmo seleccionado (0–100).
- El deslizador se reorienta automáticamente cuando habilita un algoritmo de nivel diferente.
- Cuando no hay ningún algoritmo de nivel activo, la fila del deslizador se atenúa, pero permanece en su lugar para que la cuadrícula de botones no se desplace.
- En v0.9.8, el deslizador ahora está presente al inicio para cualquier DSP que se haya guardado como habilitado en el perfil de la radio, sin necesidad de alternarlo manualmente.

### Acciones de clic derecho en botones DSP

Haga clic derecho en cualquiera de los siguientes botones para abrir el diálogo de configuración de AetherDSP para ese algoritmo:
- **NR2**, **NR4**, **MNR**, **DFNR** (accesible a través del botón ADSP)

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Distintivo TX** | TX (rojo), oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| **Distintivo SPLIT** | SPLIT (ámbar), oculto | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |

## Consejos

- Si el panel está colapsado en la tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo y que la **pantalla de frecuencia** sea accesible para la entrada directa.
- La rueda del ratón también sintoniza el slice cuando el puntero está sobre la **pantalla de frecuencia**, avanzando según el paso de sintonización actual del slice. En macOS, los eventos de desplazamiento inercial se ignoran para evitar una sintonización no deseada después de que un gesto termine.

## Solución de problemas

- **Escribir no tiene efecto** — Verifique que el slice no esté bloqueado. Un slice bloqueado ignora los comandos de sintonización. Desbloquéelo antes de ingresar una frecuencia.
- **El panel VFO no está visible** — Haga clic en el indicador VFO del slice deseado en la pantalla del espectro para abrir el panel.
- **Los botones NR2, NR4, MNR, BNR, DFNR o RN2 faltan en la pestaña DSP** — Estos módulos del lado del cliente se movieron fuera del panel VFO en v0.9.7. Actívelos desde el menú superpuesto del espectro, el botón ADSP en la pestaña DSP o el applet de AetherDSP.
- **El deslizador de nivel DSP está atenuado y no responde a los clics** — El deslizador está inactivo cuando ningún algoritmo DSP del lado de la radio que admita niveles está habilitado actualmente. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el deslizador.
- **El deslizador de nivel DSP falta al inicio, aunque un DSP estaba habilitado en el perfil guardado de la radio** — Este problema se solucionó en v0.9.8. Actualice a la última versión.
- **El squelch está desactivado en modo digital, RTTY o CW** — Esto es por diseño. El squelch está desactivado en modo digital y RTTY porque la alimentación de audio llega a decodificadores externos a través de DAX y activar el squelch bloquearía señales FSK débiles. El squelch también está desactivado en modo CW porque la radio bloquea el squelch activado a un nivel fijo y rechaza los cambios del lado del cliente (#2504).

## Relacionados

- [Descripción general del panel VFO](overview.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Cambiar modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Activar el desplazamiento RIT o XIT desde el panel VFO](enable-rit-or-xit-offset-from-the-vfo-panel.md)

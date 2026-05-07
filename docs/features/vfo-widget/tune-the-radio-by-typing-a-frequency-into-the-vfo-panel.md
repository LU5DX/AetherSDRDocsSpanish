# Sintonice la radio escribiendo una frecuencia en el panel VFO

La entrada directa de frecuencia le permite saltar a una frecuencia exacta sin hacer clic en el panadapter. Escriba un valor en MHz en la pantalla de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO para el slice objetivo debe estar abierto. Si no está visible, haga clic en la bandera del marcador VFO de ese slice en la pantalla del espectro.

## Pasos

1. Haga clic una vez en la **Pantalla de frecuencia**. La pantalla entra en modo de entrada directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicar. El slice se resintoniza inmediatamente.

## Función de cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                   |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Botón de antena RX**           | Abre el menú de selección de antena para la antena receptora de este slice.                                                                                                                                                                      |
| **Botón de antena TX**           | Abre el menú de selección de antena para la antena transmisora de este slice.                                                                                                                                                                    |
| **Pantalla de frecuencia**       | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa; escriba MHz y presione Enter o Tab para aplicar. Gire la rueda del ratón sobre la pantalla para sintonizar hacia arriba o abajo según el tamaño de paso actual. |
| **Etiqueta de ancho de filtro**  | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones preestablecidos de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Control deslizante de ganancia AF (pestaña Audio)** | Ajusta el nivel de salida de audio para este slice. Valor predeterminado: 100. Rango: 0-100. No se persiste — refleja el estado en vivo de la radio.                                                                                       |
| **Control deslizante de paneo (pestaña Audio)** | Ajusta el paneo estéreo izquierdo/derecho para este slice. Valor predeterminado: 50. Rango: 0-100. 50 = centro.                                                                                                                                |
| **Botón de silencio (pestaña Audio)** | Botón de alternancia. Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. Valor predeterminado: desactivado.                                                                                                        |
| **Botón y control deslizante de squelch (pestaña Audio)** | Botón de alternancia. Activa el squelch para este slice. El control deslizante adyacente ajusta el umbral. Valor predeterminado: desactivado. Rango: 0-100.                                                                          |
| **Combo AGC (pestaña Audio)**    | Ajusta la velocidad de ataque/liberación del AGC para este slice. Opciones: FAST, MED, SLOW, OFF. Valor predeterminado: FAST.                                                                                                                    |
| **Combo Mode (pestaña Mode)**    | Ajusta el modo de demodulación para este slice. Opciones: USB, LSB, CW, CWL, AM, SAM, DIGU, DIGL, FM, NFM, DFM, RTTY. Valor predeterminado: USB.                                                                                              |
| **Botones preestablecidos de filtro (pestaña Mode)** | Aplica un ancho de filtro preestablecido guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. Se persiste en `FilterPresets`. |
| **Botones y etiquetas RIT / XIT (pestaña X/RIT)** | Botones de alternancia. Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del ratón ajusta en pasos de 10 Hz. Valor predeterminado: desactivado.         |
| **Combo de canal DAX (pestaña DAX)** | Asigna un canal de audio DAX a este slice. Opciones: Off, 1-8. Valor predeterminado: Off.                                                                                                                                                        |
| **Botón de grosor del marcador**| Recorre la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice en `Slice{N}_MarkerWidth`.                                                                                                                                      |
| **Botón de bordes de filtro**    | Botón de alternancia. Alterna las líneas de borde del filtro en la banda pasante del espectro. Se persiste por slice en `Slice{N}_FilterEdgesHidden`. Valor predeterminado: visible.                                                              |
| **Alternancia de colapso**       | Colapsa el panel VFO a una tira compacta solo de frecuencia. En modo colapsado, desplazar el ratón sobre cualquier parte de la tira sintoniza según el tamaño de paso actual. Se persiste por slice en `SliceFlagCollapsed_{N}`.                |

## Controles de la pestaña DSP

La pestaña DSP contiene botones de alternancia para algoritmos de reducción de ruido y filtrado proporcionados por la radio, además de botones iniciadores del lado del cliente. Los siguientes botones están disponibles en la cuadrícula DSP del panel VFO:

| Botón    | Descripción |
|----------|---|
| **NR**   | Reducción de ruido. |
| **NB**   | Eliminador de ruido. |
| **ANF**  | Filtro de muesca automático. |
| **APF**  | Filtro de pico de audio. Visible solo cuando el slice está en modo CW. |
| **NRL**  | Nivel de reducción de ruido. |
| **NRS**  | Sustracción espectral. |
| **RNN**  | Reducción de ruido RNN. |
| **NRF**  | Filtro de ruido espectral. |
| **ANFL** | Filtro de muesca LMS. |
| **ANFT** | Filtro de muesca FFT. |
| **ADSP** | Botón pulsador. Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Diseñado como un botón de alternancia DSP del lado de la radio pero sin posibilidad de selección. |
| **AetherVoice** | Botón pulsador. Alterna la tira de canales de audio de Aetherial — el conjunto DSP unificado TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. |

Todos los botones DSP del lado de la radio están desactivados por defecto.

Los módulos de reducción de ruido del lado del cliente — NR2, NR4, MNR, BNR, DFNR y RN2 — ya no se muestran en la cuadrícula DSP del panel VFO. Acceda a esos algoritmos desde el menú superpuesto del espectro, el diálogo de configuración de AetherDSP (a través del botón ADSP) o el applet de AetherDSP.

### Control deslizante de nivel DSP

Cuando uno o más algoritmos DSP del lado de la radio que admiten un control de nivel están activos, aparece un control deslizante debajo de la cuadrícula de botones DSP. La etiqueta del control deslizante muestra el nombre del algoritmo habilitado más recientemente que admita nivel (por ejemplo, **NR**, **NB**, **ANF**, **NRL**, **NRS**, **NRF** o **ANFL**). La lectura numérica adyacente muestra el valor actual.

- Arrastre el control deslizante para ajustar el nivel del algoritmo objetivo (0–100).
- El control deslizante se reorienta automáticamente cuando activa un algoritmo de nivel diferente.
- Cuando ningún algoritmo de nivel está activo, la fila del control deslizante se atenúa pero permanece en su posición para que la cuadrícula de botones no se desplace.
- En v0.9.8, el control deslizante ahora está presente al inicio para cualquier DSP que se haya guardado como habilitado en el perfil de la radio, sin necesidad de alternancia manual.

### Acciones de clic derecho en botones DSP

Haga clic derecho en cualquiera de los siguientes botones para abrir el diálogo de configuración de AetherDSP para ese algoritmo:
- **NR2**, **NR4**, **MNR**, **DFNR** (accedido a través del botón ADSP)

## Indicadores

| Indicador  | Estados                | Significado                                                                 |
|------------|------------------------|-----------------------------------------------------------------------------|
| **Insignia TX** | TX (rojo), oculto      | Se muestra cuando este slice es el slice transmisor activo.                 |
| **Insignia SPLIT** | SPLIT (ámbar), oculto  | Se muestra cuando TX está asignado a un slice diferente al slice receptor activo. |

## Consejos

- Si el panel está colapsado a la tira solo de frecuencia, haga clic en cualquier parte para expandirlo y que la **Pantalla de frecuencia** sea accesible para la entrada directa.
- La rueda del ratón también sintoniza el slice cuando el puntero está sobre la **Pantalla de frecuencia**, avanzando según el tamaño de paso actual del slice. En macOS, los eventos de desplazamiento inercial se ignoran para evitar una sintonización no deseada después de finalizar un gesto.

## Solución de problemas

- **Escribir no tiene efecto** — Verifique que el slice no esté bloqueado. Un slice bloqueado ignora los comandos de sintonización. Desbloquéelo antes de ingresar una frecuencia.
- **El panel VFO no está visible** — Haga clic en la bandera del marcador VFO para el slice deseado en la pantalla del espectro para abrir el panel.
- **Faltan los botones NR2, NR4, MNR, BNR, DFNR o RN2 en la pestaña DSP** — Estos módulos del lado del cliente se movieron fuera del panel VFO en v0.9.7. Actívelos desde el menú superpuesto del espectro, el botón ADSP en la pestaña DSP o el applet de AetherDSP.
- **El control deslizante de nivel DSP está atenuado y no responde a los clics** — El control deslizante está inactivo cuando ningún algoritmo DSP del lado de la radio que admita nivel está actualmente habilitado. Active NR, NB, ANF, NRL, NRS, NRF o ANFL para activar el control deslizante.
- **El control deslizante de nivel DSP falta al inicio aunque un DSP estaba habilitado en el perfil guardado de la radio** — Este problema se solucionó en v0.9.8. Actualice a la última versión.

## Relacionado

- [Resumen del panel VFO](overview.md)
- [Colapsar el panel VFO a vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Cambiar modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Activar desfase RIT o XIT desde el panel VFO](enable-rit-or-xit-offset-from-the-vfo-panel.md)

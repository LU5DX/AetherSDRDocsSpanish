# Habilitar la reducción de ruido desde el panel VFO

Use la pestaña DSP en el panel VFO para activar uno o más algoritmos de reducción de ruido para una slice. Cada algoritmo está diseñado para un tipo de ruido diferente; puede habilitarlos de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel VFO requiere una conexión de radio activa.
- El panel VFO para la slice debe estar abierto y expandido. Si está colapsado a una tira que solo muestra la frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para la slice que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **DSP** dentro del panel VFO.
3. Haga clic en el botón del algoritmo de reducción de ruido que desea habilitar: **NR**, **NR2**, **RN2**, **NR4**, **MNR**, **DFNR**, **BNR**, **NRL**, **NRS**, **RNN**, **NRF**. El botón se resalta cuando está activo.
4. Para deshabilitar la reducción de ruido, haga clic en el mismo botón nuevamente. El resaltado desaparece.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---------|---------------------|----------------|
| **NR** | desactivado | Habilita el algoritmo estándar de reducción de ruido para esta slice. |
| **NR2** | desactivado | Habilita el algoritmo de reducción de ruido NR2 para esta slice. Haga clic derecho para abrir el cuadro de diálogo de configuración de AetherDSP para este algoritmo. |
| **RN2** | desactivado | Habilita el algoritmo de reducción de ruido RN2 para esta slice. |
| **NR4** | desactivado | Habilita el algoritmo de reducción de ruido NR4 para esta slice. Haga clic derecho para abrir el cuadro de diálogo de configuración de AetherDSP para este algoritmo. |
| **MNR** | desactivado | Habilita el algoritmo de reducción de ruido MNR para esta slice. Haga clic derecho para abrir el cuadro de diálogo de configuración de AetherDSP para este algoritmo. |
| **DFNR** | desactivado | Habilita el algoritmo de reducción de ruido DFNR para esta slice. Haga clic derecho para abrir el cuadro de diálogo de configuración de AetherDSP para este algoritmo. |
| **BNR** | desactivado | Habilita el algoritmo de reducción de ruido BNR para esta slice. |
| **NRL** | desactivado | Habilita el algoritmo de reducción de ruido NRL para esta slice. |
| **NRS** | desactivado | Habilita la sustracción espectral para esta slice. |
| **RNN** | desactivado | Habilita el algoritmo de reducción de ruido RNN para esta slice. |
| **NRF** | desactivado | Habilita el filtro de ruido espectral para esta slice. |
| Botón **ADSP** (pestaña DSP) | N/A | Abre el cuadro de diálogo de configuración de AetherDSP (NR2/NR4/DFNR/RN2/BNR/MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Tiene el estilo de un conmutador DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo de configuración de AetherDSP no modal. |
| Botón **AetherVoice** (pestaña DSP) | N/A | Alterna la tira de canales de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

La disponibilidad de los botones depende de la serie de la radio y la compilación.

## Control deslizante de nivel DSP

Cuando uno o más algoritmos DSP con nivel están activos, aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones. La etiqueta del control deslizante muestra a qué algoritmo apunta actualmente: se reasigna automáticamente al algoritmo con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del control deslizante.

El control deslizante siempre está presente en el diseño. Cuando no hay ningún algoritmo con nivel activo (o solo RNN o APF están encendidos), la fila del control deslizante se atenúa y no responde a la entrada.

El estado del control deslizante se gestiona correctamente al iniciar: si un algoritmo DSP con nivel se guardó en el perfil de la radio y está activo cuando se abre el panel VFO, el control deslizante aparece inmediatamente sin necesidad de alternar manualmente el algoritmo.

| Algoritmos que exponen el control deslizante de nivel |
|---|
| NR, NRL, NRS, NRF |

## Notas sobre el squelch

El squelch está deshabilitado (el botón y el control deslizante dejan de funcionar) cuando la slice está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

En modos digitales y RTTY, el squelch no tiene sentido porque el audio alimenta decodificadores externos a través de DAX. Además, el squelch puede bloquear señales FSK débiles (#2504). En modos CW, la radio bloquea el squelch activado a un nivel fijo y rechaza los cambios.

Si el squelch estaba activo al cambiar a uno de estos modos, se desactiva automáticamente. El estado guardado se restaura al cambiar de nuevo a un modo compatible.

## Consejos

- Pueden activarse varios botones de reducción de ruido al mismo tiempo.
- Puede abrir el applet de AetherDSP desde `Settings > AetherDSP Settings...` para configurar los algoritmos de reducción de ruido del lado del cliente.

## Relacionados

- [Descripción general del panel VFO](overview.md)
- [Habilitar el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)

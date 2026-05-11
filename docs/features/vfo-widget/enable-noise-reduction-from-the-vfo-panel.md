# Habilitar la reducción de ruido desde el panel VFO

Use la pestaña DSP en el panel VFO para activar uno o más algoritmos de reducción de ruido para un slice. Cada algoritmo está diseñado para un tipo de ruido diferente; puede habilitarlos de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice debe estar abierto y expandido. Si está contraído a una franja de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO en la pantalla de espectro para el slice que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **DSP** dentro del panel VFO.
3. Haga clic en el botón del algoritmo de reducción de ruido que desea habilitar: **NR**, **NB**, **ANF**, **NRL**, **NRS**, **RNN**, **NRF**, **ANFL** o **ANFT**. El botón se resalta cuando está activo.
4. Para deshabilitar la reducción de ruido, haga clic en el mismo botón nuevamente. El resaltado desaparece.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                | Comportamiento                                                                                                                 |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **NR**                       | apagado                                                                                                                              | Habilita el algoritmo estándar de reducción de ruido para este slice.                                                         |
| **NB**                       | apagado                                                                                                                              | Habilita el supresor de ruido impulsivo (noise blanker) para este slice.                                                      |
| **ANF**                      | apagado                                                                                                                              | Habilita el filtro de muesca automático (automatic notch filter) para este slice.                                              |
| **NRL**                      | apagado                                                                                                                              | Habilita el algoritmo de reducción de ruido NRL para este slice.                                                              |
| **NRS**                      | apagado                                                                                                                              | Habilita la sustracción espectral para este slice.                                                                            |
| **RNN**                      | apagado                                                                                                                              | Habilita el algoritmo de reducción de ruido RNN para este slice.                                                              |
| **NRF**                      | apagado                                                                                                                              | Habilita el filtro de ruido espectral para este slice.                                                                        |
| **ANFL**                     | apagado                                                                                                                              | Habilita el filtro de muesca LMS para este slice.                                                                             |
| **ANFT**                     | apagado                                                                                                                              | Habilita el filtro de muesca FFT para este slice.                                                                             |
| Botón **ADSP** (pestaña DSP) | N/A                                                                                                                                  | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Diseñado como un conmutador DSP del lado del radio pero no marcable. Haga clic para abrir y enfocar el diálogo no modal AetherDSP Settings. |
| Botón **AetherVoice** (pestaña DSP) | N/A                                                                                                                          | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

El botón **APF** también está presente, pero solo es visible cuando el slice está en modo CW.

## Control deslizante de nivel DSP

Cuando uno o más algoritmos DSP con nivel están activos, aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones. La etiqueta del control deslizante muestra a qué algoritmo se dirige actualmente: se reasigna automáticamente al algoritmo con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del control deslizante.

El control deslizante siempre está presente en el diseño. Cuando ningún algoritmo con nivel está activo (o solo RNN, ANFT o APF están encendidos), la fila del control deslizante se atenúa y no responde a la entrada.

El estado del control deslizante se gestiona correctamente al inicio: si un algoritmo DSP con nivel se guardó en el perfil del radio y está activo cuando se abre el panel VFO, el control deslizante aparece inmediatamente sin necesidad de alternar manualmente el algoritmo.

| Algoritmos que exponen el control deslizante de nivel |
|---|
| NR, NB, ANF, NRL, NRS, NRF, ANFL |

## Algoritmos de reducción de ruido del lado del cliente

Los algoritmos **NR2**, **RN2**, **NR4**, **MNR**, **BNR** y **DFNR** ya no están en la pestaña DSP del panel VFO. Estos módulos de procesamiento del lado del cliente están disponibles desde el menú superpuesto del espectro y desde el applet AetherDSP. Acceda a ellos allí para mantener el panel VFO centrado en el DSP proporcionado por el radio.

## Notas sobre el squelch

El squelch está deshabilitado (el botón y el control deslizante no funcionan) cuando el slice está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

En modos digitales y RTTY, el squelch no tiene sentido porque el audio se envía a decodificadores externos a través de DAX. Además, el squelch puede bloquear señales FSK débiles (#2504). En modos CW, el radio bloquea el squelch encendido a un nivel fijo y rechaza los cambios.

Si el squelch estaba activo al cambiar a uno de estos modos, se apaga automáticamente. El estado guardado se restaura al volver a un modo compatible.

## Consejos

- Pueden estar activos varios botones de reducción de ruido al mismo tiempo.
- Puede abrir el applet AetherDSP desde `Settings > AetherDSP Settings...` para configurar algoritmos de reducción de ruido del lado del cliente.

## Relacionados

- [Descripción general del panel VFO](overview.md)
- [Habilitar el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)

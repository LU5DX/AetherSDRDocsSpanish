# Activar la reducción de ruido desde el panel del VFO

Use la pestaña **DSP** en el panel del VFO para activar uno o más algoritmos de reducción de ruido para un slice. Cada algoritmo está diseñado para un tipo de ruido diferente; puede activarlos de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel del VFO requiere una conexión activa con la radio.
- El panel del VFO para el slice debe estar abierto y expandido. Si está colapsado a una barra que solo muestra la frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora del VFO en el visualizador del espectro para el slice que desea ajustar. El panel del VFO se abre anclado al marcador.
2. Haga clic en la pestaña **DSP** dentro del panel del VFO.
3. Haga clic en el botón del algoritmo de reducción de ruido que desea activar: **NR**, **NB**, **ANF**, **NRL**, **NRS**, **RNN**, **NRF**, **ANFL** o **ANFT**. El botón se resalta cuando está activo.
4. Para desactivar la reducción de ruido, haga clic en el mismo botón nuevamente. El resaltado desaparece.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                  | Comportamiento                                                                                                            |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| **NR**                       | desactivado                                                                                                                           | Activa el algoritmo estándar de reducción de ruido para este slice.                                                       |
| **NB**                       | desactivado                                                                                                                           | Activa el supresor de ruido (noise blanker) para este slice.                                                              |
| **ANF**                      | desactivado                                                                                                                           | Activa el filtro de muesca (notch) automático para este slice.                                                            |
| **NRL**                      | desactivado                                                                                                                           | Activa el algoritmo de reducción de ruido NRL para este slice.                                                            |
| **NRS**                      | desactivado                                                                                                                           | Activa la sustracción espectral para este slice.                                                                          |
| **RNN**                      | desactivado                                                                                                                           | Activa el algoritmo de reducción de ruido RNN para este slice.                                                            |
| **NRF**                      | desactivado                                                                                                                           | Activa el filtro de ruido espectral para este slice.                                                                      |
| **ANFL**                     | desactivado                                                                                                                           | Activa el filtro de muesca LMS para este slice.                                                                           |
| **ANFT**                     | desactivado                                                                                                                           | Activa el filtro de muesca FFT para este slice.                                                                           |
| Botón **ADSP** (pestaña DSP) | N/A                                                                                                                                   | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Ajustes (v0.9.8). Tiene el estilo de un conmutador DSP del lado de la radio, pero no se puede marcar. Al hacer clic, abre y enfoca el diálogo no modal de AetherDSP Settings. |
| Botón **AetherVoice** (pestaña DSP) | N/A                                                                                                                               | Alterna el Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para el strip. |

El botón **APF** también está presente, pero solo es visible cuando el slice está en modo CW.

## Control deslizante de nivel DSP

Cuando uno o más algoritmos DSP con nivel están activos, aparece un control deslizante de nivel compartido debajo de la cuadrícula de botones. La etiqueta del control deslizante indica a qué algoritmo apunta actualmente; se reorienta automáticamente al algoritmo con nivel activado más recientemente. El valor numérico se muestra a la derecha del control deslizante.

El control deslizante siempre está presente en el diseño. Cuando no hay ningún algoritmo con nivel activo (o solo están activos RNN, ANFT o APF), la fila del control deslizante se atenúa y no responde a la entrada.

El estado del control deslizante se gestiona correctamente al inicio: si un algoritmo DSP con nivel se guardó en el perfil de la radio y está activo cuando se abre el panel del VFO, el control deslizante aparece inmediatamente sin necesidad de activar o desactivar manualmente el algoritmo.

| Algoritmos que exponen el control deslizante de nivel |
|---|
| NR, NB, ANF, NRL, NRS, NRF, ANFL |

## Algoritmos de reducción de ruido del lado del cliente

Los algoritmos **NR2**, **RN2**, **NR4**, **MNR**, **BNR** y **DFNR** ya no están en la pestaña DSP del panel del VFO. Estos módulos de procesamiento del lado del cliente están disponibles desde el menú superpuesto del espectro y desde el applet AetherDSP. Acceda a ellos allí para mantener el panel del VFO centrado en el DSP proporcionado por la radio.

## Consejos

- Varios botones de reducción de ruido pueden estar activos al mismo tiempo.
- Puede abrir el applet AetherDSP desde `Settings > AetherDSP Settings...` para configurar los algoritmos de reducción de ruido del lado del cliente.

## Relacionados

- [VFO Panel overview](overview.md)
- [Enable squelch from the VFO panel](enable-squelch-from-the-vfo-panel.md)

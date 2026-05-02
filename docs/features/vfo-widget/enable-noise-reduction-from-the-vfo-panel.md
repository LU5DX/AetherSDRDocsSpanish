# Activar la reducción de ruido desde el panel VFO

Use la pestaña **DSP** del panel VFO para activar uno o más algoritmos de reducción de ruido en un slice (receptor independiente). Cada algoritmo está orientado a un tipo de ruido diferente; puede habilitarlos de forma independiente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice debe estar abierto y expandido. Si está contraído y muestra solo la frecuencia, haga clic en cualquier parte del panel para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora del VFO en el display del espectro correspondiente al slice que desea ajustar. El panel VFO se abre anclado al marcador.
2. Haga clic en la pestaña **DSP** dentro del panel VFO.
3. Haga clic en el botón del algoritmo de reducción de ruido que desea activar: **NR**, **NR2**, **RN2**, **NR4**, **MNR**, **DFNR**, **BNR**, **NRL**, **NRS**, **RNN** o **NRF**. El botón se resalta cuando está activo.
4. Para desactivar la reducción de ruido, haga clic en el mismo botón nuevamente. El resaltado desaparece.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **NR** | desactivado | Activa el algoritmo estándar de reducción de ruido para este slice. |
| **NR2** | desactivado | Activa el algoritmo de reducción de ruido NR2. Haga clic derecho para abrir AetherDSP Settings para NR2. |
| **RN2** | desactivado | Activa el algoritmo de reducción de ruido RN2. |
| **NR4** | desactivado | Activa el algoritmo de reducción de ruido NR4. Haga clic derecho para abrir AetherDSP Settings para NR4. |
| **MNR** | desactivado | Activa el algoritmo de reducción de ruido MNR. Haga clic derecho para abrir AetherDSP Settings para MNR. |
| **DFNR** | desactivado | Activa el algoritmo de reducción de ruido DFNR. Haga clic derecho para abrir AetherDSP Settings para DFNR. |
| **BNR** | desactivado | Activa el algoritmo de reducción de ruido BNR. |
| **NRL** | desactivado | Activa el algoritmo de reducción de ruido NRL. |
| **NRS** | desactivado | Activa el algoritmo de reducción de ruido NRS. |
| **RNN** | desactivado | Activa el algoritmo de reducción de ruido RNN. |
| **NRF** | desactivado | Activa el algoritmo de reducción de ruido NRF. |

Es posible que no todos los botones estén disponibles; la disponibilidad depende de la serie del radio y la versión de compilación.

## Consejos

- Al hacer clic derecho en **NR2**, **NR4**, **MNR** o **DFNR** se abre el diálogo AetherDSP Settings, donde puede ajustar parámetros avanzados de ese algoritmo. También puede abrir este diálogo desde `Settings > AetherDSP Settings...`.
- Pueden estar activos varios botones de reducción de ruido al mismo tiempo.

## Relacionados

- [Descripción general del panel VFO](overview.md)
- [Activar el silenciador (squelch) desde el panel VFO](enable-squelch-from-the-vfo-panel.md)

# Eliminar todos los spots y marcadores del historial de señales del panadapter

Elimine todos los spots de DX, marcadores de memoria, marcadores de voz del historial de señales y marcadores de interferencia QRM de la visualización del espectro en una sola acción.

## Antes de comenzar

- Abra el cuadro de diálogo SpotHub: `Settings > SpotHub...`

## Pasos

1. Haga clic en la pestaña **Display**.
2. Haga clic en **Clear All**.

Todos los spots de cualquier fuente (DX cluster, RBN, WSJT-X, SpotCollector, POTA, FreeDV), superposiciones de canales de memoria y marcadores del historial de señales (tanto marcadores de voz dorados como marcadores QRM rojos) desaparecen del panadapter.

## Consejos

- **Clear All** es una acción no destructiva: solo elimina las superposiciones de marcadores actuales del espectro. Las fuentes de spots conectadas (cluster, RBN, etc.) continúan funcionando y volverán a poblar el panadapter a medida que lleguen nuevos spots.
- Para evitar que los spots reaparezcan, cambie el botón de alternancia maestro **Spots:** a "Disabled" en la pestaña **Display**, o desconecte cada fuente en su pestaña respectiva.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Start WSJT-X UDP listener and filter for CQ, POTA or calls to me](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Connect to a DX cluster](../../getting-started/setup/connect-to-a-dx-cluster.md)
- Editar comandos de inicio para conexiones DX cluster y RBN

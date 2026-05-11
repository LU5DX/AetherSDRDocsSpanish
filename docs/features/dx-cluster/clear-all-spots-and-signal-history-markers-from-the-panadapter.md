# Eliminar todos los puntos y marcadores del historial de señales del panadapter

Elimine todos los puntos DX, marcadores de memoria, marcadores de voz del Historial de Señales y marcadores de interferencia QRM del visualizador de espectro en una sola acción.

## Antes de comenzar

- Abra el diálogo SpotHub: `Settings > SpotHub...`

## Pasos

1. Haga clic en la pestaña **Display**.
2. Haga clic en **Clear All**.

Todos los puntos de cada fuente (DX cluster, RBN, WSJT-X, SpotCollector, POTA, FreeDV), superposiciones de canales de memoria y marcadores del Historial de Señales (marcadores de voz dorados y marcadores QRM rojos) desaparecen del panadapter.

## Consejos

- **Clear All** es una acción no destructiva: solo elimina las superposiciones de marcadores actuales del espectro. Las fuentes de puntos conectadas (cluster, RBN, etc.) continúan funcionando y repoblarán el panadapter a medida que lleguen nuevos puntos.
- Para evitar que los puntos vuelvan a aparecer, cambie el botón maestro **Spots:** a "Disabled" en la pestaña **Display**, o desconecte cada fuente en su respectiva pestaña.

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [Start WSJT-X UDP listener and filter for CQ, POTA or calls to me](start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Connect to a DX cluster](../../getting-started/setup/connect-to-a-dx-cluster.md)

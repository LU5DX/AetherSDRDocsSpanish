# Descripción general del sintonizador

El applet Sintonizador le brinda control en tiempo real de un acoplador de antena externo 4O3A Tuner Genius XL (TGXL) directamente desde AetherSDR. Desde un solo panel puede leer la potencia directa y la ROE, iniciar un sintonizado automático, ajustar los bancos de relés, configurar el estado operativo del acoplador y — cuando hay un conmutador de antena TGXL 3x1 conectado — seleccionar entre tres puertos de antena.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL. El applet permanece oculto hasta que se encuentre el TGXL.
- AetherSDR debe estar conectado a la radio.

## Cómo funciona

El applet Sintonizador aparece en el panel de applets del lado derecho una vez que se detecta un TGXL. Alterne su visibilidad con el botón **TUN** en la barra de bandeja derecha.

El applet está dividido en tres áreas:

**Medidores (superior)** — Dos indicadores horizontales muestran lecturas en vivo del TGXL. Cada indicador tiene una etiqueta de fila externa a la izquierda (PWR, SWR) que muestra el valor en vivo. Cuando la potencia cae por debajo del umbral, la etiqueta se limpia después de 800 ms para evitar parpadeos por ruido entre paquetes.

**Barras de relés y botones (medio)** — Tres barras de posición de relés (C1, L, C2) están a la izquierda; los botones TUNE y OPERATE/BYPASS/STANDBY están a la derecha.

**Fila del conmutador de antena (inferior)** — Tres botones de selección de antena aparecen solo cuando hay una conexión directa TGXL activa y el TGXL informa que hay un conmutador de antena presente. La fila está oculta en caso contrario.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango / estados válidos |
|---|---|---|---|
| **PWR** | Medidor (etiqueta externa) | Muestra la potencia directa reportada por el TGXL. La etiqueta externa muestra el valor en vivo. La etiqueta se limpia después de 800 ms cuando la potencia cae por debajo del umbral para evitar parpadeos. La escala se ajusta automáticamente según se detecte un amplificador PGXL o Aurora. | 0–200 W (sin amplificador); 0–600 W (Aurora); 0–2000 W (con PGXL) |
| **SWR** | Medidor (etiqueta externa) | Muestra la ROE reportada por el TGXL. La etiqueta externa muestra el valor en vivo. La etiqueta se limpia después de 800 ms cuando la ROE cae por debajo del umbral para evitar parpadeos. El indicador se vuelve rojo por encima de 2.5, amarillo por encima de 2.0. | 1.0–3.0 |
| **C1** | Barra de relé | Muestra la posición del banco de relés C1. La rueda del mouse ajusta el relé cuando hay una conexión directa TGXL activa. | 0–255 |
| **L** | Barra de relé | Muestra la posición del banco de relés L. La rueda del mouse ajusta el relé cuando hay una conexión directa TGXL activa. | 0–255 |
| **C2** | Barra de relé | Muestra la posición del banco de relés C2. La rueda del mouse ajusta el relé cuando hay una conexión directa TGXL activa. | 0–255 |
| **TUNE** | Botón | Inicia un sintonizado automático. El botón se vuelve rojo y muestra **TUNING...** mientras el sintonizado está en progreso. Cuando finaliza, el botón muestra brevemente **SWR x.xx** (la ROE estabilizada posterior al sintonizado) durante 2.5 segundos, luego vuelve a **TUNE**. Cuando hay una conexión directa TGXL (puerto 9010) configurada, envía el comando nativo 'autotune' directamente al TGXL en lugar de enrutarlo a través del firmware de la radio. Vuelve a la ruta de la radio cuando no hay conexión directa disponible. Configure la conexión directa en Radio Setup → Tuner. | — |
| **OPERATE** / **BYPASS** / **STANDBY** | Botón | Cicla el estado del relé del TGXL: OPERATE → BYPASS → STANDBY → OPERATE. La etiqueta y el color reflejan el estado actual: **OPERATE** (verde), **BYPASS** (naranja), **STANDBY** (predeterminado). | — |
| **ANT 1** | Botón | Selecciona el puerto de antena 1 en el conmutador TGXL 3x1. Visible solo cuando hay una conexión directa TGXL activa y hay un conmutador de antena presente. | — |
| **ANT 2** | Botón | Selecciona el puerto de antena 2 en el conmutador TGXL 3x1. | — |
| **ANT 3** | Botón | Selecciona el puerto de antena 3 en el conmutador TGXL 3x1. | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Etiqueta PWR** | Valor en vivo / se limpia a "PWR" | Muestra la potencia directa reportada por el TGXL. Se limpia después de 800 ms cuando la potencia cae por debajo del umbral para evitar parpadeos por ruido entre paquetes. |
| **Etiqueta SWR** | Valor en vivo / se limpia a "SWR" | Muestra la ROE reportada por el TGXL. Se limpia después de 800 ms cuando la ROE cae por debajo del umbral para evitar parpadeos por ruido entre paquetes. |
| **Botón TUNE** | TUNE / TUNING... / SWR x.xx | Inactivo / sintonizado en progreso / ROE posterior al sintonizado capturada (parpadea durante 2.5 s). |
| **Botón OPERATE** | OPERATE (verde) / BYPASS (naranja) / STANDBY (predeterminado) | Estado del relé/derivación del TGXL. |
| **Indicador de potencia directa** | Barra con retención de pico | La marca blanca muestra la potencia directa pico. Se limpia después de 2.5 segundos sin nuevos picos. El indicador se vuelve amarillo a 80 W (sin amplificador), 400 W (Aurora) o 1000 W (PGXL). Se vuelve rojo a 125 W (sin amplificador), 500 W (Aurora) o 1500 W (PGXL). |

## Consejos

- La rueda del mouse en C1, L y C2 solo está habilitada cuando hay una conexión directa TGXL activa. Si el desplazamiento no tiene efecto, verifique el estado de la conexión.
- La ROE posterior al sintonizado mostrada en el botón **TUNE** refleja el valor estabilizado final después de una breve ventana de captura, no la ROE medida durante el barrido.
- La escala del indicador de potencia directa se ajusta automáticamente. No se requiere configuración manual al cambiar entre configuraciones sin amplificador, Aurora y PGXL.
- El indicador de potencia directa tiene balística: la barra sube rápidamente en ráfagas de RF pero decae durante aproximadamente 800 ms para un efecto visual suave.
- La marca blanca de retención de pico en el indicador de potencia directa se limpia automáticamente después de 2.5 segundos sin nuevos picos.

## Relacionado

- [Ejecutar un sintonizado automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del mouse](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Conmutar entre tres antenas en un TGXL 3x1](switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Leer la ROE inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)

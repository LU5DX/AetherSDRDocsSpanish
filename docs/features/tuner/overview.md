# Descripción general del sintonizador

El applet Tuner le brinda control en tiempo real sobre un sintonizador de antena externo 4O3A Tuner Genius XL (TGXL) directamente desde AetherSDR. Desde un único panel puede leer la potencia directa y el ROS, activar un autotune, ajustar los bancos de relés, establecer el estado operativo del sintonizador y — cuando hay conectado un conmutador de antenas TGXL 3x1 — seleccionar entre tres puertos de antena.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL. El applet permanece oculto hasta que el TGXL sea encontrado.
- AetherSDR debe estar conectado al radio.

## Cómo funciona

El applet Tuner aparece en el panel de applets del lado derecho una vez que se detecta un TGXL. Alterne su visibilidad con el botón **TUN** de la barra lateral derecha.

El applet está dividido en tres áreas:

**Medidores (parte superior)** — Dos indicadores horizontales muestran lecturas en tiempo real del TGXL.

**Barras de relés y botones (parte central)** — Tres barras de posición de relés (C1, L, C2) se ubican a la izquierda; los botones TUNE y OPERATE/BYPASS/STANDBY se ubican a la derecha.

**Fila del conmutador de antenas (parte inferior)** — Tres botones de selección de antena aparecen únicamente cuando hay una conexión directa con el TGXL activa y el TGXL indica que hay un conmutador de antenas presente. La fila permanece oculta en caso contrario.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango / estados válidos |
|---|---|---|---|
| **Fwd Pwr** | Medidor | Muestra la potencia directa reportada por el TGXL. La escala se ajusta automáticamente según si se detecta un amplificador PGXL o Aurora. | 0–200 W (sin amplificador); 0–600 W (Aurora); 0–2000 W (con PGXL) |
| **SWR** | Medidor | Muestra el ROS reportado por el TGXL. El indicador se vuelve rojo por encima de 2.5. | 1.0–3.0 |
| **C1** | Barra de relé | Muestra la posición del banco de relés C1. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa con el TGXL activa. | 0–255 |
| **L** | Barra de relé | Muestra la posición del banco de relés L. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa con el TGXL activa. | 0–255 |
| **C2** | Barra de relé | Muestra la posición del banco de relés C2. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa con el TGXL activa. | 0–255 |
| **TUNE** | Botón | Activa un autotune. El botón se vuelve rojo y muestra **TUNING...** mientras la sintonización está en progreso. Al completarse, el botón muestra brevemente **SWR x.xx** (el ROS final post-sintonización) durante 2.5 segundos y luego regresa a **TUNE**. | — |
| **OPERATE** / **BYPASS** / **STANDBY** | Botón | Cambia cíclicamente el estado de los relés del TGXL: OPERATE → BYPASS → STANDBY → OPERATE. La etiqueta y el color reflejan el estado actual: **OPERATE** (verde), **BYPASS** (naranja), **STANDBY** (predeterminado). | — |
| **ANT 1** | Botón | Selecciona el puerto de antena 1 en el conmutador TGXL 3x1. Visible únicamente cuando hay una conexión directa con el TGXL activa y hay un conmutador de antenas presente. | — |
| **ANT 2** | Botón | Selecciona el puerto de antena 2 en el conmutador TGXL 3x1. | — |
| **ANT 3** | Botón | Selecciona el puerto de antena 3 en el conmutador TGXL 3x1. | — |

## Consejos

- El desplazamiento con la rueda del ratón en C1, L y C2 solo está habilitado cuando hay una conexión directa con el TGXL activa. Si el desplazamiento no tiene efecto, verifique el estado de la conexión.
- El ROS post-sintonización que se muestra en el botón **TUNE** refleja el valor final estabilizado tras una breve ventana de captura, no el ROS medido durante el barrido.
- La escala del indicador de potencia directa se establece automáticamente. No se requiere configuración manual al cambiar entre configuraciones sin amplificador, Aurora y PGXL.

## Relacionados

- [Ejecutar un autotune en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajuste fino de los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Leer el ROS inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)

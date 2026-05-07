# Resumen del sintonizador

El applet Sintonizador le brinda control en tiempo real sobre un sintonizador de antena externo 4O3A Tuner Genius XL (TGXL) directamente desde AetherSDR. Desde un único panel puede leer la potencia directa y la ROE, iniciar un autosintonizado, ajustar los bancos de relés, establecer el estado operativo del sintonizador y, cuando un conmutador de antenas TGXL 3x1 está conectado, seleccionar entre tres puertos de antena.

## Antes de comenzar

- Un Tuner Genius XL debe ser detectado por AetherSDR. El applet está oculto hasta que se encuentre el TGXL.
- AetherSDR debe estar conectado a la radio.

## Cómo funciona

El applet Sintonizador aparece en el panel de applets del lado derecho una vez que se detecta un TGXL. Alterne su visibilidad con el botón de bandeja **TUN** en la barra lateral derecha.

El applet está dividido en tres áreas:

**Medidores (superior)** — Dos indicadores horizontales muestran lecturas en vivo del TGXL.

**Barras y botones de relés (centro)** — Tres barras de posición de relés (C1, L, C2) se encuentran a la izquierda; los botones TUNE y OPERATE/BYPASS/STANDBY están a la derecha.

**Fila del conmutador de antenas (inferior)** — Tres botones de selección de antena aparecen solo cuando una conexión directa al TGXL está activa y el TGXL informa que hay un conmutador de antenas presente. La fila está oculta en caso contrario.

## Qué hace cada control

| Control         | Tipo       | Comportamiento                                                                                                                                                                                                     | Rango / estados válidos                              |
| --------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **Fwd Pwr**     | Medidor    | Muestra la potencia directa reportada por el TGXL. La escala se ajusta automáticamente según se detecte un PGXL o un Aurora.                                                                                       | 0–200 W (sin ampli.); 0–600 W (Aurora); 0–2000 W (con PGXL) |
| **SWR**         | Medidor    | Muestra la ROE reportada por el TGXL. El indicador se vuelve rojo por encima de 2.5.                                                                                                                               | 1.0–3.0                                              |
| **C1**          | Barra de relé | Muestra la posición del banco de relés C1. El scroll de la rueda del ratón ajusta el relé cuando una conexión directa al TGXL está activa.                                                                        | 0–255                                                |
| **L**           | Barra de relé | Muestra la posición del banco de relés L. El scroll de la rueda del ratón ajusta el relé cuando una conexión directa al TGXL está activa.                                                                         | 0–255                                                |
| **C2**          | Barra de relé | Muestra la posición del banco de relés C2. El scroll de la rueda del ratón ajusta el relé cuando una conexión directa al TGXL está activa.                                                                        | 0–255                                                |
| **TUNE**        | Botón      | Inicia un autosintonizado. El botón se vuelve rojo y muestra **TUNING...** mientras el sintonizado está en curso. Al finalizar, el botón muestra brevemente **SWR x.xx** (la ROE estabilizada posterior al sintonizado) durante 2.5 segundos y luego regresa a **TUNE**. | —                                                    |
| **OPERATE** / **BYPASS** / **STANDBY** | Botón | Cicla el estado del relé del TGXL: OPERATE → BYPASS → STANDBY → OPERATE. La etiqueta y el color reflejan el estado actual: **OPERATE** (verde), **BYPASS** (naranja), **STANDBY** (predeterminado).               | —                                                    |
| **ANT 1**       | Botón      | Selecciona el puerto de antena 1 en el conmutador TGXL 3x1. Visible solo cuando una conexión directa al TGXL está activa y hay un conmutador de antenas presente.                                                  | —                                                    |
| **ANT 2**       | Botón      | Selecciona el puerto de antena 2 en el conmutador TGXL 3x1.                                                                                                                                                        | —                                                    |
| **ANT 3**       | Botón      | Selecciona el puerto de antena 3 en el conmutador TGXL 3x1.                                                                                                                                                        | —                                                    |

## Consejos

- El scroll de la rueda del ratón sobre C1, L y C2 solo está habilitado cuando una conexión directa al TGXL está activa. Si el scroll no tiene efecto, verifique el estado de la conexión.
- La ROE posterior al sintonizado que se muestra en el botón **TUNE** refleja el valor final estabilizado después de una breve ventana de captura, no la ROE medida durante el barrido.
- La escala del medidor de potencia directa se establece automáticamente. No se requiere configuración manual al cambiar entre configuraciones sin amplificador, con Aurora y con PGXL.

## Relacionados

- [Ejecutar un autosintonizado en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Leer la ROE inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)

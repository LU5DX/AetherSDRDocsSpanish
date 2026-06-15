# Resumen del sintonizador

El applet Sintonizador le brinda control en tiempo real sobre un sintonizador de antena externo 4O3A Tuner Genius XL (TGXL) directamente desde AetherSDR. Desde un solo panel puede leer la potencia directa y la ROE, iniciar un autosintonizador, ajustar bancos de relés, establecer el estado operativo del sintonizador y — cuando hay un conmutador de antena TGXL 3x1 conectado — seleccionar entre tres puertos de antena.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL. El applet permanece oculto hasta que se encuentre el TGXL.
- AetherSDR debe estar conectado a la radio.

## Cómo funciona

El applet Sintonizador aparece en el panel de applets del lado derecho una vez que se detecta un TGXL. Alterne su visibilidad con el botón de bandeja **TUN** en la barra lateral derecha.

El applet está dividido en tres áreas:

**Medidores (parte superior)** — Dos indicadores horizontales muestran lecturas en vivo del TGXL. Cada indicador tiene una etiqueta de fila externa a la izquierda (PWR, ROE) que muestra el valor en vivo. Cuando la potencia cae por debajo del umbral, la etiqueta se limpia después de 800 ms para evitar parpadeos por ruido entre paquetes. El indicador de ROE muestra por defecto 1.0 (vacío) cuando la potencia directa es inferior a 5 W para evitar mostrar lecturas espurias en reposo.

**Barras y botones de relés (centro)** — Tres barras de posición de relés (C1, L, C2) están a la izquierda; los botones TUNE y OPERATE/BYPASS/STANDBY están a la derecha.

**Fila del conmutador de antena (parte inferior)** — Tres botones de selección de antena aparecen solo cuando hay una conexión directa TGXL activa y el TGXL informa que hay un conmutador de antena presente. La fila está oculta en caso contrario.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango/estados válidos |
|---|---|---|---|
| **Fwd Pwr** | Medidor (indicador) | Muestra la potencia directa informada por el TGXL. La escala se ajusta automáticamente según se detecte un amplificador PGXL o Aurora. El indicador tiene balística: la barra sube rápidamente en ráfagas de RF pero disminuye en aproximadamente 800 ms para un efecto visual suave. | 0–200 W (sin amplificador); 0–600 W (Aurora); 0–2000 W (con PGXL) |
| **ROE** | Medidor (indicador) | Muestra la ROE informada por el TGXL. El indicador muestra por defecto 1.0 (vacío) cuando la potencia directa es inferior a 5 W para evitar mostrar lecturas espurias en reposo del TGXL que envía ROE=0.0000 (pérdida de retorno = 0 dB) en reposo. El indicador se vuelve rojo por encima de 2.5, amarillo por encima de 2.0. | 1.0–3.0 |
| **C1** | Barra de relé | Muestra la posición del banco de relés C1. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa TGXL activa. | 0–255 |
| **L** | Barra de relé | Muestra la posición del banco de relés L. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa TGXL activa. | 0–255 |
| **C2** | Barra de relé | Muestra la posición del banco de relés C2. El desplazamiento con la rueda del ratón ajusta el relé cuando hay una conexión directa TGXL activa. | 0–255 |
| **TUNE** | Botón | Inicia un autosintonizador. El botón se vuelve rojo y muestra **TUNNING...** mientras está en proceso. Cuando finaliza el sintonizador, el botón muestra brevemente **ROE x.xx** (la ROE estabilizada posterior al sintonizador) durante 2.5 segundos, luego vuelve a **TUNE**. Cuando hay una conexión directa TGXL (puerto 9010) configurada, envía el comando nativo 'autotune' directamente al TGXL en lugar de enrutarlo a través de la ruta del firmware de la radio. Vuelve a la ruta de la radio cuando no hay conexión directa disponible. Configure la conexión directa en Configuración de Radio → Sintonizador. | — |
| **OPERATE** / **BYPASS** / **STANDBY** | Botón | Cambia el estado del relé del TGXL: OPERATE → BYPASS → STANDBY → OPERATE. La etiqueta y el color reflejan el estado actual: **OPERATE** (verde), **BYPASS** (naranja), **STANDBY** (predeterminado). | — |
| **ANT 1** | Botón | Selecciona el puerto de antena 1 en el conmutador TGXL 3x1. Visible solo cuando hay una conexión directa TGXL activa y hay un conmutador de antena presente. | — |
| **ANT 2** | Botón | Selecciona el puerto de antena 2 en el conmutador TGXL 3x1. | — |
| **ANT 3** | Botón | Selecciona el puerto de antena 3 en el conmutador TGXL 3x1. | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Botón TUNE** | TUNE / TUNNING... / ROE x.xx | En reposo / sintonización en curso / ROE posterior al sintonizador capturada (parpadea durante 2.5 s). |
| **Botón OPERATE** | OPERATE (verde) / BYPASS (naranja) / STANDBY (predeterminado) | Estado del relé/derivación del TGXL. |
| **Indicador de potencia directa** | Barra con retención de pico | La marca blanca muestra la potencia directa máxima. Se borra después de 2.5 segundos sin nuevos picos. El indicador se vuelve amarillo a 80 W (sin amplificador), 400 W (Aurora) o 1000 W (PGXL). Se vuelve rojo a 125 W (sin amplificador), 500 W (Aurora) o 1500 W (PGXL). |
| **Indicador de ROE** | Barra | Muestra por defecto 1.0 (vacío) cuando la potencia directa es inferior a 5 W. Muestra la ROE real cuando la potencia directa es de 5 W o superior. |

## Accesibilidad

Los controles del applet Sintonizador incluyen nombres accesibles para lectores de pantalla:

| Control | Nombre accesible |
|---|---|
| Indicador de potencia directa | "Forward power" |
| Indicador de ROE | "SWR" |
| Barra de relé C1 | "Tuner capacitor C1" |
| Barra de relé L | "Tuner inductor L" |
| Barra de relé C2 | "Tuner capacitor C2" |

## Consejos

- El desplazamiento con la rueda del ratón sobre C1, L y C2 solo está habilitado cuando hay una conexión directa TGXL activa. Si el desplazamiento no tiene efecto, verifique el estado de la conexión.
- La ROE posterior al sintonizador que se muestra en el botón **TUNE** refleja el valor final estabilizado después de una breve ventana de captura, no la ROE medida durante el barrido.
- La escala del indicador de potencia directa se establece automáticamente. No se requiere configuración manual al cambiar entre configuraciones sin amplificador, Aurora y PGXL.
- El indicador de potencia directa tiene balística: la barra sube rápidamente en ráfagas de RF pero disminuye en aproximadamente 800 ms para un efecto visual suave.
- La marca blanca de retención de pico en el indicador de potencia directa se borra automáticamente después de 2.5 segundos sin nuevos picos.
- El indicador de ROE permanece en 1.0 (vacío) cuando la potencia directa es inferior a 5 W. Esto evita que el indicador muestre lecturas espurias de ROE alta cuando el TGXL está en reposo y envía ROE=0.0000 (pérdida de retorno = 0 dB). El indicador solo muestra valores de ROE en vivo cuando la potencia directa es de 5 W o superior.

## Relacionado

- [Ejecutar un autosintonizador en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)
- [Cambiar entre tres antenas en un TGXL 3x1](switch-between-three-antennas-on-a-tgxl-3x1.md)
- [Leer la ROE inmediatamente después de un sintonizador](read-swr-immediately-after-a-tune.md)

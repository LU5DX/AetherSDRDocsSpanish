## Ajuste fino de los relés C1/L/C2 con la rueda del ratón

Después de un autoajuste, puede ajustar las posiciones de los bancos de relés C1, L y C2 paso a paso con la rueda del ratón. Esto le permite recorrer manualmente las posiciones de relés adyacentes para buscar una ROE más baja sin desencadenar un reajuste completo.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL (TGXL). El applet Tuner está oculto hasta que eso ocurra.
- Debe estar activa una **conexión directa al TGXL**. El desplazamiento con la rueda del ratón sobre las barras de relés está deshabilitado cuando AetherSDR se comunica con el TGXL solo a través de la radio (modo no directo).
- Abra el applet Tuner haciendo clic en el botón de la bandeja **TUN** en la barra lateral derecha.

## Pasos

1. Confirme que el applet Tuner esté visible. Si no lo está, haga clic en el botón de la bandeja **TUN**.
2. Verifique que la conexión directa al TGXL esté activa. Si las barras de relés no responden al desplazamiento, la conexión directa no está establecida; consulte [Descripción general del Tuner](overview.md).
3. Coloque el cursor del ratón sobre la barra **C1**.
4. Desplace la rueda del ratón hacia arriba para aumentar la posición del relé C1 en un paso, o hacia abajo para disminuirla en un paso.
5. Repita el procedimiento en la barra **L** para ajustar el banco de relés de inductancia.
6. Repita el procedimiento en la barra **C2** para ajustar el segundo banco de relés de capacitancia.
7. Observe el indicador **SWR** después de cada paso para evaluar el efecto.

## Qué hace cada control

| Control | Qué muestra | Rango válido | Predeterminado | Clave de configuración |
|---------|--------------|-------------|---------|-------------|
| **C1** | Posición del banco de relés C1 | 0–255 | 0 | — |
| **L** | Posición del banco de relés L | 0–255 | 0 | — |
| **C2** | Posición del banco de relés C2 | 0–255 | 0 | — |
| **SWR** | ROE informada por el TGXL | 1.0–3.0 (rojo por encima de 2.5) | — | — |
| **Fwd Pwr** | Potencia directa informada por el TGXL | 0–200 W sin amplificador, 0–600 W Aurora, 0–2000 W con PGXL | — | — |
| **TUNE** | Inicia un autoajuste en el TGXL | — | — | — |
| **OPERATE** | Cicla el TGXL entre los estados OPERATE, BYPASS y STANDBY | — | — | — |
| **ANT 1**, **ANT 2**, **ANT 3** | Selecciona el puerto de antena 1, 2 o 3 en el conmutador 3x1 del TGXL | — | — | — |

## Qué hace cada botón

### TUNE

Haga clic en **TUNE** para iniciar un autoajuste en el TGXL. Durante el ajuste, el botón se vuelve rojo y muestra **TUNING...**; cuando el ajuste se completa, parpadea mostrando la ROE posterior al ajuste como **SWR x.xx** durante 2.5 segundos y luego vuelve a **TUNE**.

Cuando está configurada una conexión directa al TGXL (puerto 9010), AetherSDR envía el comando de autoajuste directamente al TGXL. Esto evita la ruta del firmware de la radio que podría fallar en algunas configuraciones con el firmware 4.2. Cuando no hay conexión directa disponible, AetherSDR recurre a enrutar el comando a través de la radio. Configure la conexión directa en **Radio Setup > Tuner**.

### OPERATE

Haga clic en **OPERATE** para ciclar el TGXL a través de sus tres estados:

- **OPERATE** (verde): el acoplador pasa RF a través de la red de ajuste.
- **BYPASS** (naranja): el acoplador está en derivación.
- **STANDBY**: el acoplador está en espera.

Un clic avanza al siguiente estado, envolviéndose después de STANDBY.

### ANT 1 / ANT 2 / ANT 3

Haga clic en **ANT 1**, **ANT 2** o **ANT 3** para seleccionar el puerto de antena correspondiente en el conmutador 3x1 del TGXL. Esta fila solo es visible cuando una conexión directa al TGXL está activa y el conmutador de antenas está presente.

## Notas sobre la visualización de potencia y ROE

- El indicador de potencia directa se escala automáticamente según la configuración de su radio y amplificador:
  - **Sin amplificador:** 0–200 W, amarillo por encima de 80 W, rojo por encima de 125 W
  - **Aurora (amplificador de 500 W):** 0–600 W, amarillo por encima de 400 W, rojo por encima de 500 W
  - **PGXL:** 0–2000 W, amarillo por encima de 1000 W, rojo por encima de 1500 W
- Las etiquetas de escala y los colores de umbral se actualizan automáticamente al cambiar la configuración del amplificador en Radio Setup. AetherSDR omite actualizaciones redundantes del indicador cuando la configuración relevante para la escala no ha cambiado, evitando repintados innecesarios por mensajes de estado repetidos.
- El indicador de potencia utiliza balística de liberación lenta: la barra sube rápidamente en ráfagas de RF pero decae en aproximadamente 800 ms, evitando el parpadeo por ruido entre paquetes.
- Un indicador de retención de pico (marca blanca) señala la potencia directa máxima registrada. El pico se borra después de 2.5 segundos sin un nuevo pico.
- Cuando la potencia cae por debajo del umbral de detección, las etiquetas PWR y SWR permanecen visibles durante 800 ms antes de volver a su texto predeterminado, evitando parpadeos durante pausas breves en la transmisión.
- El indicador de ROE se ajusta automáticamente a 1.0 cuando la potencia directa es inferior a 5 W. Esto evita que el indicador se fije en un valor alto debido al ruido en reposo cuando no hay señal presente. La lectura se actualiza normalmente cuando la potencia directa es de 5 W o superior.

## Consejos

- El desplazamiento ajusta la posición del relé un paso por detente de la rueda. No hay modo grueso/fino; cada evento de desplazamiento envía un incremento o decremento al TGXL.
- Si desea volver a una posición conocida y correcta, ejecute un nuevo autoajuste con el botón **TUNE** en lugar de retroceder manualmente paso a paso.

## Solución de problemas

- **Desplazar la rueda del ratón sobre una barra de relés no hace nada**: la conexión directa al TGXL no está activa. El desplazamiento con la rueda del ratón solo está habilitado cuando la conexión directa está presente. Verifique el estado de la conexión en la descripción general del Tuner.
- **Los valores de las barras de relés cambian pero la ROE no se actualiza**: el indicador **SWR** refleja los valores informados por el TGXL a través de la conexión directa. Si el medidor está congelado, la conexión directa puede haberse interrumpido.
- **El indicador de potencia permanece fijo en un valor**: la balística de liberación lenta mantiene la barra visible durante 800 ms. Si permanece fija por más tiempo, la conexión directa puede haberse interrumpido.
- **El indicador de ROE muestra 1.0 incluso con desajuste**: verifique su potencia directa. El indicador de ROE se mantiene en 1.0 cuando la potencia directa es inferior a 5 W. Active el transmisor o aumente la excitación hasta que la lectura de potencia supere los 5 W.
- **El botón TUNE no inicia un ajuste**: verifique que la conexión directa al TGXL esté funcionando. Si la conexión directa no está disponible, AetherSDR enruta el comando de ajuste a través de la radio, lo que puede fallar en algunas configuraciones con firmware 4.2.

## Relacionados

- [Descripción general del Tuner](overview.md)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Poner el acoplador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)

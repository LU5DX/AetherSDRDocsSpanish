# Ajuste fino de los relés C1/L/C2 con la rueda del ratón

Después de un sintonizado automático, puede ajustar las posiciones de los bancos de relés C1, L y C2 paso a paso usando la rueda del ratón. Esto le permite recorrer manualmente las posiciones de relés adyacentes para buscar una ROE más baja sin activar un resintonizado completo.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL (TGXL). La applet del sintonizador permanece oculta hasta que eso ocurra.
- Debe haber una **conexión directa con el TGXL** activa. El desplazamiento con la rueda del ratón sobre las barras de relés está deshabilitado cuando AetherSDR se comunica con el TGXL solo a través de la radio (modo no directo).
- Abra la applet del sintonizador haciendo clic en el botón de la bandeja **TUN** en la barra lateral derecha.

## Pasos

1. Confirme que la applet del sintonizador sea visible. Si no lo es, haga clic en el botón de la bandeja **TUN**.
2. Verifique que haya una conexión directa con el TGXL activa. Si las barras de relés no responden al desplazamiento, la conexión directa no está establecida — consulte [Descripción general del sintonizador](overview.md).
3. Coloque el cursor del ratón sobre la barra **C1**.
4. Desplace la rueda del ratón hacia arriba para aumentar la posición del relé C1 en un paso, o hacia abajo para disminuirla en un paso.
5. Repita en la barra **L** para ajustar el banco de relés de inductancia.
6. Repita en la barra **C2** para ajustar el segundo banco de relés de condensador.
7. Observe el indicador **SWR** después de cada paso para evaluar el efecto.

## Qué hace cada control

| Control | Lo que muestra | Rango válido | Valor predeterminado | Clave de configuración |
|---------|----------------|--------------|----------------------|------------------------|
| **C1** | Posición del banco de relés C1 | 0–255 | 0 | — |
| **L** | Posición del banco de relés L | 0–255 | 0 | — |
| **C2** | Posición del banco de relés C2 | 0–255 | 0 | — |
| **SWR** | ROE reportada por el TGXL | 1.0–3.0 (rojo por encima de 2.5) | — | — |
| **Fwd Pwr** | Potencia directa reportada por el TGXL | 0–200 W sin amplificador, 0–600 W Aurora, 0–2000 W con PGXL | — | — |

## Notas sobre la visualización de potencia

- El indicador de potencia directa se escala automáticamente según la configuración de su radio y amplificador:
  - **Sin amplificador:** 0–200 W, amarillo por encima de 80 W, rojo por encima de 125 W
  - **Aurora (amplificador de 500 W):** 0–600 W, amarillo por encima de 400 W, rojo por encima de 500 W
  - **PGXL:** 0–2000 W, amarillo por encima de 1000 W, rojo por encima de 1500 W
- Las etiquetas de escala y los colores de umbral se actualizan automáticamente al cambiar la configuración del amplificador en Radio Setup.
- El indicador de potencia utiliza una balística de liberación lenta: la barra sube rápidamente en las ráfagas de RF, pero decae en aproximadamente 800 ms, evitando parpadeos debido al ruido entre paquetes.
- Un indicador de retención de pico (marca blanca) señala la potencia directa más alta observada. El pico se limpia después de 2.5 segundos sin un nuevo pico.
- Cuando la potencia cae por debajo del umbral de detección, las etiquetas PWR y SWR permanecen visibles durante 800 ms antes de volver a su texto predeterminado, evitando parpadeos durante pausas breves en la transmisión.

## Consejos

- El desplazamiento ajusta la posición del relé un paso por cada muesca de la rueda. No hay un modo grueso/fino; cada evento de desplazamiento envía un incremento o decremento al TGXL.
- Si desea volver a una posición conocida como buena, ejecute un nuevo sintonizado automático usando el botón **TUNE** en lugar de retroceder manualmente.

## Solución de problemas

- **Desplazar la rueda del ratón sobre una barra de relés no produce ningún efecto** — La conexión directa con el TGXL no está activa. El desplazamiento con la rueda del ratón solo está habilitado cuando la conexión directa está presente. Verifique el estado de la conexión en la descripción general del sintonizador.
- **Los valores de las barras de relés cambian pero la ROE no se actualiza** — El indicador **SWR** refleja los valores reportados por el TGXL a través de la conexión directa. Si el medidor está congelado, es posible que la conexión directa se haya perdido.
- **El indicador de potencia permanece atascado en un valor** — La balística de liberación lenta mantiene la barra visible durante 800 ms. Si permanece atascada por más tiempo, es posible que la conexión directa se haya perdido.

## Relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un sintonizado automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un sintonizado](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)

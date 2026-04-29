# Ajuste fino de los relés C1/L/C2 con la rueda del ratón

Tras un ajuste automático (autotune), puede mover las posiciones de los bancos de relés C1, L y C2 un paso a la vez usando la rueda del ratón. Esto le permite recorrer manualmente las posiciones adyacentes del sintonizador para buscar una ROS más baja sin disparar un nuevo ajuste completo.

## Antes de comenzar

- AetherSDR debe haber detectado un Tuner Genius XL (TGXL). El applet Tuner permanece oculto hasta que eso ocurra.
- Debe haber una **conexión directa al TGXL** activa. El desplazamiento con la rueda del ratón sobre las barras de relés está deshabilitado cuando AetherSDR se comunica con el TGXL únicamente a través del radio (modo no directo).
- Abra el applet Tuner haciendo clic en el botón de bandeja **TUN** de la barra lateral derecha.

## Pasos

1. Confirme que el applet Tuner es visible. Si no lo es, haga clic en el botón de bandeja **TUN**.
2. Verifique que haya una conexión directa al TGXL activa. Si las barras de relés no responden al desplazamiento, la conexión directa no está establecida — consulte [Descripción general del sintonizador](overview.md).
3. Coloque el cursor del ratón sobre la barra **C1**.
4. Desplace la rueda hacia arriba para aumentar la posición del relé C1 un paso, o hacia abajo para disminuirla un paso.
5. Repita el proceso en la barra **L** para ajustar el banco de relés de inductancia.
6. Repita el proceso en la barra **C2** para ajustar el segundo banco de relés del condensador.
7. Observe el indicador **SWR** después de cada paso para evaluar el efecto.

## Qué hace cada control

| Control | Qué muestra | Rango válido | Valor predeterminado | Clave de ajuste |
|---------|-------------|--------------|----------------------|-----------------|
| **C1** | Posición del banco de relés C1 | 0–255 | 0 | — |
| **L** | Posición del banco de relés L | 0–255 | 0 | — |
| **C2** | Posición del banco de relés C2 | 0–255 | 0 | — |
| **SWR** | ROS reportada por el TGXL | 1.0–3.0 (rojo por encima de 2.5) | — | — |

## Consejos

- El desplazamiento ajusta la posición del relé un paso por cada detente de la rueda. No existe un modo grueso/fino; cada evento de desplazamiento envía un incremento o decremento al TGXL.
- Si desea volver a una posición conocida como buena, ejecute un nuevo ajuste automático con el botón **TUNE** en lugar de retroceder manualmente paso a paso.

## Solución de problemas

- **Desplazar la rueda del ratón sobre una barra de relés no hace nada** — La conexión directa al TGXL no está activa. El desplazamiento con la rueda solo está habilitado cuando la conexión directa está presente. Verifique el estado de la conexión en la descripción general del sintonizador.
- **Los valores de las barras de relés cambian pero la ROS no se actualiza** — El indicador **SWR** refleja los valores reportados por el TGXL a través de la conexión directa. Si el medidor está congelado, es posible que la conexión directa se haya interrumpido.

## Temas relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un ajuste automático en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROS inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)

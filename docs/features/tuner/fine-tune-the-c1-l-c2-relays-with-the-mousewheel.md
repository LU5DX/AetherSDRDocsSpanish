# Ajuste preciso de los relés C1/L/C2 con la rueda del ratón

Después de un autoajuste, puede mover las posiciones de los bancos de relés C1, L y C2 un paso a la vez usando la rueda del ratón. Esto le permite recorrer manualmente posiciones de relés adyacentes para buscar una ROE más baja sin desencadenar un reajuste completo.

## Antes de comenzar

- AetherSDR debe detectar un Tuner Genius XL (TGXL). El applet del sintonizador permanece oculto hasta que eso ocurra.
- Debe estar activa una **conexión directa con el TGXL**. El desplazamiento con la rueda del ratón sobre las barras de relés está desactivado cuando AetherSDR se comunica con el TGXL solo a través de la radio (modo no directo).
- Abra el applet del sintonizador haciendo clic en el botón de la bandeja **TUN** de la barra lateral derecha.

## Pasos

1. Confirme que el applet del sintonizador esté visible. Si no lo está, haga clic en el botón de la bandeja **TUN**.
2. Verifique que haya una conexión directa activa con el TGXL. Si las barras de relés no responden al desplazamiento, la conexión directa no está establecida; consulte [Visión general del sintonizador](overview.md).
3. Coloque el cursor del ratón sobre la barra **C1**.
4. Desplace la rueda del ratón hacia arriba para aumentar la posición del relé C1 en un paso, o hacia abajo para disminuirla en un paso.
5. Repita en la barra **L** para ajustar el banco de relés de inductancia.
6. Repita en la barra **C2** para ajustar el segundo banco de relés de condensador.
7. Observe el indicador de **SWR** después de cada paso para evaluar el efecto.

## Qué hace cada control

| Control | Qué muestra | Rango válido | Valor predeterminado | Clave de configuración |
|---------|-------------|--------------|---------------------|------------------------|
| **C1** | Posición del banco de relés C1 | 0–255 | 0 | — |
| **L** | Posición del banco de relés L | 0–255 | 0 | — |
| **C2** | Posición del banco de relés C2 | 0–255 | 0 | — |
| **SWR** | ROE reportada por el TGXL | 1.0–3.0 (rojo por encima de 2.5) | — | — |

## Consejos

- El desplazamiento ajusta la posición del relé un paso por muesca de la rueda. No existe un modo grueso/fino; cada evento de desplazamiento envía un incremento o decremento al TGXL.
- Si desea volver a una posición conocida que funcionaba bien, ejecute un nuevo autoajuste usando el botón **TUNE** en lugar de retroceder manualmente paso a paso.

## Solución de problemas

- **Desplazar la rueda del ratón sobre una barra de relés no hace nada** — La conexión directa con el TGXL no está activa. El desplazamiento con la rueda del ratón solo está habilitado cuando la conexión directa está presente. Verifique el estado de la conexión en la visión general del sintonizador.
- **Los valores de las barras de relés cambian pero la ROE no se actualiza** — El indicador de **SWR** refleja los valores reportados por el TGXL a través de la conexión directa. Si el medidor está congelado, es posible que la conexión directa se haya perdido.

## Relacionados

- [Visión general del sintonizador](overview.md)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)

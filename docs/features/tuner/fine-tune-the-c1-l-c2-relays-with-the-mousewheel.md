# Ajuste fino de los relés C1/L/C2 con la rueda del ratón

Después de un autotune, puede ajustar manualmente las posiciones de los relés C1, L y C2. Esto permite optimizar la adaptación sin ejecutar un ciclo completo de autotune.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- Debe detectarse un 4O3A Tuner Genius XL; el botón TUN del área de notificación aparece en la barra lateral derecha únicamente cuando hay uno presente.
- El TGXL debe estar conectado mediante una conexión directa TGXL. El desplazamiento con la rueda del ratón sobre las barras de relés queda desactivado cuando solo hay una conexión mediada por radio activa.
- El applet Tuner debe estar abierto. Haga clic en el botón TUN del área de notificación para mostrarlo.

## Pasos

1. Confirme que las barras de relés responden a la rueda del ratón. Si hay una conexión directa TGXL activa, las barras C1, L y C2 responden a la rueda del ratón. Si no responden, consulte la sección Solución de problemas más abajo.
2. Coloque el puntero del ratón sobre la barra C1.
3. Desplace la rueda hacia arriba para aumentar la posición del relé C1, o hacia abajo para disminuirla. Cada paso de desplazamiento ajusta la posición en una unidad. Rango válido: 0–255.
4. Coloque el puntero sobre la barra L y desplace la rueda para ajustar la posición del relé L. Rango válido: 0–255.
5. Coloque el puntero sobre la barra C2 y desplace la rueda para ajustar la posición del relé C2. Rango válido: 0–255.
6. Observe el medidor de ROE mientras realiza los ajustes para confirmar que la adaptación mejora.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Comportamiento |
|---------|------|----------------------|--------------|----------------|
| C1 | Barra de relé | 0 | 0–255 | Muestra y ajusta la posición del banco de relés C1. Desplazar hacia arriba incrementa; desplazar hacia abajo decrementa. |
| L | Barra de relé | 0 | 0–255 | Muestra y ajusta la posición del banco de relés L. Desplazar hacia arriba incrementa; desplazar hacia abajo decrementa. |
| C2 | Barra de relé | 0 | 0–255 | Muestra y ajusta la posición del banco de relés C2. Desplazar hacia arriba incrementa; desplazar hacia abajo decrementa. |
| SWR | Medidor | — | 1.0–3.0 (rojo por encima de 2.5) | Muestra la ROE reportada por el TGXL en tiempo real mientras se ajustan los relés. |

## Consejos

- Ajuste un relé a la vez y espere a que el medidor de ROE se estabilice antes de pasar al siguiente. La interacción entre C1, L y C2 implica que cambiar uno afecta a los demás.
- Si la ROE está lejos de 1:1, ejecute primero un autotune completo y luego use la rueda del ratón para la corrección fina.

## Solución de problemas

- **Desplazar la rueda del ratón sobre una barra de relé no tiene efecto** — No hay una conexión directa TGXL activa. Verifique la conexión de red o USB del TGXL. El desplazamiento con la rueda del ratón se habilita únicamente cuando la conexión directa está presente.
- **El botón TUN del área de notificación no es visible** — No se ha detectado ningún Tuner Genius XL. Verifique que el TGXL esté encendido y sea accesible desde la misma red que AetherSDR.

## Temas relacionados

- [Ejecutar un autotune en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de una sintonización](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](put-the-tuner-in-operate-bypass-or-standby.md)

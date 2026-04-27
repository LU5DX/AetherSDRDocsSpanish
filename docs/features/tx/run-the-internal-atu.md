# Ejecutar el sintonizador automático de antena interno

Use el sintonizador automático de antena (ATU) interno para encontrar una coincidencia de bajo ROE en su frecuencia actual. Tras un ciclo de sintonización exitoso, el ATU almacena el resultado en memoria para recuperarlo rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX no es funcional sin una conexión al radio.
- El TGXL no debe estar en modo OPERATE. El ATU se deshabilita cuando el TGXL está en modo OPERATE.
- Establezca `Tune Pwr` en un nivel adecuado para su antena antes de ejecutar el ATU. El valor predeterminado es 10.

## Pasos

1. Haga clic en el botón de bandeja TX en la barra lateral derecha para abrir el applet TX Controls si aún no está visible.
2. Ajuste el control deslizante `Tune Pwr` al nivel de potencia de portadora de sintonización deseado (0–100; predeterminado 10).
3. Haga clic en `ATU`.
4. Espere a que el ciclo de sintonización se complete. Observe los indicadores `Success`, `Byp` y `Mem` para ver el resultado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango |
|---|---|---|---|---|
| ATU | Botón de acción | Inicia el ciclo de sintonización del ATU interno. Se deshabilita cuando el TGXL está en modo OPERATE. | — | — |
| MEM | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Se deshabilita cuando el TGXL está en modo OPERATE. | — | — |
| Tune Pwr | Control deslizante | Establece el nivel de potencia de portadora de sintonización enviado al radio durante la sintonización. | 10 | 0–100 |
| Success | Indicador | Se ilumina en verde cuando el resultado de sintonización del ATU es exitoso o correcto. | apagado | apagado / verde |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en modo Bypass o ManualBypass. | apagado | apagado / naranja |
| Mem | Indicador | Se ilumina en verde cuando el ATU está usando una memoria almacenada. | apagado | apagado / verde |

## Sugerencias

- Si `Byp` se ilumina después del ciclo de sintonización, el ATU no pudo encontrar una coincidencia y se ha puesto en derivación (bypass). Verifique su sistema de antena y el ROE antes de transmitir a plena potencia.
- Si `Mem` se ilumina, el ATU aplicó una memoria de sintonización almacenada previamente en lugar de ejecutar una sintonización completa. Esto es normal cuando `MEM` está habilitado y existe una memoria válida para la frecuencia actual.

## Solución de problemas

- **El botón ATU no responde** — El TGXL del radio está en modo OPERATE. El ATU se deshabilita en este modo. Saque el TGXL del modo OPERATE antes de intentar sintonizar.
- **El indicador Success no se ilumina después de sintonizar** — Es posible que el ATU haya entrado en derivación (verifique `Byp`) o que la potencia de portadora de sintonización sea demasiado baja para que el ATU funcione con su antena. Aumente `Tune Pwr` e inténtelo de nuevo.

## Relacionado

- [Recuperar una memoria de ATU](recall-an-atu-memory.md)
- [Iniciar una portadora de sintonización para verificar el ROE](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de portadora de sintonización](set-tune-carrier-power.md)
- [Descripción general de TX Controls](overview.md)

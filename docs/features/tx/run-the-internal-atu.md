# Ejecutar el ATU interno

Use el sintonizador automático de antena (ATU) interno para encontrar una coincidencia de bajo ROS en su frecuencia actual. Después de un ciclo de sintonización exitoso, el ATU almacena el resultado en memoria para recuperarlo rápidamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX no es funcional sin una conexión de radio.
- El TGXL no debe estar en modo OPERATE. El ATU se desactiva cuando el TGXL está en modo OPERATE.
- Establezca `Tune Pwr` a un nivel apropiado para su antena antes de ejecutar el ATU. El valor predeterminado es 10.

## Pasos

1. Haga clic en el botón TX tray en la barra lateral derecha para abrir el applet TX Controls si aún no está visible.
2. Ajuste el deslizador `Tune Pwr` al nivel de potencia de portadora de sintonización deseado (0–100; predeterminado 10).
3. Haga clic en `ATU`.
4. Espere a que se complete el ciclo de sintonización. Supervise los indicadores `Success`, `Byp` y `Mem` para ver el resultado.

## Qué hace cada control

| Control  | Tipo          | Comportamiento                                                                     |
|----------|---------------|------------------------------------------------------------------------------|
| ATU      | Botón pulsador   | Inicia el ciclo de sintonización del ATU interno. Se desactiva cuando el TGXL está en modo OPERATE. |
| MEM      | Botón de alternancia | Activa o desactiva la recuperación de memoria del ATU. Se desactiva cuando el TGXL está en modo OPERATE.     |
| Tune Pwr | Deslizador        | Establece el nivel de potencia de portadora de sintonización enviado a la radio durante la sintonización.           |
| Success  | Indicador     | Se ilumina en verde cuando el resultado de sintonización del ATU es exitoso u OK.                 |
| Byp      | Indicador     | Se ilumina en naranja cuando el ATU está en Bypass o ManualBypass.                     |
| Mem      | Indicador     | Se ilumina en verde cuando el ATU utiliza una memoria almacenada.                          |

## Consejos

- Si `Byp` se ilumina después del ciclo de sintonización, el ATU no pudo encontrar una coincidencia y se ha puesto en bypass. Verifique su sistema de antena y ROS antes de transmitir a potencia total.
- Si `Mem` se ilumina, el ATU aplicó una memoria de sintonización previamente almacenada en lugar de ejecutar una sintonización completa. Esto es normal cuando `MEM` está habilitado y existe una memoria válida para la frecuencia actual.

## Solución de problemas

- **El botón ATU no responde** — El TGXL de la radio está en modo OPERATE. El ATU se desactiva en este modo. Cambie el TGXL fuera del modo OPERATE antes de intentar sintonizar.
- **El indicador Success no se ilumina después de la sintonización** — El ATU puede haberse puesto en bypass (compruebe `Byp`) o la potencia de portadora de sintonización puede ser demasiado baja para que el ATU funcione con su antena. Aumente `Tune Pwr` e intente de nuevo.

## Relacionado

- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Iniciar una portadora de sintonización para verificar ROS](start-a-tune-carrier-to-check-swr.md)
- [Establecer la potencia de la portadora de sintonización](set-tune-carrier-power.md)
- [Descripción general de TX Controls](overview.md)

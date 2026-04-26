# Ajustar la potencia del portador de sintonía

El control deslizante "Tune Pwr" regula la potencia de RF que el radio emite cuando se presiona TUNE. Mantener este valor bajo protege la antena, el sintonizador y los transistores finales durante ajustes rutinarios del ATU o verificaciones de ROS.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX Controls no funciona sin una conexión de radio.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón TX tray en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice la fila "Tune Pwr:" en el applet TX Controls.
2. Arrastre el control deslizante "Tune Pwr" hacia la izquierda o la derecha para establecer el nivel de potencia del portador de sintonía deseado.
3. Lea el valor numérico que se muestra a la derecha del control deslizante para confirmar su configuración.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido |
|---|---|---|---|
| Tune Pwr | Establece el nivel de potencia del portador de sintonía transmitido cuando TUNE está activo. | 10 | 0–100 |

## Consejos

- El indicador numérico a la derecha del control deslizante "Tune Pwr" se actualiza mientras arrastra, de modo que puede fijar un valor exacto antes de presionar TUNE.
- Muchos operadores mantienen la potencia de sintonía en 10 o menos para reducir el desgaste de los transistores finales y cumplir con los requisitos del ATU. Auméntela solo si el sintonizador no logra encontrar una concordancia a menor potencia.
- La configuración de "Tune Pwr" es independiente del control deslizante "RF Power", que regula la potencia normal de transmisión. Cambiar uno no afecta al otro.

## Relacionado

- [Iniciar un portador de sintonía para verificar el ROS](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)

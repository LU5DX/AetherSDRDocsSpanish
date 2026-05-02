# Desplazar el tono lateral de CW a la izquierda o a la derecha

Use el control de paneo L / R en el applet Phone/CW para desplazar el tono lateral de CW hacia el canal estéreo izquierdo o derecho. El ajuste de paneo se aplica simultáneamente tanto al monitor del radio alimentado por DAX como al generador de tono lateral de baja latencia del lado del cliente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo CW para que el panel CW sea visible en el applet Phone/CW.
- El tono lateral debe estar habilitado. Si no lo está, haga clic en Sidetone en el applet Phone/CW para habilitarlo.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW si aún no está visible.
2. Confirme que el applet muestra el panel CW — los controles Sidetone, Delay, Speed, Breakin, Iambic y Pitch deben ser visibles. Si se muestra el panel Phone en su lugar, cambie el slice activo a un modo CW.
3. Localice el control deslizante **L / R pan (CW)**.
4. Arrastre el control deslizante hacia la izquierda para desplazar el tono lateral al canal izquierdo, o hacia la derecha para desplazarlo al canal derecho.
5. Para volver al centro, haga doble clic en el control deslizante **L / R pan (CW)**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| L / R pan (CW) | 50 (centro) | 0–100 | Establece la posición de paneo estéreo para el tono lateral de CW. Aplica paneo de potencia constante tanto al monitor del lado del radio (`mon_pan_cw`) como al generador de tono lateral del lado del cliente de forma sincronizada. El doble clic restablece el valor a 50. |

## Sugerencias

- La posición de paneo siempre sigue el ajuste `mon_pan_cw` del radio. Si otro cliente o el propio radio cambia `mon_pan_cw`, el control deslizante se actualizará automáticamente.
- Hacer doble clic en el control deslizante es la forma más rápida de restablecer un tono lateral centrado sin tener que adivinar el punto medio.

## Relacionado

- [Habilitar el tono lateral de CW de baja latencia (el botón Sidetone controla tanto el radio como la ruta local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Cambiar el tono / frecuencia del tono lateral de CW](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de tono lateral de TX](listen-to-a-tx-sidetone-monitor.md)

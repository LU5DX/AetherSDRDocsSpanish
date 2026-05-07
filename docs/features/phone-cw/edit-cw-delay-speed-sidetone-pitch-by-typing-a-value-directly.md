# Editar retardo/velocidad/tono local/tono de CW escribiendo un valor directamente

Escriba un número preciso directamente en cualquiera de los cuatro campos de valor de CW (Retardo, Velocidad, Volumen del tono local, Tono) en lugar de arrastrar un control deslizante o hacer clic en botones de incremento. Esto coincide con el comportamiento nativo de SmartSDR y es útil cuando ya conoce el valor exacto que desea.

## Antes de comenzar

- Asegúrese de que el slice activo esté en modo CW (el applet Phone/CW cambia automáticamente a los controles de CW).

## Pasos

1. Haga clic en el botón **P/CW** de la barra lateral derecha si el applet Phone/CW no está visible.
2. Localice el control de CW que desea editar: **Delay**, **Speed**, **Sidetone volume** o **Pitch**. Cada uno está junto a su control deslizante correspondiente.
3. Haga clic dentro del campo numérico (un QLineEdit). El campo mostrará un cursor de texto.
4. Escriba el valor deseado usando su teclado.
5. Presione **Enter** o haga clic en otro lugar para aplicar el valor.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Delay** | 500 | 0–2000 ms (paso 10) | — | Configura el retardo de interrupción de CW. |
| **Speed** | 20 | 5–100 WPM | — | Configura la velocidad de tecleo de CW. |
| **Sidetone volume** | 50 | 0–100 | — | Configura el volumen de monitorización de CW (afecta tanto a la radio como al tono local). |
| **Pitch** | 600 | 100–6000 Hz (paso 10) | — | Configura el tono/frecuencia del tono local de CW. |

## Solución de problemas

- **El valor escrito vuelve al valor anterior** — Es posible que la radio haya rechazado el valor. Asegúrese de que su entrada esté dentro del rango válido mostrado arriba. Para valores de Delay, la emisión de la radio ya no retrocede el control deslizante en la versión v0.9.8 (#2428).

## Relacionados

- [Configurar el retardo de interrupción de CW](set-cw-break-in-delay.md)
- [Configurar la velocidad de tecleo de CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar el tono/frecuencia del tono local de CW](change-cw-pitch-sidetone-frequency.md)
- [Activar el tono local de CW de baja latencia (el botón Sidetone maneja tanto la radio como la ruta local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)

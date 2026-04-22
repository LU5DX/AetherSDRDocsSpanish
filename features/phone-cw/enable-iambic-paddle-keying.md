# Habilitar el manipulador de paleta iámbica

El manipulador iámbico le permite usar una paleta squeeze para generar CW con el manipulador integrado del FLEX-8600. Esta página explica cómo activarlo y ajustar los controles CW relacionados.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW requiere una conexión activa con el radio.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente al panel de control CW cuando se selecciona un modo CW; los controles iámbicos no son visibles en modos de telefonía.

## Pasos

1. Seleccione un modo CW en el slice que desea manipular. El applet P/CW cambia al panel CW automáticamente.
2. Si el applet P/CW no está visible, haga clic en el botón de bandeja "P/CW" en la barra lateral derecha para abrirlo.
3. Haga clic en "Iambic" para activar o desactivar el manipulador de paleta iámbica. El botón se ilumina cuando está activo.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|---|
| Iambic | Botón de alternar | — | On / Off | — |
| Breakin | Botón de alternar | — | On / Off | — |
| Delay (CW) | Control deslizante | — | 0–2000 ms (paso 10) | — |
| Speed (CW) | Control deslizante | — | 5–100 WPM | — |
| Sidetone | Botón de alternar | — | On / Off | — |
| Sidetone volume | Control deslizante | — | 0–100 | — |
| Pitch < / > | Cuadro de giro | 600 Hz | 100–6000 Hz (paso 10) | — |
| L / R pan (CW) | Control deslizante | 50 | 0–100 | — |

## Consejos

- Active "Breakin" junto con "Iambic" si desea operación QSK completa — el radio volverá a recepción entre cada elemento.
- Ajuste "Delay (CW)" para establecer cuánto tiempo permanece el radio en transmisión después del último elemento manipulado antes de volver a recepción. Con 0 ms el radio pasa a recepción de inmediato.

## Temas relacionados

- [Ajustar la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Ajustar el retardo de break-in en CW](set-cw-break-in-delay.md)
- [Cambiar el pitch CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone en TX](listen-to-a-tx-sidetone-monitor.md)

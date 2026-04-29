# Compare rápidamente el ecualizador activado y desactivado con el botón ON

Use el botón ON para activar y desactivar el ecualizador del lado del equipo mientras escucha, de modo que pueda percibir la diferencia entre los ajustes actuales de banda y una respuesta plana sin mover ningún control deslizante.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet de EQ requiere una conexión activa con el equipo.
- Abra el panel Equalizer haciendo clic en el botón EQ de la bandeja en el panel de applets de la barra lateral derecha.
- Ajuste los controles deslizantes de banda a una curva no plana. Activar ON cuando todas las bandas están en 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el panel Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los controles deslizantes muestran la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se ilumina en verde y el ecualizador se aplica a la ruta seleccionada en el equipo.
4. Escuche el audio.
5. Haga clic en ON nuevamente. El resaltado verde desaparece y el ecualizador queda en bypass — el equipo vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3–5 las veces que sea necesario para comparar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se ilumina en verde cuando está habilitado. Las posiciones de los controles deslizantes se conservan mientras está en bypass. | Desactivado (sin marcar) |
| RX | Selecciona la ruta de recepción para visualización y edición. ON actúa sobre el ecualizador RX cuando RX está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para visualización y edición. ON actúa sobre el ecualizador TX cuando TX está activo. El applet se abre en esta vista de forma predeterminada. | Marcado |

## Consejos

- ON es específico de cada ruta. Activar ON mientras RX está seleccionado no afecta al ecualizador TX, y viceversa. Cambie de ruta con RX o TX antes de conmutar si desea comparar la otra dirección.
- Las posiciones de los controles deslizantes de banda no cambian al conmutar ON. Puede activarlo y desactivarlo repetidamente sin perder su curva.

## Relacionado

- [Descripción general del ecualizador (gráfico)](overview.md)
- [Activar el EQ gráfico del lado del equipo para RX](enable-radio-side-graphic-eq-for-rx.md)
- [Activar el EQ gráfico del lado del equipo para TX](enable-radio-side-graphic-eq-for-tx.md)
- [Cambiar entre el modelado de audio RX y TX](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Aumentar o reducir bandas de octava específicas (63 Hz a 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)

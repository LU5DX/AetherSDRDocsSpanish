# Compare rápidamente EQ activado vs EQ desactivado con el botón ON

Use el botón ON para activar y desactivar el ecualizador del lado de la radio mientras escucha, de modo que pueda oír la diferencia entre la configuración actual de su banda y una respuesta plana sin mover ningún deslizador.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet EQ requiere una conexión activa con la radio.
- Abra el mosaico Equalizer haciendo clic en el botón de la bandeja EQ en el panel de applets de la barra lateral derecha.
- Ajuste los deslizadores de su banda a una curva que no sea plana. Activar ON cuando todas las bandas están a 0 dB no produce ninguna diferencia audible.

## Pasos

1. En el mosaico Equalizer, haga clic en RX o TX para seleccionar la ruta que desea evaluar.
2. Confirme que los deslizadores muestren la curva que desea comparar con la respuesta plana.
3. Haga clic en ON. El botón se resalta en verde y el ecualizador se aplica a la ruta seleccionada en la radio.
4. Escuche el audio.
5. Vuelva a hacer clic en ON. El resaltado verde desaparece y el ecualizador se omite: la radio vuelve a una respuesta plana en esa ruta.
6. Repita los pasos 3 a 5 tantas veces como sea necesario para comparar.

## Función de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| ON | Activa o desactiva el ecualizador para la ruta seleccionada actualmente (RX o TX). Se resalta en verde cuando está activado. Las posiciones de los deslizadores se conservan mientras está omitido. | Desactivado (sin marcar) |
| RX | Selecciona la ruta de recepción para visualización y edición. ON actúa sobre el ecualizador RX cuando RX está activo. | Sin marcar |
| TX | Selecciona la ruta de transmisión para visualización y edición. ON actúa sobre el ecualizador TX cuando TX está activo. El applet se abre en esta vista de forma predeterminada. | Marcado |

## Consejos

- ON es específico de la ruta. Activar ON mientras RX está seleccionado no afecta al ecualizador TX, y viceversa. Cambie de ruta con RX o TX antes de activar si desea comparar la otra dirección.
- Las posiciones de los deslizadores de su banda no se modifican al activar ON. Puede activar y desactivar repetidamente de forma segura sin perder su curva.

## Relacionado

- [Equalizer (Graphic) overview](overview.md)
- [Enable radio-side graphic EQ for RX](enable-radio-side-graphic-eq-for-rx.md)
- [Enable radio-side graphic EQ for TX](enable-radio-side-graphic-eq-for-tx.md)
- [Switch between shaping RX audio and TX audio](switch-between-shaping-rx-audio-and-tx-audio.md)
- [Boost or cut specific octave bands (63 Hz to 8 kHz)](boost-or-cut-specific-octave-bands-63-hz-to-8-khz.md)

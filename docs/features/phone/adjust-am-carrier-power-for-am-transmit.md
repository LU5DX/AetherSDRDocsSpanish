# Ajustar la potencia de portadora AM para transmisión en AM

Use el control deslizante AM Carrier en el applet Phone para establecer el nivel de potencia de portadora al transmitir en modo AM. Reducir este valor disminuye la potencia de portadora no modulada; aumentarlo la incrementa.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone no está disponible sin una conexión activa al radio.
- Su slice debe estar configurado en modo AM antes de que el nivel de portadora AM tenga algún efecto en la transmisión.

## Pasos

1. Si el applet Phone no es visible en la barra lateral derecha, haga clic en el botón de bandeja **PHNE** para mostrarlo.
2. Localice la fila **AM Carrier** en la parte superior del applet Phone.
3. Arrastre el control deslizante **AM Carrier** hacia la izquierda para disminuir la potencia de portadora o hacia la derecha para aumentarla. El valor numérico a la derecha del control deslizante se actualiza mientras arrastra (por ejemplo, **48**).

## Qué hace cada control

| Control | Tipo | Rango válido | Predeterminado | Clave persistida |
|---|---|---|---|---|
| AM Carrier | Deslizador | 0–100 | — | — |

La etiqueta numérica junto al control deslizante muestra el valor actual. No existe una configuración persistida para el nivel de AM Carrier; el valor se lee desde el radio en cada conexión.

## Consejos

- El nivel actual se muestra como un número a la derecha del control deslizante (por ejemplo, **48**). Utilícelo para volver a un ajuste conocido después de experimentar.
- El control deslizante AM Carrier no tiene efecto cuando el slice está en un modo que no es AM, como SSB o CW.

## Relacionado

- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de disparo](enable-vox-and-set-trigger-threshold.md)
- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)

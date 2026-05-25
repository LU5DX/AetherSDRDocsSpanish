# Rotar la simetría de fase de la voz con el Phase rotator (0–6 etapas)

El Phase rotator encadena etapas de filtros pasa-todo antes de la compresión para simetrizar los picos de la forma de onda de la voz, reduciendo la relación de potencia pico a promedio (PAPR). Esto le permite forzar más el compresor mientras mantiene los picos limpios, maximizando la potencia de transmisión promedio sin distorsión. El control está disponible en el editor flotante StripCompPanel.

## Antes de comenzar

- El StripCompPanel flotante debe estar abierto. Haga doble clic en el mosaico **COMP** del widget **CHAIN** en el lado de TX para abrir `Aetherial Compressor — TX`.

## Pasos

1. Abra el StripCompPanel flotante haciendo doble clic en el mosaico **COMP** del widget CHAIN en el lado de TX.
2. Localice el mando **Phase** en la columna derecha del editor.
3. Gire el mando **Phase** al número de etapas deseado:
   - **0 etapas** (mostrado como `Off`) — rotación de fase desactivada.
   - **1–6 etapas** — secciones pasa-todo en cascada. 4 etapas es el valor predeterminado de radiodifusión.
4. Ajuste el mando **Drive** (0.0–18.0 dB) para inyectar más señal en el compresor, usando el Phase rotator para mantener los niveles de pico bajo control.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---------|----------------------|--------------|------------------------|----------------|
| Mando **Phase** | 0 etapas | 0–6 etapas | `ClientCompTxPhaseRotatorStages` | Número de secciones pasa-todo en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Se muestra como `Off` cuando es 0, `N stg` cuando está activo. |
| Mando **Drive** | 0.0 dB | 0.0–18.0 dB | `ClientCompTxDriveDb` | Aumento de ganancia previo a la compresión. Inyecta más señal por encima del umbral para que el compresor actúe con más fuerza, elevando la potencia promedio. Se muestra como `+X.X dB`. |

## Consejos

- Un ajuste de Phase de 4 etapas es el valor predeterminado de radiodifusión y funciona bien para la mayoría del audio de voz.
- Combine el Phase rotator con el mando **Drive**: aumente Drive para elevar la potencia promedio, luego incremente las etapas de Phase para limpiar los picos resultantes.
- El Phase rotator solo afecta al audio de TX y no tiene efecto en el audio de RX.

## Relacionado

- [Drive the compressor harder with pre-comp gain for PAPR reduction](drive-the-compressor-harder-with-pre-comp-gain-for-papr-reduction.md)
- [Open the full Compressor editor for knee, limiter, Drive, and Phase controls](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)

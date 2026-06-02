# Girar la simetría de fase de la voz con el rotador de fase (0–6 etapas)

El rotador de fase encadena etapas de filtro pasa-todo antes de la compresión para simetrizar los picos de la forma de onda de la voz, reduciendo la relación potencia pico a potencia promedio (PAPR). Esto le permite impulsar el compresor con más fuerza mientras mantiene los picos limpios, maximizando la potencia de transmisión promedio sin distorsión. El control está disponible en el editor flotante StripCompPanel.

## Antes de empezar

- El StripCompPanel flotante debe estar abierto. Haga doble clic en el mosaico **COMP** del widget **CHAIN** en el lado de TX para abrir `Aetherial Compressor — TX`.

## Pasos

1. Abra el StripCompPanel flotante haciendo doble clic en el mosaico **COMP** del widget CHAIN en el lado de TX.
2. Localice el mando **Phase** en la columna derecha del editor.
3. Gire el mando **Phase** al número deseado de etapas:
   - **0 etapas** (mostrado como `Off`) — rotación de fase desactivada.
   - **1–6 etapas** — secciones pasa-todo en cascada. 4 etapas es el valor por defecto de emisora.
4. Ajuste el mando **Drive** (0.0–18.0 dB) para enviar más señal al compresor, usando el rotador de fase para mantener los niveles de pico bajo control.

## Función de cada control

| Control          | Valor por defecto                                                                                                                                                                                                                                                     | Rango válido                                                                                                                                                                                                                                                                                                                                                                         |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mando **Phase**  | 0 etapas                                                                                                                                                                                                                                                              | 0–6 etapas                                                                                                                                                                                                                                                                                                                                                                           |
| Mando **Drive**  | 0.0 dB                                                                                                                                                                                                                                                                | 0.0–18.0 dB                                                                                                                                                                                                                                                                                                                                                                          |
| Drive            | Aumento de ganancia previo a la compresión con auto-compensación de nivel vinculada. Envía más señal a través del umbral para que el compresor trabaje con más fuerza, y simultáneamente añade la misma ganancia a la salida para que el RMS promedio suba junto con los picos, en lugar de bajar. Combínelo con Phase para mantener los picos limpios. | Se muestra solo en el StripCompPanel flotante (columna derecha). La etiqueta aparece como '+X.X dB'. La información sobre herramientas explica la reducción de PAPR #2887. La auto-compensación sigue el modelo broadcast-Optimod — Drive envía más material al procesamiento Y añade la misma ganancia de vuelta, para que el control fijo de Makeup siga siendo un mando de ajuste final limpio y posterior a todo. |
| Phase            | Número de secciones pasa-todo en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. | Se muestra solo en el StripCompPanel flotante (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase previo a la compresión (#2887). Cascada pasa-todo que simetriza los picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor por defecto de emisora.' Los centros por defecto (300/700/1500/2500 Hz con opcionales 1000/2000 Hz) cubren el rango de formantes del habla sin agruparse. |

## Consejos

- Un ajuste de Phase de 4 etapas es el valor por defecto de emisora y funciona bien para la mayoría del audio de voz.
- Combine el rotador de fase con el mando **Drive**: aumente Drive para elevar la potencia promedio, luego aumente las etapas de Phase para limpiar los picos resultantes.
- El rotador de fase solo afecta al audio de TX y no tiene efecto sobre el audio de RX.

## Relacionado

- [Drive the compressor harder with pre-comp gain for PAPR reduction](drive-the-compressor-harder-with-pre-comp-gain-for-papr-reduction.md)
- [Open the full Compressor editor for knee, limiter, Drive, and Phase controls](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)

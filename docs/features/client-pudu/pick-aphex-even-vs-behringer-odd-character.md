# Seleccionar carácter Aphex (Even) vs Behringer (Odd)

Elija entre dos algoritmos de realce armónico en el excitador PUDU: el modo Even (linaje Aphex) para un carácter más cálido y asimétrico, o el modo Odd (linaje Behringer) para un sonido más brillante y simétrico. La selección se aplica de forma independiente a las cadenas TX y RX.

## Antes de comenzar

- La etapa PUDU debe estar visible en la cadena Aetherial Audio. Si el applet está oculto, habilite la etapa PUDU mediante el widget CHAIN en el lado TX o RX, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante.
- Decida si va a ajustar la ruta de transmisión ("Aetherial TX Poodoo™") o la ruta de recepción ("Aetherial RX Poodoo™"). Los dos lados son completamente independientes.

## Pasos

1. Ubique el applet correcto — "Aetherial TX Poodoo™" para transmisión o "Aetherial RX Poodoo™" para recepción — dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Localice los dos botones de modo directamente debajo del logotipo de PooDoo: `Even` y `Odd`.
3. Haga clic en `Even` para seleccionar el modelado asimétrico de linaje Aphex — predominantemente armónicos pares, más cálido, con saturación LF de tipo Big Bottom. El botón se ilumina en ámbar cuando está activo.
4. Haga clic en `Odd` para seleccionar el modelado simétrico tanh de linaje Behringer — armónicos impares puros, más brillante, con un compresor de graves de tipo feed-forward.
5. Repita el proceso en el otro applet si desea el mismo carácter en ambas cadenas.

La selección se guarda inmediatamente en `ClientPuduTxMode` (TX) o `ClientPuduRxMode` (RX).

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| `Even` | Selecciona el modelado asimétrico de linaje Aphex. Exclusivo con `Odd`. | — | Seleccionado / no seleccionado | `ClientPuduTxMode` / `ClientPuduRxMode` |
| `Odd` | Selecciona el modelado simétrico tanh de linaje Behringer. Exclusivo con `Even`. | — | Seleccionado / no seleccionado | `ClientPuduTxMode` / `ClientPuduRxMode` |

Solo uno de los modos `Even` u `Odd` puede estar activo a la vez. Al seleccionar uno, el otro se deselecciona automáticamente.

## Consejos

- El modo Even es adecuado para señales de voz cuando el objetivo es calidez y cuerpo en las frecuencias bajas. El modo Odd es preferible cuando se busca mayor presencia y brillo.
- El logotipo de PooDoo pulsa con el nivel RMS de la señal procesada (wet), de modo que puede observar la reacción del excitador al cambiar de modo sin necesidad de monitorear el audio.
- Los seis mandos Poo y Doo permanecen activos independientemente del modo seleccionado; su efecto sobre la señal varía según el modo elegido.

## Relacionados

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Ajustar el drive Poo para mayor grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Agregar aire con los armónicos Doo](add-air-with-doo-harmonics.md)
- [Omitir PUDU desde cualquiera de las cadenas](bypass-pudu-from-either-chain.md)

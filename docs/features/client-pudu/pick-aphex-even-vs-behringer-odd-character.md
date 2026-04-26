# Seleccionar el carácter Aphex (Par) o Behringer (Impar)

Elija entre dos algoritmos de realce armónico en el excitador PUDU: el modo Even (linaje Aphex) para un carácter más cálido y asimétrico, o el modo Odd (linaje Behringer) para un sonido más brillante y simétrico. La selección se aplica de forma independiente a las cadenas de TX y RX.

## Antes de comenzar

- La etapa PUDU debe ser visible en la cadena Aetherial Audio. Si el applet está oculto, habilite la etapa PUDU mediante el widget CHAIN en el lado TX o RX, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante.
- Decida si está ajustando la ruta de transmisión ("Aetherial TX Poodoo™") o la ruta de recepción ("Aetherial RX Poodoo™"). Los dos lados son completamente independientes.

## Pasos

1. Localice el applet correcto —"Aetherial TX Poodoo™" para transmisión o "Aetherial RX Poodoo™" para recepción— dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Encuentre los dos botones de modo directamente debajo del logotipo de PooDoo: `Even` y `Odd`.
3. Haga clic en `Even` para seleccionar el modelado asimétrico de linaje Aphex — predominantemente armónicos pares, más cálido, con saturación LF tipo Big Bottom. El botón se ilumina en ámbar cuando está activo.
4. Haga clic en `Odd` para seleccionar el modelado simétrico tanh de linaje Behringer — armónicos impares puros, más brillante, con un compresor de graves de alimentación directa (feed-forward).
5. Repita el procedimiento en el otro applet si desea el mismo carácter en ambas cadenas.

La selección se guarda inmediatamente en `ClientPuduTxMode` (TX) o `ClientPuduRxMode` (RX).

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|
| `Even` | Selecciona el modelado asimétrico de linaje Aphex. Exclusivo con `Odd`. | — | Seleccionado / no seleccionado | `ClientPuduTxMode` / `ClientPuduRxMode` |
| `Odd` | Selecciona el modelado simétrico tanh de linaje Behringer. Exclusivo con `Even`. | — | Seleccionado / no seleccionado | `ClientPuduTxMode` / `ClientPuduRxMode` |

Solo uno de `Even` u `Odd` puede estar activo a la vez. Al seleccionar uno, el otro se deselecciona automáticamente.

## Consejos

- El modo Even es adecuado para señales de voz cuando el objetivo es calidez y cuerpo en las bajas frecuencias. El modo Odd es preferible cuando se busca mayor presencia y brillo.
- El logotipo de PooDoo pulsa con el RMS de la señal procesada (wet), por lo que puede ver la reacción del excitador al cambiar de modo sin necesidad de monitorear el audio.
- Los seis controles Poo y Doo permanecen activos independientemente del modo seleccionado; su efecto sobre la señal cambia de carácter según el modo elegido.

## Relacionado

- [Descripción general de Aetherial TX Poodoo / Aetherial RX Poodoo](overview.md)
- [Ajustar el Drive Poo para mayor grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Agregar aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Omitir el PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md)

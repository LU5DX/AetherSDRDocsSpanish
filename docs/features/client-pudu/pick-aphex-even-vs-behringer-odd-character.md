# Elegir el carácter Par (Aphex) frente a Impar (Behringer)

Elija entre dos algoritmos de realce armónico en el excitador PUDU: el modo Par (linaje Aphex) para un carácter más cálido y asimétrico, o el modo Impar (linaje Behringer) para un sonido más brillante y simétrico. La elección se aplica de forma independiente a las cadenas de TX y RX.

## Antes de comenzar

- La etapa PUDU debe estar visible en la cadena Aetherial Audio. Si el applet está oculto, habilite la etapa PUDU mediante el widget CHAIN en el lado de TX o RX, o haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor flotante.
- Decida si está ajustando la ruta de transmisión ("Aetherial TX Voice Processor — TX") o la ruta de recepción ("Aetherial Voice Processor — RX"). Ambos lados son completamente independientes.
- En TX, el panel se abre con el título "Aetherial Voice Processor — TX". En RX, el panel se abre con el título "Aetherial Voice Processor — RX". Utilice el panel correcto para la cadena que desea ajustar.

## Pasos

1. Abra el panel del excitador PUDU: haga doble clic en la etapa PUDU en el widget CHAIN del lado TX o RX. Aparecerá el editor flotante con el título correcto para esa cadena.
2. Localice los dos botones de modo directamente debajo del logotipo de PooDoo: `Even` y `Odd`.
3. Haga clic en `Even` para seleccionar el modelado asimétrico de linaje Aphex — armónicos pares predominantes, más cálidos, con saturación Big Bottom de LF. El botón se ilumina en ámbar cuando está activo.
4. Haga clic en `Odd` para seleccionar el modelado simétrico tanh de linaje Behringer — armónicos impares puros, más brillantes, con un compresor de graves feed-forward.
5. Cierre el panel. Para ajustar la otra cadena, haga doble clic en su etapa PUDU en el widget CHAIN para abrir su panel independiente.

La selección se guarda inmediatamente en `ClientPuduTxMode` (TX) o `ClientPuduRxMode` (RX).

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|
| `Even` | Selecciona el modelado asimétrico de linaje Aphex. Exclusivo con `Odd`. | — | Seleccionado / Sin seleccionar | `ClientPuduTxMode` / `ClientPuduRxMode` |
| `Odd` | Selecciona el modelado simétrico tanh de linaje Behringer. Exclusivo con `Even`. | — | Seleccionado / Sin seleccionar | `ClientPuduTxMode` / `ClientPuduRxMode` |

Solo puede estar activo uno de los modos `Even` u `Odd` a la vez. Seleccionar uno deselecciona el otro.

## Consejos

- El modo Even es adecuado para señales de voz donde se busca calidez y cuerpo en las frecuencias graves. El modo Odd es adecuado para situaciones donde se prefiere una mayor presencia y brillo.
- El logotipo de PooDoo pulsa con la RMS de la señal procesada (wet), de modo que puede ver la reacción del excitador al cambiar de modos sin necesidad de monitorizar el audio.
- Cuando la etapa PUDU está en bypass, el mosaico completo del applet se atenúa aproximadamente al 55% de opacidad, igualando el efecto de atenuación aplicado a la curva EQ. Esto es solo un indicador visual y no afecta a sus ajustes.
- Los seis controles de Body y Clarity permanecen activos independientemente del modo seleccionado; su efecto sobre la señal cambia de carácter según el modo elegido.

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Dial Poo Drive for LF thickness](dial-poo-drive-for-lf-thickness.md)
- [Add air with Doo Air](add-air-with-doo-harmonics.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)

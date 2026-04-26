# Verificar la IP del radio y la dirección de enlace local

Use el diálogo **Network Diagnostics** para confirmar qué dirección IP está apuntando AetherSDR en el radio y qué interfaz de red local está utilizando para la conexión.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse tanto si hay un radio conectado como si no.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice el grupo **Network Status**.
3. Lea **Target Radio IP**. Muestra la dirección IP del radio conectado. Si no hay ningún radio conectado, muestra `Not connected`.
4. Lea **Selected Source**. Muestra la NIC local o la ruta de enlace que AetherSDR está utilizando para la conexión.
5. Opcionalmente, lea **Local TCP** y **Local UDP** para ver los extremos locales exactos de cada protocolo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **Status** | Estado general del enlace. |
| **Target Radio IP** | Dirección IP del radio conectado. Muestra `Not connected` cuando no hay ningún radio presente. |
| **Selected Source** | NIC local o ruta de enlace utilizada para la conexión. |
| **Local TCP** | Extremo TCP local para la conexión con el radio. |
| **Local UDP** | Extremo UDP local para la conexión con el radio. |

## Consejos

- No es necesario tener una conexión activa con el radio para abrir el diálogo. **Target Radio IP** mostrará `Not connected` en lugar de una dirección cuando el radio esté desconectado, lo que puede confirmar por sí mismo que no se ha establecido ninguna conexión.
- **Selected Source** es la ruta de enlace elegida en el momento de la conexión. Si AetherSDR está enrutando el tráfico a través de una interfaz inesperada, compruebe este valor antes de buscar el problema en otro lugar.

## Relacionados

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)

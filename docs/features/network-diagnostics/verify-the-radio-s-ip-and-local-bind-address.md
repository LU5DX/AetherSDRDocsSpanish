# Verificar la IP del radio y la dirección de enlace local

Use esta página para confirmar a qué dirección IP se ha conectado AetherSDR en su FLEX-8600 y qué interfaz de red local está utilizando para esa conexión.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión activa con el radio, pero los campos mostrarán valores significativos únicamente después de que se haya realizado un intento de conexión.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice el grupo **Network Status** en la parte superior izquierda.
3. Lea **Target Radio IP** — muestra la dirección IP del radio al que se conectó AetherSDR. Si no se ha establecido ninguna conexión, el campo muestra `Not connected`.
4. Lea **Selected Source** — muestra la interfaz de red local o la ruta de enlace que AetherSDR utilizó para alcanzar el radio.
5. Lea **Local TCP** y **Local UDP** para ver los extremos locales exactos de cada protocolo.
6. Haga clic en Close cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **Status** | Estado general del enlace de la conexión actual. |
| **Target Radio IP** | Dirección IP del radio conectado. Muestra `Not connected` si no hay ninguna conexión activa. |
| **Selected Source** | NIC local o ruta de enlace utilizada para alcanzar el radio. |
| **Local TCP** | Extremo TCP local (dirección y puerto). |
| **Local UDP** | Extremo UDP local (dirección y puerto). |

## Consejos

- El diálogo actualiza todos los valores una vez por segundo. Si acaba de conectarse, espere un momento para que los campos se completen.
- **Selected Source** es útil cuando el equipo tiene múltiples interfaces de red. Confirme que muestra la interfaz en la misma subred que el radio, y no una VPN o un adaptador secundario.

## Solución de problemas

- **Target Radio IP muestra `Not connected`** — No hay ninguna conexión activa con el radio. Use `Settings > Connect to Radio...` para descubrir y conectarse a su FLEX-8600, y luego vuelva a abrir el diálogo.
- **Selected Source muestra una interfaz inesperada** — Su sistema operativo enrutó la conexión a través de una NIC diferente a la prevista. Revise su tabla de enrutamiento o deshabilite las interfaces de red no utilizadas, y luego vuelva a conectarse.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)

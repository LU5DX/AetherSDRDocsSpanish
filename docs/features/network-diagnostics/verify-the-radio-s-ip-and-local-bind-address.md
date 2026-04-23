# Verificar la IP del radio y la dirección de enlace local

Use esta página para confirmar a qué dirección IP se ha conectado AetherSDR y qué interfaz de red local utiliza para alcanzar el radio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse tanto si hay un radio conectado como si no.
- Si desea ver una dirección IP activa, conéctese primero a su FLEX-8600.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Se abre el diálogo Network Diagnostics. Localice el grupo **Network Status** en el área superior izquierda.
3. Lea el indicador **Target Radio IP**. Muestra la dirección IP del radio conectado. Si no hay ningún radio conectado, indica `Not connected`.
4. Lea el indicador **Selected Source**. Muestra la interfaz de red local o la ruta de enlace que AetherSDR utiliza para la conexión.
5. Lea **Local TCP** y **Local UDP** para ver los puntos de conexión locales exactos asignados a cada protocolo.
6. Haga clic en Close cuando termine.

## Qué hace cada control

| Indicador | Qué muestra |
|---|---|
| **Status** | Estado general del enlace de la conexión con el radio. |
| **Target Radio IP** | Dirección IP del radio conectado. Muestra `Not connected` cuando no hay ningún radio conectado. |
| **Selected Source** | La NIC local o ruta de enlace utilizada para la conexión. |
| **Local TCP** | El punto de conexión TCP local (dirección y puerto) para la conexión de control. |
| **Local UDP** | El punto de conexión UDP local (dirección y puerto) para la conexión de flujo de datos. |

## Consejos

- El campo **Selected Source** es útil cuando su equipo tiene múltiples interfaces de red. Confirme que muestra la interfaz que está en la misma subred que el radio.
- **Target Radio IP** y **Selected Source** se actualizan una vez por segundo. Si acaba de conectarse, espere un momento para que la pantalla se refresque.

## Solución de problemas

- **Target Radio IP muestra `Not connected`** — No hay ninguna conexión de radio activa. Vaya a `Settings > Connect to Radio...` para descubrir y conectarse a un FLEX-8600 en la red.
- **Selected Source muestra una interfaz inesperada** — Es posible que AetherSDR se haya enlazado a la NIC incorrecta. Revise la tabla de enrutamiento de su sistema operativo y confirme que la subred del radio es accesible desde la interfaz esperada.

## Relacionados

- [Descripción general de Network Diagnostics](overview.md)
- [Medir el RTT y la pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)

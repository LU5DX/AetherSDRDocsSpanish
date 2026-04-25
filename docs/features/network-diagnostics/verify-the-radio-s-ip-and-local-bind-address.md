# Verificar la IP del equipo y la dirección de enlace local

Utilice el diálogo Network Diagnostics para confirmar a qué dirección IP se ha conectado AetherSDR y qué interfaz de red local utiliza para comunicarse con el equipo.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse independientemente de si hay un equipo conectado, pero los indicadores mostrarán datos en tiempo real únicamente cuando haya una conexión activa.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice el grupo **Network Status**.
3. Lea **Target Radio IP** — muestra la dirección IP del equipo conectado. Si no hay ninguna conexión activa, aparece `Not connected`.
4. Lea **Selected Source** — muestra la NIC local o la ruta de enlace que AetherSDR está utilizando para la conexión.
5. Si necesita confirmar los puntos de enlace locales exactos, lea **Local TCP** y **Local UDP** — muestran las direcciones y puertos TCP y UDP locales en uso.
6. Haga clic en `Close` cuando haya terminado.

## Función de cada control

| Indicador | Significado |
|---|---|
| **Status** | Estado general del enlace con el equipo. |
| **Target Radio IP** | Dirección IP del equipo conectado. Muestra `Not connected` cuando no hay ningún equipo conectado. |
| **Selected Source** | NIC local o ruta de enlace utilizada para la conexión. |
| **Local TCP** | Punto de enlace TCP local (dirección y puerto). |
| **Local UDP** | Punto de enlace UDP local (dirección y puerto). |

## Consejos

- El diálogo actualiza todos los indicadores una vez por segundo, por lo que los valores se reflejan en tiempo real mientras se observan.
- Si **Target Radio IP** muestra `Not connected` y se espera una conexión, verifique la configuración de conexión mediante `Settings > Connect to Radio...`.

## Temas relacionados

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)

# Verificar la IP del radio y la dirección de enlace local

Abra el diálogo Network Diagnostics para confirmar a qué dirección IP se ha conectado AetherSDR y qué interfaz de red local está utilizando para esa conexión.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse independientemente de si hay un radio conectado, pero los campos estarán vacíos o mostrarán "Not connected" hasta que se establezca una conexión.

## Pasos

1. Haga clic en `Settings > Network...`.
2. Localice el grupo **Network Status** en la parte superior izquierda del diálogo.
3. Lea el campo **Target Radio IP**. Este muestra la dirección IP del radio al que se ha conectado AetherSDR. Si no hay ninguna conexión activa, el campo indica `Not connected`.
4. Lea el campo **Selected Source**. Este muestra la interfaz de red local o la ruta de enlace que AetherSDR está utilizando para la conexión.
5. Opcionalmente, consulte **Local TCP** y **Local UDP** para ver los extremos locales exactos de cada protocolo.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **Status** | Estado general del enlace de la conexión con el radio. |
| **Target Radio IP** | Dirección IP del radio conectado. Muestra `Not connected` cuando no hay ninguna conexión activa. |
| **Selected Source** | Interfaz de red local o ruta de enlace utilizada para alcanzar el radio. |
| **Local TCP** | Extremo TCP local (dirección y puerto). |
| **Local UDP** | Extremo UDP local (dirección y puerto). |

## Consejos

- El grupo **Network Status** se actualiza cada segundo, por lo que los valores se refrescan en el lugar sin necesidad de volver a abrir el diálogo.
- Si **Target Radio IP** muestra una dirección incorrecta, cierre el diálogo y use `Settings > Connect to Radio...` para seleccionar el radio correcto antes de volver a conectarse.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Observar la marca de tiempo del primer paquete UDP tras la conexión](../../getting-started/setup/watch-the-first-udp-packet-timestamp-after-connect.md)

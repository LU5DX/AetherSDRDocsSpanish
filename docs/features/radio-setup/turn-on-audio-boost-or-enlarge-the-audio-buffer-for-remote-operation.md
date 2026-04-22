# Activar el refuerzo de audio o ampliar el búfer de audio para operación remota

Use estos ajustes para compensar niveles de audio bajos o audio entrecortado al operar AetherSDR a través de una conexión VPN o SmartLink. Audio Boost añade ganancia adicional en la ruta de audio del cliente; un Audio Buffer más grande absorbe la fluctuación de red a costa de latencia adicional.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles se encuentran en Radio Setup, lo cual requiere una conexión de radio activa.
- Si el audio se corta, considere también verificar la configuración del códec. Consulte [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el nivel de audio del cliente, haga clic en **Audio Boost:** para activarlo.
4. Para aumentar el búfer de audio, haga clic en el control numérico **Audio Buffer:** e introduzca un valor entre 50 y 1000 ms.
5. Cierre el cuadro de diálogo. Los ajustes se guardan de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | Desactivado | Activado / Desactivado | `AudioBoost` |
| **Audio Buffer:** | Establece el tamaño del búfer de audio en el lado del cliente. Los valores más grandes reducen los cortes en conexiones de alta latencia o con fluctuación. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink):** | Selecciona el códec de audio utilizado a través de SmartLink o LAN (Auto / Uncompressed / Opus). | Auto | Auto / Uncompressed / Opus | `AudioCompression` |

## Consejos

- Aumente **Audio Buffer:** en incrementos de 50–100 ms hasta que los cortes desaparezcan. Cada incremento añade la misma cantidad de latencia de audio en un sentido, por lo que use el valor mínimo que produzca audio limpio.
- **Audio Boost:** afecta únicamente la ruta de audio del cliente; no modifica la ganancia de Line Out ni de los auriculares de la radio.

## Solución de problemas

- **El audio sigue entrecortado después de ampliar el búfer** — El códec puede ser el cuello de botella. Cambie **Audio Compression (SmartLink):** de Auto a Opus, que está diseñado para enlaces con pérdidas o ancho de banda variable. Consulte [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).
- **Audio Boost provoca distorsión** — La señal entrante puede estar en o cerca del nivel máximo. Reduzca la ganancia de audio del slice antes de activar **Audio Boost:**, o desactívelo y aumente la ganancia solo hasta donde la señal lo permita sin recorte.

## Relacionados

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)

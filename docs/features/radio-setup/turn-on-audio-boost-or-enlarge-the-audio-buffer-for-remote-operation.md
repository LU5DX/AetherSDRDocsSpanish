# Activar el refuerzo de audio o ampliar el búfer de audio para operación remota

Use estas opciones cuando opere AetherSDR a través de una conexión VPN o SmartLink y necesite audio más fuerte o una reproducción más fluida con menos interrupciones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña `Audio` no es accesible sin una conexión activa al radio.
- Si usa SmartLink, confirme primero su configuración de compresión de audio. Consulte [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña `Audio`.
3. Para aumentar el nivel de salida en el cliente, haga clic en `Audio Boost:` para activarlo.
4. Para reducir las interrupciones de audio en un enlace con alta latencia o fluctuación, haga clic en el cuadro de control `Audio Buffer:` y establezca un valor en milisegundos. Los valores más altos añaden más latencia pero absorben mayor fluctuación.
5. Cierre el diálogo. La configuración se guarda automáticamente al cerrar.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| `Audio Boost:` | Habilita ganancia adicional en la ruta de audio del cliente. | Desactivado | Activado / Desactivado | `AudioBoost` |
| `Audio Buffer:` | Aumenta el búfer de audio del lado del cliente para absorber la fluctuación de VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| `Audio Compression (SmartLink):` | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Las opciones son Auto, Uncompressed y Opus. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |

## Consejos

- Comience con un aumento moderado de `Audio Buffer:` (por ejemplo, 150–200 ms) antes de subir más. Los valores más grandes mejoran la estabilidad, pero aumentan el retardo entre la transmisión y la escucha del tono lateral o el audio de monitoreo.
- `Audio Boost:` afecta únicamente la ruta de reproducción del cliente. No modifica los niveles de salida de línea ni de auriculares del radio.

## Solución de problemas

- **El audio sigue cortándose después de aumentar el búfer** — Verifique si el códec está configurado en Uncompressed en `Audio Compression (SmartLink):`. El audio sin comprimir demanda considerablemente más ancho de banda que Opus. Cambie a Auto u Opus si su enlace tiene capacidad limitada.
- **Sin mejora después de activar Audio Boost:** — Verifique que el dispositivo de salida de su PC esté correctamente seleccionado en `PC Audio Devices: Output:`. Si el dispositivo incorrecto está seleccionado, el refuerzo no tendrá efecto audible.

## Relacionados

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Cambiar la MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)

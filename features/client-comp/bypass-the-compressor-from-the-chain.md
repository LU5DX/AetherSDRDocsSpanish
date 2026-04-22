# Omitir el Compresor de la Cadena

Use esta página para deshabilitar (omitir) el compresor de TX del lado del cliente, de modo que el audio pase sin ser modificado. Omitirlo le permite comparar el audio comprimido y el no comprimido, o retirar temporalmente el compresor de la cadena de señal TX sin cambiar ninguna de sus configuraciones.

## Antes de comenzar

- El contenedor principal TXDSP (PooDoo Audio) debe estar visible en el panel de applets.
- La etapa Compressor ya debe estar presente en el widget CHAIN.

## Pasos

1. Localice el widget CHAIN dentro del contenedor principal TXDSP.
2. Haga clic una vez en la etapa **Comp** del widget CHAIN para activar o desactivar el bypass.
   - Cuando el bypass está activo, el mosaico del subcontenedor COMPRESSOR se oculta y `ClientCompTxEnabled` se establece en `false`.
   - Cuando el bypass está desactivado (compresor activo), el mosaico del subcontenedor COMPRESSOR se vuelve visible y `ClientCompTxEnabled` se establece en `true`.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Clave persistida |
|---|---|---|---|
| Etapa Comp (widget CHAIN) | Alternar | Habilitado (bypass desactivado) | `ClientCompTxEnabled` |
| Thresh | Perilla | -18.0 dB | `ClientCompTxThresholdDb` |
| Ratio | Perilla | 3.0 | `ClientCompTxRatio` |
| Attack | Perilla | 20.0 ms | `ClientCompTxAttackMs` |
| Release | Perilla | 200 ms | `ClientCompTxReleaseMs` |
| Makeup | Perilla | 0.0 dB | `ClientCompTxMakeupDb` |

Omitir la etapa no restablece ninguno de estos valores. Todas las posiciones de las perillas se conservan mientras la etapa está en bypass.

## Consejos

- Un solo clic activa o desactiva el bypass; un doble clic abre el editor flotante del Compressor. Tenga cuidado de no hacer doble clic cuando solo desea activar el bypass.
- El mosaico del subcontenedor COMPRESSOR desaparece por completo cuando el bypass está activo. Esto es normal: vuelve a aparecer en cuanto se reactiva la etapa.
- La barra de reducción de ganancia muestra cero mientras el bypass está activo, ya que no se aplica ninguna atenuación.

## Relacionados

- [Descripción general del Compressor](overview.md)
- [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Ver la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)

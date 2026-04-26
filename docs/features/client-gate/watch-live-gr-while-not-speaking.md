# Ver la reducción de ganancia en vivo sin estar hablando

La barra de reducción de ganancia en el applet GATE se actualiza en tiempo real, incluso cuando no está transmitiendo. Úsela para verificar que el gate permanece en silencio cuando usted calla y se abre limpiamente cuando habla.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el widget CHAIN. El subcontenedor GATE permanece oculto hasta que la etapa esté activa.
- El subcontenedor GATE debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Abra el contenedor PooDoo Audio (TXDSP) en el panel de applets.
2. Localice el subcontenedor GATE. Si no está visible, habilite primero la etapa Gate mediante el widget CHAIN.
3. Permanezca en silencio. Observe la **barra de reducción de ganancia** ámbar en la parte superior del applet. Se llena desde la derecha cuando el gate está aplicando atenuación.
4. Hable con normalidad. El relleno debe colapsar hacia cero a medida que su voz supere el umbral y el gate se abra.
5. Deje de hablar. La barra debe volver a llenarse, lo que indica que la atenuación regresa. La velocidad del relleno refleja su ajuste de **Release**.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|---|
| Transfer curve | Indicador | — | — | — |
| Gain-reduction bar | Medidor | — | 0 a 40 dB GR | — |
| Thresh | Perilla | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` |
| Ratio | Perilla | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` |
| Attack | Perilla | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` |
| Release | Perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` |
| Floor | Perilla | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` |

**Transfer curve** — muestra la curva de transferencia estática del expansor. La bola de entrada en vivo se desplaza a lo largo de la curva y cambia de estado para indicar si el gate está abierto o cerrado en ese momento.

**Gain-reduction bar** — franja ámbar horizontal, rellena desde la derecha. La escala va de 0 a 40 dB. Una marca en −15 dB indica el nivel mínimo predeterminado del expansor suave. Una barra vacía significa que no se está aplicando atenuación. Una barra llena significa que el gate está aplicando la atenuación máxima.

**Thresh** — nivel por debajo del cual el gate comienza a atenuar. Ajústelo justo por encima del nivel de ruido de fondo de su sala. Mapeo lineal.

**Ratio** — pendiente de atenuación por debajo del umbral. Los valores más altos producen un gate más duro; los valores más bajos producen una expansión descendente más suave. Mapeo lineal.

**Attack** — velocidad con la que el gate se abre cuando la entrada supera el umbral. Mapeo exponencial.

**Release** — velocidad con la que el gate se cierra después de que la entrada cae por debajo del umbral. Mapeo exponencial.

**Floor** — atenuación máxima que el gate puede aplicar. Evita que el gate corte completamente hasta el silencio. Mapeo lineal.

## Consejos

- Observe la bola de entrada en la transfer curve junto con la gain-reduction bar. Cuando la bola se encuentre por debajo del marcador de umbral, la barra debe estar llenándose. Cuando la bola lo supere, la barra debe estar vacía o casi vacía.
- Las perillas del applet permanecen sincronizadas con el editor flotante Gate. Los cambios realizados en cualquiera de los dos lugares aparecen en ambos dentro de un ciclo del medidor (aproximadamente 33 ms).
- Una marca en −15 dB en la gain-reduction bar corresponde al valor predeterminado de **Floor**. Si la barra nunca alcanza esa marca durante el silencio, es posible que **Thresh** esté ajustado demasiado bajo para capturar el ruido de fondo.

## Solución de problemas

- **La gain-reduction bar nunca se mueve** — Es posible que la etapa Gate esté omitida. Revise el widget CHAIN y confirme que la etapa esté activa. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md).
- **La barra permanece completamente llena incluso al hablar en voz alta** — Es probable que **Thresh** esté ajustado demasiado alto, por lo que la voz nunca lo supera. Reduzca **Thresh** o consulte [Ajustar el umbral justo por encima del nivel de ruido de fondo](set-threshold-just-above-room-noise-floor.md).
- **La barra se vacía y se llena de forma demasiado abrupta, produciendo un sonido entrecortado** — **Release** es demasiado corto. Aumente el valor de la perilla **Release**. Consulte [Ajustar el ataque y la liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).

## Temas relacionados

- [Descripción general del Noise Gate / Expansor](overview.md)
- [Ajustar el umbral justo por encima del nivel de ruido de fondo](set-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar el ataque y la liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md)

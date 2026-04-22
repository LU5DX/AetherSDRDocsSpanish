# Ajuste una mezcla sutil — entre 10 % y 15 % es lo habitual para voz

El control Mix regula el balance seco/húmedo del efecto de reverberación en el audio transmitido. Mantener Mix bajo — entre 10 % y 15 % — añade sensación de espacio sin que la voz suene procesada o hueca.

## Antes de comenzar

- El subcontenedor REVERB debe estar visible en el contenedor principal PooDoo Audio (TXDSP). Permanece oculto hasta que la etapa de reverberación se habilite mediante el widget CHAIN o el editor flotante.
- Habilite la etapa de reverberación antes de ajustar Mix; de lo contrario, el efecto no se escuchará aunque Mix esté por encima de cero.

## Pasos

1. Localice el subcontenedor REVERB dentro del panel PooDoo Audio (TXDSP).
2. Encuentre el control Mix — el botón más a la derecha en la fila de cinco botones.
3. Gire Mix hasta el valor deseado. La etiqueta se actualiza en tiempo real mostrando el porcentaje actual (por ejemplo, `15 %`).
4. Transmita una señal de prueba y escuche la salida de monitoreo. Ajuste Mix hacia arriba o hacia abajo hasta que la cola de reverberación sea audible pero no predominante.

Para restablecer Mix a su valor predeterminado, haga doble clic en el control Mix. El valor predeterminado es 15 %.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave persistente | Comportamiento |
|---------|----------------|-------|-------------------|----------------|
| Mix | 15 % | 0 % a 100 % | `ClientReverbTxMix` | Establece el balance seco/húmedo. Valores más altos aumentan la proporción de señal reverberada respecto a la señal seca. Mapeo lineal. |

## Consejos

- Entre 10 % y 15 % es un punto de partida práctico para voz en SSB. En estos niveles, la cola añade calidez sin hacerse notar en el extremo receptor.
- Subir Mix por encima de 30 % hace que el efecto de reverberación sea audible para la mayoría de los oyentes y puede reducir la inteligibilidad en condiciones de banda deficientes.
- Mantenga presionada la tecla Shift mientras arrastra el control Mix para un ajuste más fino (la sensibilidad del arrastre se reduce a un cuarto de lo normal).
- Desplace la rueda del ratón sobre el control Mix para avanzar en incrementos de 1 %.

## Resolución de problemas

- **Mix está por encima de 0 % pero no se escucha reverberación** — Es posible que la etapa de reverberación no esté habilitada en el widget CHAIN. Habilite la etapa y vuelva a verificar Mix.
- **La posición del control no cambia tras editarlo** — El editor flotante de reverberación y el applet REVERB se sincronizan a 30 Hz. Los cambios realizados en uno se reflejan en el otro dentro de un ciclo de actualización. Si parecen desincronizados, espere un momento o vuelva a abrir el applet.

## Temas relacionados

- [Descripción general de la reverberación](overview.md)
- [Desactivar la reverberación desde la cadena](bypass-reverb-from-the-chain.md)
- [Ajustar el tiempo de decaimiento sin enturbiar la voz](tune-decay-to-taste-without-muddying-speech.md)
- [Reducir el brillo en las frecuencias altas de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)

# Reduzca el destello agudo de la cola con Damp

El control **Damp** determina la velocidad con la que las frecuencias altas se desvanecen dentro de la cola de reverberación. Subirlo elimina el brillo y la ligereza aérea que pueden hacer que la reverberación de la voz suene antinatural en el aire.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. Si no lo está, el applet Aetherial FreeVerb está oculto y Damp no tiene efecto.
- El applet Aetherial FreeVerb o su editor flotante deben estar visibles. Consulte [Descripción general de Aetherial FreeVerb](overview.md) si aún no lo ha abierto.

## Pasos

1. Abra el editor de Aetherial FreeVerb haciendo doble clic en la etapa VERB en el widget CHAIN. Se abrirá la ventana sin marco titulada "Aetherial FreeVerb — TX".
2. Localice el control **Damp** — el tercer control desde la izquierda en la fila de cinco controles.
3. Gire **Damp** en el sentido de las agujas del reloj para aumentar el amortiguamiento. Los valores más altos hacen que las frecuencias altas decaigan más rápido, reduciendo el brillo en la cola.
4. Gire **Damp** en el sentido contrario a las agujas del reloj para permitir que las frecuencias altas persistan más tiempo, produciendo una cola más brillante y más abierta.
5. Suelte el control. El valor se guarda inmediatamente en `ClientReverbTxDamping`.

## Qué hace cada control

| Control             | Valor predeterminado | Rango       | Clave de ajuste            | Notas                                                                                              |
|---------------------|----------------------|-------------|----------------------------|----------------------------------------------------------------------------------------------------|
| Size                | 50 %                 | 0 % – 100 % | `ClientReverbTxSize`       | Mapeo lineal. Define el tamaño de la sala modelada. La etiqueta se muestra como porcentaje.        |
| Decay               | 1.20 s               | 0.3 – 5.0 s | `ClientReverbTxDecayS`     | Mapeo exponencial (0.3 * (5.0/0.3)^n, ~16.7x). Etiqueta 'X.XX s'.                                 |
| Damp                | 50 %                 | 0 % – 100 % | `ClientReverbTxDamping`    | Mapeo lineal. Los valores más altos amortiguan las frecuencias altas más rápido en la cola. La etiqueta se muestra como porcentaje. |
| Pre                 | 20 ms                | 0 – 100 ms  | `ClientReverbTxPreDelayMs` | Mapeo lineal. Predelay entre la señal seca y las primeras reflexiones. Etiqueta 'X ms'.            |
| Mix                 | 15 %                 | 0 % – 100 % | `ClientReverbTxMix`        | Mapeo lineal. Balance seco/húmedo. La etiqueta se muestra como porcentaje.                         |
| Visualización de reverberación | —       | —           | —                          | ReverbVizBox — visualización en vivo que muestra el paquete de senoidal seca (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). 90 px de altura. |

## Visualización en vivo

El editor de Aetherial FreeVerb muestra un diagrama compacto en tiempo real (90 px de altura) sobre la fila de controles. Se actualiza inmediatamente conforme ajusta cualquier control y muestra tres elementos superpuestos:

| Elemento | Color | Qué representa |
|----------|-------|----------------|
| Paquete de senoidal seca | Cian, con degradado de desvanecimiento hacia la derecha | La señal no procesada que atraviesa |
| Reflexiones de primer orden | Amarillo | Reflexiones tempranas; espaciado definido por Size, amplitud por Mix y Damp |
| Cola reverberante | Magenta | La cola de reverberación completa; duración definida por Decay, brillo por Damp |

La visualización es puramente informativa. No afecta al procesamiento de audio.

### Cómo aparece Damp en la visualización

- Subir **Damp** hace que la cola magenta decaiga más abruptamente y reduce la amplitud de las ráfagas de reflexiones amarillas sucesivas.
- Bajar **Damp** produce una curva de decaimiento magenta más plana y amplitudes de reflexión amarilla más uniformes.

## Consejos

- Un valor alrededor del 50–70 % es adecuado para la mayoría de trabajos de voz. Suaviza la cola sin que la reverberación suene apagada.
- Si la cola suena opaca o poco definida, baje **Damp** hacia el 20–30 % para permitir que pase más contenido de alta frecuencia.
- **Damp** interactúa con **Decay**: una decadencia larga con bajo amortiguamiento produce una cola brillante y persistente que puede enmascarar el habla. Suba **Damp** si también sube Decay.
- Use la visualización en vivo para confirmar la interacción entre **Damp** y **Decay** antes de transmitir.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decaimiento a su gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Marque una mezcla sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ignore la reverberación desde la cadena](bypass-reverb-from-the-chain.md)

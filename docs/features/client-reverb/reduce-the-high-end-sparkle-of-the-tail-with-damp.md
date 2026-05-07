# Reduzca el brillo agudo de la cola con Damp

El control **Damp** determina la rapidez con que las frecuencias altas se desvanecen dentro de la cola de reverberación. Incrementarlo elimina el brillo aireado y chispeante que puede hacer que la reverberación de la voz suene poco natural en el aire.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. Si no lo está, el applet Aetherial FreeVerb está oculto y Damp no tiene efecto.
- El applet Aetherial FreeVerb o su editor flotante deben estar visibles. Consulte [Descripción general de Aetherial FreeVerb](overview.md) si aún no lo ha abierto.

## Pasos

1. Abra el editor de Aetherial FreeVerb haciendo doble clic en la etapa VERB del widget CHAIN. Se abre la ventana sin marco titulada "Aetherial FreeVerb — TX".
2. Localice el control **Damp** — el tercer control desde la izquierda en la fila de cinco controles.
3. Gire **Damp** en el sentido de las agujas del reloj para aumentar el amortiguamiento. Los valores más altos hacen que las frecuencias altas decaigan más rápido, reduciendo el brillo en la cola.
4. Gire **Damp** en el sentido contrario a las agujas del reloj para que las frecuencias altas persistan por más tiempo, produciendo una cola más brillante y abierta.
5. Suelte el control. El valor se guarda inmediatamente en `ClientReverbTxDamping`.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|---------|---------------------|-------|------------------|----------------|
| Damp | 50 % | 0 % – 100 % | `ClientReverbTxDamping` | Los valores más altos amortiguan las frecuencias altas más rápido en la cola de reverberación. Mapeo lineal. |

## Visualización en vivo

A partir de la versión v0.9.7, el editor de Aetherial FreeVerb muestra un diagrama compacto en tiempo real (90 px de alto) sobre la fila de controles. Se actualiza inmediatamente al ajustar cualquier control y muestra tres elementos superpuestos:

| Elemento | Color | Qué representa |
|----------|-------|----------------|
| Paquete de senoidal seco | Cian, con degradado hacia la derecha | La señal sin procesar que atraviesa |
| Primeras reflexiones | Amarillo | Reflexiones tempranas; espaciado determinado por Size, amplitud por Mix y Damp |
| Cola reverberante | Magenta | La cola de reverberación completa; duración determinada por Decay, brillo por Damp |

La visualización es puramente informativa. No afecta el procesamiento de audio.

### Cómo aparece Damp en la visualización

- Aumentar **Damp** hace que la cola magenta decaiga más abruptamente y reduce la amplitud de los estallidos de reflexión amarillos sucesivos.
- Reducir **Damp** produce una curva de decaimiento magenta más plana y amplitudes de reflexión amarillas más uniformes.

## Consejos

- Un valor de alrededor del 50-70 % funciona bien para la mayoría del trabajo con voz. Suaviza la cola sin que la reverberación suene apagada.
- Si la cola suena opaca o poco definida, reduzca **Damp** hacia el 20-30 % para dejar pasar más contenido de altas frecuencias.
- **Damp** interactúa con **Decay**: una cola larga con bajo amortiguamiento produce una reverberación brillante y persistente que puede enmascarar el habla. Aumente **Damp** si también aumenta Decay.
- Utilice la visualización en vivo para confirmar la interacción entre **Damp** y **Decay** antes de transmitir.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste el decaimiento al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Marque una mezcla sutil: lo típico para voz es del 10-15 %](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Ignore la reverberación desde la cadena](bypass-reverb-from-the-chain.md)

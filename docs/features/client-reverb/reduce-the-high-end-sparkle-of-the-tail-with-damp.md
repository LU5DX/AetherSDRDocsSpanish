# Reduzca el brillo agudo de la cola reverberante con Damp

El control **Damp** determina la velocidad con que las frecuencias altas se desvanecen en la cola de la reverberación. Subirlo elimina el brillo aireado que puede hacer que la reverberación de la voz suene poco natural al aire.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. De lo contrario, el applet Aetherial FreeVerb queda oculto y Damp no tiene efecto.
- El applet Aetherial FreeVerb o su editor flotante deben estar visibles. Consulte [Descripción general de Aetherial FreeVerb](overview.md) si aún no lo ha abierto.

## Pasos

1. Abra el editor de Aetherial FreeVerb haciendo doble clic en la etapa VERB del widget CHAIN. Se abrirá la ventana sin marco titulada "Aetherial FreeVerb — TX".
2. Localice el control **Damp** — el tercer control desde la izquierda en la fila de cinco mandos.
3. Gire **Damp** en el sentido de las agujas del reloj para aumentar la amortiguación. Los valores más altos hacen que las frecuencias altas decaigan más rápido, reduciendo el brillo en la cola.
4. Gire **Damp** en sentido contrario a las agujas del reloj para que las frecuencias altas persistan más tiempo, produciendo una cola más brillante y abierta.
5. Suelte el control. El valor se guarda inmediatamente en `ClientReverbTxDamping`.

## Qué hace cada control

| Control              | Valor predeterminado | Rango      | Clave de ajuste           | Notas                                                                                            |
|----------------------|----------------------|------------|---------------------------|--------------------------------------------------------------------------------------------------|
| Size                 | 50 %                 | 0 % – 100 % | `ClientReverbTxSize`      | Mapeo lineal. Define el tamaño de la sala modelada. La etiqueta se muestra como porcentaje.     |
| Decay                | 1,20 s               | 0,3 – 5,0 s | `ClientReverbTxDecayS`    | Mapeo exponencial (0,3 * (5,0/0,3)^n, ~16,7x). Etiqueta 'X,XX s'.                              |
| Damp                 | 50 %                 | 0 % – 100 % | `ClientReverbTxDamping`   | Mapeo lineal. Los valores más altos amortiguan las frecuencias altas más rápido en la cola. Etiqueta mostrada como porcentaje. |
| Pre                  | 20 ms                | 0 – 100 ms  | `ClientReverbTxPreDelayMs`| Mapeo lineal. Predelay entre la señal seca y las primeras reflexiones. Etiqueta 'X ms'.         |
| Mix                  | 15 %                 | 0 % – 100 % | `ClientReverbTxMix`       | Mapeo lineal. Balance seco/húmedo. Etiqueta mostrada como porcentaje.                           |
| Visualización de reverberación | —       | —           | —                         | ReverbVizBox — visualización en vivo que muestra el paquete de seno seco (cian), reflexiones de primer orden (amarillo) y cola reverberante (magenta). 90 px de alto. |

## Visualización en vivo

El editor de Aetherial FreeVerb muestra un diagrama compacto en tiempo real (90 px de alto) sobre la fila de mandos. Se actualiza inmediatamente al ajustar cualquier control y muestra tres elementos superpuestos:

| Elemento | Color | Qué representa |
|----------|-------|----------------|
| Paquete de seno seco | Cian, con degradado hacia la derecha | La señal sin procesar que atraviesa |
| Reflexiones de primer orden | Amarillo | Primeras reflexiones; espaciado definido por Size, amplitud por Mix y Damp |
| Cola reverberante | Magenta | La cola completa de reverberación; duración definida por Decay, brillo por Damp |

La visualización es meramente informativa. No afecta al procesamiento de audio.

### Cómo aparece Damp en la visualización

- Subir **Damp** hace que la cola magenta decaiga más abruptamente y reduce la amplitud de los sucesivos destellos de reflexión amarillos.
- Bajar **Damp** produce una curva de decaimiento magenta más plana y amplitudes de reflexión amarillas más uniformes.

## Temas y colores de los mandos

El applet Aetherial FreeVerb utiliza un contenedor de tema dedicado (`applet/reverb`) para sus componentes de mandos. Esto permite sobrescribir colores por applet. Los siguientes colores de los mandos provienen del sistema de temas:

| Clave del tema | Propósito |
|----------------|-----------|
| `color.knob.background` | Aro de fondo del mando |
| `color.knob.foreground` | Arco de valor que muestra el ajuste actual |
| `color.knob.handle` | Línea indicadora desde el centro al arco |
| `color.text.secondary` | Texto de la etiqueta debajo del mando |
| `color.text.primary` | Texto del valor mostrado en el centro del mando |

Si cambia de tema, los colores de los mandos se actualizan automáticamente. Los archivos de tema personalizados pueden asignar colores distintos al contenedor `applet/reverb` para que los mandos de reverberación se distingan visualmente de otros mandos de DSP.

## Consejos

- Un valor alrededor del 50–70 % funciona bien para la mayoría del trabajo con voz. Suaviza la cola sin que la reverberación suene apagada.
- Si la cola suena opaca o poco definida, baje **Damp** hacia el 20–30 % para dejar pasar más contenido de alta frecuencia.
- **Damp** interactúa con **Decay**: una decadencia larga con poca amortiguación produce una cola brillante y persistente que puede enmascarar el habla. Suba **Damp** si también sube Decay.
- Use la visualización en vivo para confirmar la interacción entre **Damp** y **Decay** antes de transmitir.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste la decadencia al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Marque una mezcla sutil — 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Evite la reverberación desde la cadena](bypass-reverb-from-the-chain.md)

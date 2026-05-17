# Reflejos desplazados de la señal seca con Pre

El control Pre añade un espacio entre la señal seca y el inicio de la cola de reverberación. Úselo para mantener su voz nítida y al frente mientras permite que la reverberación se despliegue detrás.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial FreeVerb o el editor flotante. Para abrir el editor, haga doble clic en la etapa VERB en el widget CHAIN; la ventana se titula "Aetherial FreeVerb — TX".

## Pasos

1. Localice el control Pre en la fila de cinco controles (Size, Decay, Damp, **Pre**, Mix).
2. Gire Pre en sentido horario para aumentar el retardo entre la señal seca y las primeras reflexiones, o en sentido antihorario para reducirlo.
3. Supervise la etiqueta debajo del control; muestra el valor en milisegundos (por ejemplo, `20 ms`).
4. Deténgase cuando la cola de reverberación se sienta separada de su voz sin sonar desconectada.

## Qué hace cada control

| Control             | Valor predeterminado                                                                                                                                                                                                                         | Rango válido                                                                                                |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Size                | 50 %                                                                                                                                                                                                                                         | 0.0 a 100 %                                                                                                 |
| Decay               | 1.20 s                                                                                                                                                                                                                                       | 0.3 a 5.0 s                                                                                                 |
| Damp                | 50 %                                                                                                                                                                                                                                         | 0.0 a 100 %                                                                                                 |
| Pre                 | 20 ms                                                                                                                                                                                                                                        | 0 a 100 ms                                                                                                  |
| Mix                 | 15 %                                                                                                                                                                                                                                         | 0.0 a 100 %                                                                                                 |
| Visualización de reverberación | ReverbVizBox: visualización en vivo que muestra el paquete de onda senoidal seca (cian), las reflexiones de primer orden (amarillo) y la cola reverberante (magenta). Los cinco valores de control alimentan la representación, por lo que la visualización sigue las ediciones de los controles en tiempo real. 90 px de alto. | Reemplaza el widget de curva utilizado por otros applets DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. |

## Edición de valor en línea

A partir de la versión v26.5.2.1, cada control admite la edición de valor en línea. Haga clic en la etiqueta de valor debajo de cualquier control (Size, Decay, Damp, Pre o Mix) para entrar en el modo de edición. La etiqueta se transforma en un campo de entrada de texto con un sutil fondo oscuro y borde cian para indicar que el editor está activo.

Escriba un valor numérico y presione Enter para confirmar el cambio. El valor se ajusta automáticamente al rango válido del control. Presione Escape o haga clic en otro lugar para aplicar la edición y volver al modo de visualización normal.

Para editar el valor de un control mediante el editor en línea:

1. Haga clic en la etiqueta de valor debajo del control. La etiqueta se convierte en un campo de texto editable con borde cian.
2. Escriba el valor deseado. El análisis compatible con la configuración regional admite tanto el punto como la coma como separadores decimales (por ejemplo, `25.5` o `25,5`).
3. Presione Enter para aplicar el valor. El control se actualiza para coincidir y la etiqueta vuelve a su apariencia predeterminada.
4. Para cancelar sin cambiar el valor, presione Escape.

El editor en línea está siempre disponible cuando el applet está abierto. No se requiere configuración para habilitarlo o deshabilitarlo.

## Visualización en vivo

A partir de la versión v0.9.7, el applet Aetherial FreeVerb incluye un diagrama de reverberación en tiempo real que se muestra encima de la fila de controles. La visualización es un panel compacto de 90 píxeles de alto con fondo oscuro y líneas de cuadrícula. Se actualiza inmediatamente cuando mueve cualquiera de los cinco controles.

El diagrama muestra tres capas de forma de onda superpuestas:

- **Cian — señal seca.** Un paquete de onda senoidal que representa el audio sin procesar. Su amplitud disminuye a medida que se aumenta Mix, lo que refleja el cambio hacia la señal húmeda.
- **Amarillo — reflexiones de primer orden.** Una serie de ráfagas de onda senoidal cortas que comienzan después del espacio de pre-retardo. Su separación se amplía a medida que aumenta Size, y su amplitud disminuye más rápido a medida que aumenta Damp.
- **Magenta — cola reverberante.** Una oscilación de decrecimiento exponencial que comienza en el mismo desplazamiento que las reflexiones. Su extensión horizontal crece con Decay, y los valores más altos de Damp hacen que la amplitud de la cola se colapse más rápidamente.

La posición en la que comienzan las capas amarilla y magenta se desplaza hacia la derecha a medida que aumenta Pre, mostrando directamente el espacio entre la señal seca y las primeras reflexiones.

No se requiere configuración. La visualización siempre está visible cuando el applet está abierto y la etapa Reverb está activa.

## Consejos

- Un valor de Pre de 0 ms hace que las reflexiones comiencen inmediatamente, lo que puede difuminar los transitorios. Los valores en el rango de 15 a 30 ms son comunes para la voz y ayudan a preservar la inteligibilidad.
- Pre interactúa con Decay: un Pre corto con un Decay largo puede hacer que la cola parezca comenzar antes de lo esperado. Aumente Pre si la reverberación parece engullir el borde inicial de las palabras.
- Tanto el control del applet compacto (etiquetado como Pre) como el control del editor flotante controlan el mismo ajuste `ClientReverbTxPreDelayMs` y se mantienen sincronizados.
- Use la visualización en vivo para confirmar que las ráfagas de reflexión amarillas comiencen claramente a la derecha del paquete seco cian. Si las dos capas parecen superponerse, aumente Pre.
- Use la edición de valor en línea para escribir un valor de Pre preciso en lugar de girar el control. Esto es especialmente útil cuando se busca coincidir con un ajuste de milisegundos específico.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste de Decay al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Marque un Mix sutil: 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omitir la reverberación desde la cadena](bypass-reverb-from-the-chain.md)

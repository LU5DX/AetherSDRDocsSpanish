# Desplazamiento de las reflexiones de la señal seca con Pre

El control Pre añade un intervalo entre la señal seca y el inicio de la cola de reverberación. Úselo para mantener su voz nítida y al frente mientras permite que la reverberación se desarrolle detrás.

## Antes de comenzar

- La etapa Reverb debe estar habilitada en el widget CHAIN. La applet permanece oculta hasta que la etapa esté activa.
- Abra la applet Aetherial FreeVerb o el editor flotante. Para abrir el editor, haga doble clic en la etapa VERB en el widget CHAIN; la ventana se titula "Aetherial FreeVerb — TX".

## Pasos

1. Localice el control Pre en la fila de cinco controles (Size, Decay, Damp, **Pre**, Mix).
2. Gire Pre en sentido horario para aumentar el retardo entre la señal seca y las primeras reflexiones, o en sentido antihorario para reducirlo.
3. Supervise la etiqueta debajo del control; muestra el valor en milisegundos (por ejemplo, `20 ms`).
4. Deténgase cuando la cola de reverberación se sienta separada de su voz sin sonar desconectada.

## Función de cada control

| Control              | Valor predeterminado                                                                                                                                                                                                                       | Rango válido                                                                                               |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Size                 | 50 %                                                                                                                                                                                                                                       | 0.0 a 100 %                                                                                                |
| Decay                | 1.20 s                                                                                                                                                                                                                                     | 0.3 a 5.0 s                                                                                                |
| Damp                 | 50 %                                                                                                                                                                                                                                       | 0.0 a 100 %                                                                                                |
| Pre                  | 20 ms                                                                                                                                                                                                                                      | 0 a 100 ms                                                                                                 |
| Mix                  | 15 %                                                                                                                                                                                                                                       | 0.0 a 100 %                                                                                                |
| Visualización de reverberación | ReverbVizBox — visualización en vivo que muestra el paquete de onda sinusoidal seca (cian), las reflexiones de primer orden (amarillo) y la cola reverberante (magenta). Los valores de los cinco controles alimentan la representación, por lo que la visualización sigue las ediciones de los controles en tiempo real. 90 píxeles de alto. | Reemplaza el widget de curva utilizado por otras applets de DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. |

## Edición de valor en línea

A partir de la versión v26.5.2.1, cada control admite la edición de valor en línea. Haga clic en la etiqueta de valor debajo de cualquier control (Size, Decay, Damp, Pre o Mix) para ingresar al modo de edición. La etiqueta se transforma en un campo de entrada de texto con un sutil fondo oscuro y un borde cian que indica que el editor está activo.

Escriba un valor numérico y presione Enter para confirmar el cambio. El valor se ajusta automáticamente al rango válido del control. Presione Escape o haga clic en otro lugar para aplicar la edición y volver al modo de visualización normal.

Para editar un valor de control usando el editor en línea:

1. Haga clic en la etiqueta de valor debajo del control. La etiqueta se convierte en un campo de texto editable con un borde cian.
2. Escriba el valor deseado. El análisis compatible con la configuración regional admite tanto el punto como la coma como separadores decimales (por ejemplo, `25.5` o `25,5`).
3. Presione Enter para aplicar el valor. El control se actualiza para coincidir y la etiqueta vuelve a su apariencia predeterminada.
4. Para cancelar sin cambiar el valor, presione Escape.

El editor en línea está siempre disponible cuando la applet está abierta. No se requiere configuración para habilitarlo o deshabilitarlo.

## Visualización en vivo

A partir de la versión v0.9.7, la applet Aetherial FreeVerb incluye un diagrama de reverberación en tiempo real que se muestra encima de la fila de controles. La visualización es un panel compacto de 90 píxeles de alto con un fondo oscuro y líneas de cuadrícula. Se actualiza inmediatamente cuando mueve cualquiera de los cinco controles.

El diagrama muestra tres capas de forma de onda superpuestas:

- **Cian — señal seca.** Un paquete de onda sinusoidal que representa el audio no procesado. Su amplitud disminuye a medida que se aumenta Mix, lo que refleja el cambio hacia la señal procesada.
- **Amarillo — reflexiones de primer orden.** Una serie de ráfagas de onda sinusoidal cortas que comienzan después del intervalo de pre-retardo. Su espaciado se amplía a medida que aumenta Size, y su amplitud se desvanece más rápido a medida que aumenta Damp.
- **Magenta — cola reverberante.** Una oscilación que decae exponencialmente y comienza en el mismo desplazamiento que las reflexiones. Su extensión horizontal crece con Decay, y los valores más altos de Damp hacen que la amplitud de la cola se colapse más rápidamente.

La posición en la que comienzan las capas amarilla y magenta se desplaza hacia la derecha a medida que aumenta Pre, lo que muestra directamente el intervalo entre la señal seca y las primeras reflexiones.

No se requiere configuración. La visualización está siempre visible cuando la applet está abierta y la etapa Reverb está activa.

## Consejos

- Un valor de Pre de 0 ms hace que las reflexiones comiencen de inmediato, lo que puede difuminar los transitorios. Los valores en el rango de 15–30 ms son comunes para la voz a fin de preservar la inteligibilidad.
- Pre interactúa con Decay: un Pre corto con un Decay largo puede hacer que la cola parezca comenzar antes de lo esperado. Aumente Pre si la reverberación parece engullir el borde inicial de las palabras.
- Tanto el control de la applet compacta (etiquetado Pre) como el control del editor flotante ajustan la misma configuración `ClientReverbTxPreDelayMs` y se mantienen sincronizados.
- Use la visualización en vivo para confirmar que las ráfagas de reflexión amarillas comiencen claramente a la derecha del paquete seco cian. Si las dos capas parecen superponerse, aumente Pre.
- Use la edición de valor en línea para escribir un valor Pre preciso en lugar de girar el control. Esto es especialmente útil cuando se debe coincidir con un ajuste de milisegundos específico.

## Colores

A partir de la versión v26.6.1, los colores de los controles en la applet Aetherial FreeVerb son impulsados por la configuración del tema en lugar de valores codificados. Las entradas `color.knob.background`, `color.knob.foreground` y `color.knob.handle` en el tema activo controlan el fondo del anillo, el arco de valor y el puntero respectivamente. Las entradas `color.text.primary` y `color.text.secondary` controlan el texto del valor y la etiqueta debajo de cada control. El contenedor de la applet se establece en el espacio de nombres de color `applet/reverb`, lo que permite anulaciones de color por applet en temas personalizados. Los temas predeterminados proporcionan una apariencia consistente y de alto contraste para todos los controles.

## Relacionados

- [Descripción general de Aetherial FreeVerb](overview.md)
- [Ajuste la caída al gusto sin enturbiar el habla](tune-decay-to-taste-without-muddying-speech.md)
- [Marque una Mezcla sutil: 10-15 % es típico para la voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)

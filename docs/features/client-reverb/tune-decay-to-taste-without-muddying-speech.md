# Ajuste la caída al gusto sin opacar la voz

El control **Decay** determina cuánto tiempo persiste la cola de reverberación después de cada sílaba. Un valor demasiado alto difumina el habla; en esta página se muestra cómo encontrar un valor que añada presencia sin perjudicar la inteligibilidad.

## Antes de empezar

- La etapa Reverb debe estar habilitada en el widget CHAIN. El subcontenedor "Aetherial FreeVerb" permanece oculto hasta que la etapa esté activa.
- Abra los controles de reverberación: localice el subcontenedor "Aetherial FreeVerb" dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets, o haga doble clic en la etapa VERB del widget CHAIN para abrir el editor flotante titulado "Aetherial FreeVerb — TX".

## Pasos

1. Localice el control **Decay**. Muestra un valor en el formato `X.XX s`.
2. Gire **Decay** hacia abajo, hasta aproximadamente `0.30 s`, y transmita una muestra de voz. En este extremo, la cola es apenas audible.
3. Aumente lentamente **Decay** mientras habla o monitorea una grabación. Deténgase cuando la cola se vuelva audible entre las sílabas.
4. Reduzca ligeramente hasta que las sílabas ya no se difuminen entre sí. Para la mayoría de los trabajos de voz, los valores en el rango de `0.5 s` a `1.5 s` mantienen el habla clara.
5. Si la cola aún suena opaca, aumente **Damp** para atenuar la energía de alta frecuencia en la cola, lo que a menudo reduce la percepción de borrosidad sin acortar más el Decay.
6. Verifique que **Mix** no esté ajustado demasiado alto. Un Mix de `10 %` a `15 %` es típico para voz; una señal wet excesiva amplifica el efecto de cualquier valor de Decay.

## Qué hace cada control

| Etiqueta            | Valor predeterminado                                                                                                                                                                                                                         | Rango                                                                                                       |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Size                | 50 %                                                                                                                                                                                                                                         | 0.0 a 1.0 (mostrado como %)                                                                                 |
| Decay               | 1.20 s                                                                                                                                                                                                                                       | 0.3 a 5.0 s                                                                                                |
| Damp                | 50 %                                                                                                                                                                                                                                         | 0.0 a 1.0 (mostrado como %)                                                                                 |
| Pre                 | 20 ms                                                                                                                                                                                                                                        | 0 a 100 ms                                                                                                 |
| Mix                 | 15 %                                                                                                                                                                                                                                         | 0.0 a 1.0 (mostrado como %)                                                                                 |
| Visualización de reverberación | ReverbVizBox: visualización en vivo que muestra el paquete de seno seco (cian), las reflexiones de primer orden (amarillo) y la cola reverberante (magenta). Los cinco valores de control alimentan la representación, por lo que la visualización sigue las ediciones de los controles en tiempo real. 90 px de alto. | Reemplaza el widget de curva utilizado por otros applets DSP. El algoritmo de representación coincide con StripReverbPanel::GridBox. |

## Visualización en vivo

El panel de applets y el editor flotante "Aetherial FreeVerb — TX" muestran un diagrama de ondas compacto (90 px de alto) que se actualiza en tiempo real mientras mueve cualquier control. El diagrama utiliza tres capas codificadas por colores:

- **Cian** — el paquete de señal seca, con degradado hacia la derecha. Su amplitud disminuye a medida que aumenta Mix.
- **Amarillo** — reflexiones de primer orden. El espaciado y la cantidad responden a Size; la amplitud por reflexión disminuye con valores más altos de Damp.
- **Magenta** — la cola reverberante. Su longitud horizontal refleja Decay, su atenuación de alta frecuencia refleja Damp y su amplitud general refleja Mix.

La visualización es solo orientativa; no representa una medición precisa de respuesta al impulso. Use sus oídos para realizar los ajustes finales.

## Edición directa de valores en los controles

A partir de la versión v26.5.2.1, cualquier control en "Aetherial FreeVerb — TX" se puede editar escribiendo un valor numérico en lugar de girar el control.

1. Haga clic en el valor numérico que se muestra debajo de un control. El valor se convierte en un campo de texto editable con un borde cian.
2. Escriba el valor deseado. Puede incluir unidades o caracteres adicionales; el editor los elimina automáticamente. Por ejemplo, `1.5` o `1.5 s` configuran Decay en `1.50 s`.
3. Presione Enter o haga clic fuera del editor para confirmar el valor. El control se actualiza y el editor vuelve a su apariencia de etiqueta.
4. Presione Escape para cancelar la edición y restaurar el valor anterior.

La edición en línea respeta la configuración regional: en regiones que usan coma como separador decimal (como `1,5`), el editor lo interpreta correctamente.

## Consejos

- Debido a que Decay utiliza un mapeo exponencial, el control es mucho más sensible en el extremo inferior de su recorrido. Realice ajustes pequeños cuando trabaje por debajo de `1.0 s`.
- Los controles del applet y el editor flotante "Aetherial FreeVerb — TX" se mantienen sincronizados a aproximadamente 30 Hz. Los ajustes realizados en uno se reflejan inmediatamente en el otro.
- Haga doble clic en el control **Decay** para restablecerlo al valor predeterminado de `1.20 s`.

## Solución de problemas

- **El habla suena opaca incluso con valores cortos de Decay** — Verifique **Mix**. Si Mix está por encima de `30 %`, la señal wet domina independientemente de la longitud de la cola. Reduzca Mix a `10–15 %` primero, luego reevalúe Decay.
- **El control Decay no tiene efecto audible** — Es posible que la etapa Reverb no esté habilitada. Confirme que la etapa VERB esté activa en el widget CHAIN. El applet está oculto y el procesador está desviado cuando la etapa está desactivada.

## Relacionados

- [Resumen de Aetherial FreeVerb](overview.md)
- [Reduzca el brillo agudo de la cola con Damp](reduce-the-high-end-sparkle-of-the-tail-with-damp.md)
- [Ajuste un Mix sutil: 10-15 % es típico para voz](dial-in-a-subtle-mix-10-15-is-typical-for-voice.md)
- [Omita la reverberación desde la cadena](bypass-reverb-from-the-chain.md)

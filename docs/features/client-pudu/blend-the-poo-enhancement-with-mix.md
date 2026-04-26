# Combinar la mejora Poo con Mix

El mando **Poo / Mix** controla qué proporción de la señal de baja frecuencia procesada se mezcla con el audio seco. Úselo para incorporar la justa cantidad de mejora Poo sin saturar su señal de transmisión.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Si el applet PUDU no es visible, habilite la etapa PUDU (Enh) a través del widget CHAIN o haga doble clic en él para abrir el editor flotante.
- El motor de audio debe estar en funcionamiento con una fuente de audio de transmisión activa para poder escuchar el efecto de la mezcla.

## Pasos

1. Abra el subcontenedor PUDU dentro del contenedor padre PooDoo Audio (TXDSP) en el panel de applets.
2. Localice el grupo **Poo** — los tres mandos bajo el corchete etiquetado **Poo**.
3. Gire el tercer mando del grupo Poo, etiquetado **Mix**, para ajustar la mezcla húmedo/seco del procesador de baja frecuencia.
   - Girar a la izquierda hacia 0 % deja pasar solo la señal seca.
   - Girar a la derecha hacia 100 % deja pasar solo la señal de banda baja procesada.
4. Suelte el mando. El valor se guarda automáticamente en `ClientPuduTxPooMix`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Poo / Mix | 30 % | 0 % a 100 % (interno 0.0 a 1.0) | `ClientPuduTxPooMix` |

El mando utiliza una correspondencia lineal. La etiqueta mostrada indica la mezcla como un porcentaje en número entero (por ejemplo, **30 %**).

## Consejos

- Comience en el valor predeterminado de 30 % y aumente lentamente. En valores altos, la saturación de banda baja puede añadir un peso significativo; incrementos pequeños producen un efecto audible.
- El logotipo de PooDoo pulsa con mayor brillo a medida que aumenta el nivel RMS húmedo (procesado) — úselo como guía visual cuando no pueda monitorear el audio directamente.
- Ajuste Poo / Drive y Poo / Tune a valores apropiados antes de fijar un nivel de Mix. El carácter de la señal que se está mezclando depende de esos dos mandos.

## Solución de problemas

- **Girar Poo / Mix no produce efecto audible** — confirme que la etapa PUDU está habilitada en el widget CHAIN y no está puenteada. Si la etapa está puenteada, los tres mandos Poo no tienen efecto en la salida.
- **Mix vuelve a su posición anterior tras el ajuste** — es posible que el motor de audio no esté conectado. Verifique que AetherSDR esté conectado al FLEX-8600 y que la ruta de audio TX esté activa.

## Temas relacionados

- [Descripción general del excitador PUDU](overview.md)
- [Ajustar Poo Drive para el grosor de baja frecuencia](dial-poo-drive-for-lf-thickness.md)
- [Ajustar Poo al fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Combinar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Puentear PUDU desde la cadena](bypass-pudu-from-the-chain.md)

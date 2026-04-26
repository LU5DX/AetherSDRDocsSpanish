# Combinar la excitación Doo con Mix

Use el control Doo / Mix para determinar cuánta excitación de alta frecuencia del Doo se mezcla de vuelta en su señal de transmisión. Un valor más bajo mantiene el efecto sutil; un valor más alto hace que la mejora de presencia y aire sea más prominente.

## Antes de comenzar

- El applet PUDU Exciter debe estar visible. Permanece oculto hasta que la etapa PUDU se habilite mediante el widget CHAIN o el editor flotante de PUDU.
- El motor de audio debe estar en funcionamiento y conectado a la cadena de transmisión para que los cambios surtan efecto en tiempo real.

## Pasos

1. Localice el applet PUDU Exciter en el contenedor principal PooDoo Audio (TXDSP).
2. Encuentre el grupo **Doo** — los tres controles giratorios bajo la etiqueta del corchete derecho.
3. Gire el tercer control de ese grupo, etiquetado **Mix**, para establecer la mezcla wet/dry de la etapa Doo.
4. Observe el indicador de valor bajo el control. Muestra un porcentaje (por ejemplo, `30 %`).
5. Suelte el control. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Doo / Mix | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduTxDooMix` | Mezcla linealmente la señal de alta frecuencia procesada con la señal seca. 0 % no aplica ningún efecto Doo; 100 % pasa únicamente la señal procesada. |

## Consejos

- Comience con el valor predeterminado de 30 % y auméntelo gradualmente mientras transmite hacia una carga dummy o monitorea su audio de TX. El logotipo de PooDoo pulsa con el RMS de la señal wet, proporcionando una indicación visual de cuánta señal procesada está presente.
- Doo / Mix funciona junto con Doo / Air (`ClientPuduTxDooHarmonicsDb`). Si Air está configurado bajo, subir Mix tendrá poco efecto audible. Ajuste Air primero y luego use Mix al gusto.
- Valores de Mix muy altos pueden hacer que el efecto suene duro en SSB. Los valores entre 20 % y 50 % son típicos para uso de voz.

## Relacionado

- [Agregar aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
- [Combinar la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Descripción general del PUDU Exciter](overview.md)

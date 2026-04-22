# Mezcle el efecto Doo con Mix

Use el control Doo / Mix para ajustar cuánto de la señal excitada de alta frecuencia se mezcla de vuelta con su audio seco. Un valor bajo agrega presencia sutil; un valor alto lleva el efecto Doo más al frente.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Si el applet PUDU no es visible, consulte [Omitir PUDU de la cadena](bypass-pudu-from-the-chain.md).
- Abra el applet PUDU Exciter. Aparece en el subcontenedor PUDU dentro del contenedor principal PooDoo Audio (TXDSP). También puede hacer doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante de PUDU.

## Pasos

1. Ubique el grupo **Doo** — los tres controles en el lado derecho del applet PUDU, bajo la etiqueta de corchete **Doo**.
2. Encuentre el tercer control del grupo Doo, etiquetado como **Mix**.
3. Gire **Mix** para ajustar la mezcla wet/dry. El control muestra el valor actual como porcentaje (por ejemplo, `30 %`).
4. Suelte el control. La configuración se guarda automáticamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| **Doo / Mix** | 30 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientPuduTxDooMix` |

## Consejos

- Comience en el valor predeterminado de `30 %` y auméntelo gradualmente mientras transmite. El logotipo de PooDoo pulsa con mayor brillo a medida que sube el nivel de la señal procesada (wet), lo que ofrece una indicación visual de cuánto efecto está presente.
- Doo / Mix funciona junto con **Doo / Air** y **Doo / Tune**. Ajuste primero la frecuencia y la cantidad de armónicos correctos, y luego use Mix para establecer la mezcla final. Consulte [Agregar aire con Doo Harmonics](add-air-with-doo-harmonics.md) y [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md).
- Fijar Mix en `0 %` omite efectivamente la sección Doo sin modificar ningún otro parámetro.

## Relacionados

- [Agregar aire con Doo Harmonics](add-air-with-doo-harmonics.md)
- [Centrar Doo en la banda de presencia de su micrófono](centre-doo-on-the-presence-band-for-your-mic.md)
- [Mezclar la mejora Poo con Mix](blend-the-poo-enhancement-with-mix.md)
- [Descripción general de PUDU Exciter](overview.md)

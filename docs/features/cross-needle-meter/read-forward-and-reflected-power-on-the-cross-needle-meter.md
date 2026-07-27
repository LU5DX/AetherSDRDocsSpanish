# Lectura de potencia directa y reflejada en el medidor de agujas cruzadas

Visualice la potencia RF directa, la potencia reflejada y la ROE simultáneamente en una pantalla de medidor de agujas cruzadas de estilo analógico, con lecturas digitales opcionales para valores precisos.

## Antes de comenzar

- La radio debe estar conectada y transmitiendo o recibiendo una señal para mostrar lecturas significativas.
- El applet Cross-Needle Meter debe estar abierto. Ábralo desde **Applet panel > Cross-Needle tile**.

## Pasos

1. Abra el applet Cross-Needle Meter (si aún no está visible).
2. Observe las dos agujas que se cruzan:
   - **Potencia directa** — indicada por la aguja derecha.
   - **Potencia reflejada** — indicada por la aguja izquierda.
   - El punto donde se cruzan las agujas indica la **ROE** en la escala curva de ROE.
3. (Opcional) Lea los valores numéricos debajo de la cara del medidor:
   - Potencia **directa** en vatios.
   - Potencia **reflejada** en vatios.
   - **ROE** como una relación.
4. (Opcional) Haga clic en **Peak hold** para congelar la aguja en su deflexión máxima — útil para leer los picos de voz en SSB.
5. (Opcional) Use el cuadro combinado **Meter face theme** para cambiar el estilo de la cara del medidor.

## Función de cada control

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---------|------|----------------|------------------------|----------------|
| Agujas de potencia directa/reflejada | indicador | — | — | Pantalla analógica de doble aguja: potencia directa (aguja derecha) y potencia reflejada (aguja izquierda) que se cruzan para indicar la ROE. |
| Peak hold | botón de alternancia | Off | — | Mantiene la posición máxima de la aguja para facilitar la lectura durante los picos de voz en SSB. |
| Lectura digital | indicador | — | — | Valores numéricos de potencia directa, potencia reflejada y ROE mostrados debajo del medidor. |
| Meter face theme | cuadro combinado | — | — | Seleccione entre estilos predefinidos de cara de medidor (negro clásico, blanco, militar, etc.). |

## Consejos

- El medidor de agujas cruzadas es más informativo durante portadora continua (CW, AM, FM) o habla SSB estable. En SSB, use **Peak hold** para capturar los picos de voz.
- Para mediciones precisas de ROE, transmita una portadora continua y lea el punto de cruce de las dos agujas.

## Relacionados

- [Resumen](overview.md)
- [Activar peak-hold para picos de voz en SSB](enable-peak-hold-for-ssb-voice-peaks.md)
- [Cambiar el tema de la cara del medidor](change-the-meter-face-theme.md)

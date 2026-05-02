# Leer el medidor de nivel de salida en el applet Tube

El medidor de nivel de salida dentro del applet Tube muestra el nivel de señal de pico después de la etapa de saturación de tubo. Úselo para confirmar que su salida es suficientemente alta para ser útil y para detectar niveles cercanos al recorte (clipping).

## Antes de comenzar

- El applet Tube debe estar visible. Aparece como "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) dentro del contenedor principal Aetherial Audio (TXDSP). Si el applet está oculto, habilite la etapa Tube mediante el widget CHAIN en el lado correspondiente.
- No se requiere conexión de radio para leer el medidor.

## Pasos

1. Localice el applet Tube del lado que desea monitorear: "Aetherial Mic-PreAmp" para TX o "Aetherial Dynamic Tube" para RX.
2. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor sin marco titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
3. Encuentre el medidor vertical etiquetado **OUT** en el extremo derecho del editor, a la derecha de las columnas de mandos.
4. Pase audio a través de la etapa (transmita o reciba una señal). La barra de color sube y baja con el nivel de pico de salida.
5. Lea el color y la posición relativa de la barra para evaluar el nivel de operación. Consulte las tablas a continuación para conocer los umbrales de color.

## Qué hace cada control

| Elemento | Qué muestra | Rango | Notas |
|---|---|---|---|
| **OUT** (etiqueta de encabezado) | Identifica el medidor como la salida posterior a la saturación | — | Etiqueta estática; establecida por el applet Tube. |
| Barra de nivel | Nivel de pico con código de color por nivel | −60 dB (abajo) a 0 dB (arriba) | Balística de ataque rápido / liberación lenta. |
| Marcas de escala en dB | Líneas de referencia estáticas a 0, −6, −12, −20 y −40 dB | — | Las líneas de marca se extienden desde la columna de etiquetas hasta la barra. |

### Significado de los colores

| Color de la barra | Rango de nivel | Significado |
|---|---|---|
| Verde | −60 a −12 dB | Muy alejado del recorte. |
| Verde lima | −12 a −6 dB | Se acerca a niveles moderados. |
| Ámbar | −6 a −3 dB | Cerca del recorte; observe el mando Output. |
| Rojo | Por encima de −3 dB | A menos de 3 dB del recorte. Reduzca Drive u Output. |

## Consejos

- El medidor utiliza balística de ataque rápido / liberación lenta: los picos transitorios breves se capturan rápidamente, pero la barra no baja de forma instantánea. Las excursiones breves al rojo pueden representar picos cortos aunque la barra permanezca allí momentáneamente.
- El medidor solo es visible en el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX"). No aparece en el panel del applet acoplado.
- Si la barra se encuentra regularmente en el rojo, reduzca el mando **Output** (rango −24.0 a 12.0 dB, valor predeterminado 0.00 dB) para bajar el nivel posterior a la saturación sin modificar el carácter de la saturación.
- Si la barra apenas se mueve desde la parte inferior, aumente **Drive** (rango 0.0 a 24.0 dB, valor predeterminado 0.00 dB) para introducir más señal en la etapa de tubo y elevar la lectura de salida.

## Relacionados

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)

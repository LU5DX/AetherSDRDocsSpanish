# Lectura del medidor de nivel de salida en el applet Tube

El medidor de nivel de salida dentro del applet Tube muestra el nivel máximo de la señal después de la etapa de saturación del tubo. Úselo para confirmar que su salida es lo suficientemente alta como para ser útil y para detectar niveles cercanos al recorte.

## Antes de comenzar

- El applet Tube debe estar visible. Aparece como "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) dentro del contenedor principal Aetherial Audio (TXDSP). Si el applet está oculto, habilite la etapa Tube mediante el widget CHAIN en el lado correspondiente.
- No se requiere conexión de radio para leer el medidor.

## Pasos

1. Localice el applet Tube para el lado que desea monitorear: "Aetherial Mic-PreAmp" para TX o "Aetherial Dynamic Tube" para RX.
2. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor sin marco titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
3. Encuentre el medidor vertical etiquetado como **OUT** en el extremo derecho del editor, a la derecha de las columnas de perillas.
4. Pase audio a través de la etapa (transmita o reciba una señal). La barra de color sube y baja con el nivel máximo de salida.
5. Lea el color y la posición relativa de la barra para evaluar el nivel de operación. Consulte las tablas a continuación para conocer los umbrales de color.

## Descripción de cada control

| Elemento | Qué muestra | Rango | Notas |
|---|---|---|---|
| **OUT** (etiqueta de encabezado) | Identifica el medidor como la salida posterior a la saturación | — | Etiqueta estática; establecida por el applet Tube. |
| Barra de nivel | Relleno de nivel máximo, codificado por colores según el nivel | −60 dB (inferior) a 0 dB (superior) | Balística de ataque rápido / caída lenta. |
| Marcas de escala en dB | Líneas de referencia estáticas en 0, −6, −12, −20 y −40 dB | — | Las líneas se extienden desde la columna de etiquetas hasta la barra. |

### Significado de los colores

| Color de la barra | Rango de nivel | Significado |
|---|---|---|
| Verde | −60 a −12 dB | Muy lejos del recorte. |
| Lima | −12 a −6 dB | Acercándose a niveles moderados. |
| Ámbar | −6 a −3 dB | Cada vez más cerca del recorte; vigile el control Output. |
| Rojo | Por encima de −3 dB | A menos de 3 dB del recorte. Reduzca Drive u Output. |

## Consejos

- El medidor utiliza balística de ataque rápido / caída lenta: los picos transitorios breves se capturan rápidamente, pero la barra no cae de inmediato. Las incursiones breves en la zona roja pueden representar picos cortos, incluso si la barra permanece allí momentáneamente.
- El medidor solo es visible en el editor flotante ("Aetherial Tube — TX" o "Aetherial Tube — RX"). No aparece en el mosaico acoplado del applet.
- Si la barra se sitúa con frecuencia en la zona roja, reduzca el control **Output** (rango −24.0 a 12.0 dB, valor predeterminado 0.00 dB) para bajar el nivel posterior a la saturación sin cambiar el carácter de saturación.
- Si la barra apenas se mueve desde la parte inferior, aumente **Drive** (rango 0.0 a 24.0 dB, valor predeterminado 0.00 dB) para enviar más señal a la etapa de tubo y elevar la lectura de salida.

## Relacionados

- [Visión general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajuste Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)

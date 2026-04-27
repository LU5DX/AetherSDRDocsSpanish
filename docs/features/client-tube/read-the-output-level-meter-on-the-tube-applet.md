# Leer el medidor de nivel de salida en el applet Tube

El medidor de nivel de salida dentro del applet Tube muestra el nivel de pico suavizado de la señal después de la etapa de saturación de tubo. Úselo para confirmar que su señal de salida es suficientemente fuerte para ser útil y para detectar niveles que se acercan al recorte (clipping).

## Antes de comenzar

- El applet Tube debe estar visible. Aparece como "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) dentro del contenedor principal Aetherial Audio (TXDSP). Si el applet está oculto, habilite la etapa Tube mediante el widget CHAIN del lado correspondiente.
- No se requiere conexión de radio para leer el medidor.

## Pasos

1. Localice el applet Tube para el lado que desea monitorear: "Aetherial Mic-PreAmp" para TX o "Aetherial Dynamic Tube" para RX.
2. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor sin marcos titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
3. Encuentre el medidor vertical a la derecha de la curva de saturación. Su etiqueta de encabezado muestra **OUT**.
4. Pase audio por la etapa (transmita o reciba una señal). La barra de color sube y baja con el nivel de pico de salida suavizado.
5. Lea el nivel exacto en el indicador numérico debajo de la barra. El valor se muestra como una cifra en dB con signo y un decimal (por ejemplo, `−4.3 dB`). Por debajo de aproximadamente −59.5 dB, el indicador muestra `-inf`.

## Qué hace cada control

| Elemento | Qué muestra | Rango | Notas |
|---|---|---|---|
| **OUT** (etiqueta de encabezado) | Identifica el medidor como la salida posterior a la saturación | — | Etiqueta estática; establecida por el applet Tube. |
| Barra de nivel | Relleno de pico suavizado, codificado por color según el nivel | −60 dB (fondo) a 0 dB (tope) | Ataque rápido (alpha = 0.6), liberación lenta (alpha = 0.08). |
| Marcas de escala en dB | Líneas de referencia estáticas en 0, −6, −12, −20 y −40 dB | — | Las líneas de marca se extienden desde la columna de etiquetas sobre la barra. |
| Indicador numérico | Pico suavizado como valor en dB con signo | `-inf` o un valor con signo y un decimal | Muestra `-inf` por debajo de aproximadamente −59.5 dB. |

### Significado de los colores

| Color de la barra | Rango de nivel | Significado |
|---|---|---|
| Verde | −60 a −12 dB | Bien alejado del recorte. |
| Verde lima | −12 a −6 dB | Acercándose a niveles moderados. |
| Ámbar | −6 a −3 dB | Cercano al recorte; observe el control Output. |
| Rojo | Por encima de −3 dB | A menos de 3 dB del recorte. Reduzca Drive u Output. |

## Consejos

- El medidor utiliza la misma dinámica de ataque rápido / liberación lenta que el medidor del fader de salida del EQ, por lo que los picos transitorios breves se capturan rápidamente, pero la barra no cae de inmediato — las incursiones breves en el rojo pueden representar picos cortos aunque la barra tarde en bajar.
- Si la barra permanece en el rojo con regularidad, reduzca el control Output (rango −24.0 a 12.0 dB, valor predeterminado 0.0 dB) para bajar el nivel posterior a la saturación sin modificar el carácter de la saturación.
- Si la barra apenas se mueve del fondo, aumente Drive (rango 0.0 a 24.0 dB, valor predeterminado 0.0 dB) para introducir más señal en la etapa de tubo y elevar la lectura de salida.

## Relacionado

- [Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)](overview.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Ajustar Drive hasta que la curva comience a curvarse (calidez en TX o moldeado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)

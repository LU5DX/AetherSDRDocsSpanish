# Lea el medidor de nivel de salida en el applet Tube

El Medidor de Nivel de Salida en el applet Tube muestra el nivel máximo post-saturación suavizado de su señal de audio. Úselo para confirmar que la etapa Tube no está recortando su salida y para juzgar cuánto margen queda después de aplicar la ganancia de entrada y salida.

## Antes de comenzar

- El applet Tube debe estar presente en el panel de applets.
- El editor de Tube debe estar abierto. Si no está abierto, haga doble clic en la etapa TUBE en el widget de cadena para abrirlo.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget de cadena para abrir el editor de Tube.
2. Localice el medidor vertical en el lado derecho del editor, a la derecha de la curva de saturación. La etiqueta del encabezado dice **OUT**.
3. Introduzca audio a través de la radio. La barra de nivel sube y baja a medida que la señal pasa por la etapa Tube.
4. Lea el color del relleno para juzgar el margen de un vistazo (consulte los significados de los colores a continuación).
5. Lea el valor numérico en la lectura debajo de la barra para obtener un valor dB con signo preciso. La lectura numérica se actualiza a 10 Hz para mantener los dígitos legibles mientras la barra se anima en cada fotograma.

## Qué hace cada control

| Elemento | Qué muestra | Rango | Notas |
|---|---|---|---|
| Etiqueta del encabezado | Identifica el medidor | Muestra **OUT** | Confirma que este medidor muestra el nivel de salida post-saturación. |
| Barra de nivel | Relleno máximo suavizado | −60 dB (inferior) a 0 dB (superior) | Utiliza balística de ataque rápido (alfa = 0,6) / liberación lenta (alfa = 0,08). El degradado de relleno usa el token del tema `color.meter.bar.fillGradient`; colores predeterminados: verde (bajo) → lima → ámbar → rojo (superior, por encima de −3 dB). Cuando el tema cambia, el medidor se renderiza automáticamente. |
| Marcas de escala dB | Cuadrícula de referencia estática | Marcadas en 0, −6, −12, −20, −40 dB | Las líneas de marca se extienden sobre la barra para que el nivel absoluto sea legible de un vistazo. |
| Lectura numérica | Máximo suavizado como valor dB con signo | `-inf` o un valor con signo con un decimal, ej. `+0.0 dB` | Muestra `-inf` cuando la señal está por debajo de aproximadamente −59,5 dB. Se actualiza a 10 Hz para facilitar la lectura. |

### Significados de los colores de la barra de nivel

| Color | Nivel aproximado | Significado |
|---|---|---|
| Verde | −60 dB a −12 dB | Amplio margen. |
| Lima | −12 dB a −6 dB | Nivel moderado; rango de funcionamiento normal para la mayoría de las señales. |
| Ámbar | −6 dB a −3 dB | Acercándose al recorte; considere reducir Drive o Output. |
| Rojo | Por encima de −3 dB | A 3 dB o menos del recorte. Reduzca Drive o Output para bajar el nivel. |

## Consejos

- La balística del medidor coincide con la del medidor de salida EQ, por lo que la sensación visual es coherente si usa ambos applets uno al lado del otro.
- Si la barra permanece roja durante los picos normales del habla, reduzca el control **Output** (rango −24 dB a +12 dB, predeterminado 0,0 dB) o reduzca el control **Drive** (rango 0 dB a 24 dB, predeterminado 0,0 dB) hasta que el ámbar o un nivel inferior sea típico para sus picos de señal.
- La balística de liberación lenta (alfa = 0,08) significa que la barra desciende gradualmente después de un pico, lo que facilita la detección visual de sobrecargas transitorias.
- La lectura numérica se actualiza a 10 Hz en lugar de en cada fotograma de pintado. Esto evita que los dígitos parpadeen o se vuelvan ilegibles durante cambios rápidos de nivel, mientras la barra continúa animándose suavemente.
- El degradado del medidor se aplica mediante el token `color.meter.bar.fillGradient` en el Theme Manager. Cualquier edición en vivo de este token en el Theme Editor hace que el medidor se vuelva a renderizar sin reiniciar AetherSDR.

## Relacionados

- [Resumen del medidor de nivel de salida](overview.md)
- [Theme Editor](theme-editor.md)

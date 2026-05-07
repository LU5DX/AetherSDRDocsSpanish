# Leer el medidor de nivel de salida en el applet Tube

El medidor de nivel de salida en el applet Tube muestra el nivel máximo suavizado posterior a la saturación de su señal de audio. Úselo para confirmar que la etapa Tube no está recortando su salida y para juzgar cuánto margen queda después de aplicar la ganancia de entrada y de salida.

## Antes de comenzar

- El applet Tube debe estar presente en el panel de applets.
- El editor del Tube debe estar abierto. Si no lo está, haga doble clic en la etapa TUBE en el widget de cadena para abrirlo.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget de cadena para abrir el editor del Tube.
2. Localice el medidor vertical en el lado derecho del editor, a la derecha de la curva de saturación. La etiqueta del encabezado dice **OUT**.
3. Alimente audio a través de la radio. La barra de nivel sube y baja a medida que la señal pasa por la etapa Tube.
4. Lea el color del relleno para juzgar el margen de un vistazo (vea los significados de los colores a continuación).
5. Lea el valor numérico en la lectura debajo de la barra para obtener un valor preciso en dB con signo.

## Qué hace cada elemento

| Elemento | Qué muestra | Rango | Notas |
|---|---|---|---|
| Etiqueta del encabezado | Identifica el medidor | Dice **OUT** | Confirma que este medidor muestra el nivel de salida posterior a la saturación. |
| Barra de nivel | Relleno de pico suavizado | −60 dB (inferior) a 0 dB (superior) | Usa balística de ataque rápido (alfa = 0.6) / liberación lenta (alfa = 0.08). |
| Marcas de escala en dB | Cuadrícula de referencia estática | 0, −6, −12, −20, −40 dB etiquetados | Las líneas de marca se extienden sobre la barra para que el nivel absoluto sea legible de un vistazo. |
| Lectura numérica | Pico suavizado como un valor dB con signo | `-inf` o un valor con signo con un decimal, p. ej. `+0.0 dB` | Muestra `-inf` cuando la señal está por debajo de aproximadamente −59.5 dB. |

### Significados de los colores de la barra de nivel

| Color | Nivel aproximado | Significado |
|---|---|---|
| Verde | −60 dB a −12 dB | Amplio margen. |
| Lima | −12 dB a −6 dB | Nivel moderado; rango operativo normal para la mayoría de las señales. |
| Ámbar | −6 dB a −3 dB | Acercándose al recorte; considere reducir Drive u Output. |
| Rojo | Por encima de −3 dB | A 3 dB o menos del recorte. Reduzca Drive u Output para bajar el nivel. |

## Consejos

- La balística del medidor coincide con la del medidor del fader de salida del ecualizador, por lo que la sensación visual es consistente si usa ambos applets lado a lado.
- Si la barra permanece roja durante los picos normales del habla, reduzca la perilla **Output** (rango −24 dB a +12 dB, predeterminado 0.0 dB) o reduzca la perilla **Drive** (rango 0 dB a 24 dB, predeterminado 0.0 dB) hasta que el color ámbar o inferior sea típico para sus picos de señal.
- La balística de liberación lenta (alfa = 0.08) significa que la barra desciende gradualmente después de un pico, lo que facilita la detección visual de sobrecargas transitorias.

## Relacionados

- [Descripción general del medidor de nivel de salida](overview.md)

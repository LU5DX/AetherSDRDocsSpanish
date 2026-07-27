# Procesador de Voz TX Aetherial / Resumen de Aetherial RX Poodoo™

## Propósito

El excitador PUDU es la pieza central de la cadena de audio Aetherial. Aplica procesamiento de tipo Aphex Aural Exciter + Big Bottom (modo Even) o de tipo Behringer con conformación tanh + compresión de graves (modo Odd) para dar forma y mejorar el audio. Existen dos instancias independientes: una para transmisión ("Aetherial TX Voice Processor") y otra para recepción ("Aetherial RX Poodoo™"), cada una con su estado completamente independiente.

## Apertura del Applet

- Abra el applet Aetherial TX Voice Processor o Aetherial RX Poodoo™ en el Panel de Applets.
- Alternativamente, haga doble clic en la etapa PUDU en el widget CHAIN para abrir un editor flotante titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".

## Resumen de Controles

El applet está dividido en dos secciones de procesamiento principales:

### Grupo Body (Procesador de Bajas Frecuencias)

Controla el modelado y la saturación de las bajas frecuencias. Tres perillas debajo de la etiqueta del recuadro "Body":

| Control        | Valor Predeterminado | Rango Válido | Clave de Configuración           | Comportamiento                                               |
|----------------|----------------------|--------------|----------------------------------|--------------------------------------------------------------|
| Poo / Drive    | 6.0 dB               | 0.0 a 24.0 dB| `ClientPuduTxPooDriveDb`         | Mapeo lineal. Exige más al saturación/comprobador de baja frecuencia. |
| Poo / Tune     | 100 Hz               | 50 a 160 Hz  | `ClientPuduTxPooTuneHz`          | Mapeo lineal. Centra la banda de enfoque de baja frecuencia. |
| Poo / Mix      | 30 %                 | 0.0 a 1.0    | `ClientPuduTxPooMix`             | Mapeo lineal. Mezcla la banda baja mejorada con la señal seca. |

### Grupo Clarity (Procesador de Altas Frecuencias)

Controla la excitación armónica y la presencia en altas frecuencias. Tres perillas debajo de la etiqueta del recuadro "Clarity":

| Control        | Valor Predeterminado | Rango Válido       | Clave de Configuración               | Comportamiento                                                      |
|----------------|----------------------|--------------------|--------------------------------------|---------------------------------------------------------------------|
| Doo / Tune     | 5000 Hz              | 1000 a 10000 Hz    | `ClientPuduTxDooTuneHz`              | Mapeo logarítmico (1000 * 10^n). Centra la banda de excitación de alta frecuencia. |
| Doo / Air      | 6.0 dB               | 0.0 a 24.0 dB      | `ClientPuduTxDooHarmonicsDb`         | Mapeo lineal. Cantidad de armónicos/'aire' añadidos en la banda alta. |
| Doo / Mix      | 30 %                 | 0.0 a 1.0          | `ClientPuduTxDooMix`                 | Mapeo lineal. Mezcla las altas frecuencias excitadas con la señal seca. |

### Selección de Modo

| Control | Clave de Configuración | Comportamiento                                                                                                                          |
|---------|------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| Even    | `ClientPuduTxMode`     | Selecciona el modelado asimétrico de linaje Aphex — armónicos predominantemente pares, más cálidos, con saturación LF Big Bottom. Color ámbar PooDoo cuando está marcado. Excluyente con Odd. |
| Odd     | `ClientPuduTxMode`     | Selecciona el modelado tanh simétrico de linaje Behringer — armónicos puramente impares, más brillantes, con un compresor de graves feed-forward. Excluyente con Even. |

### Indicador

El **logo AetherVoice** es un logotipo animado que pulsa con el RMS de la señal húmeda. Muestra la marca "AetherVoice™" y tiene una altura mínima de 40 píxeles.

## Soporte de Temas (v26.6.1)

A partir de la versión 26.6.1, el applet PUDU y su editor flotante admiten completamente los colores del tema:

- Los componentes de las perillas (anillo de fondo, arco de valor, manija del puntero, texto de etiqueta, texto de valor) leen los colores del sistema de temas a través de los espacios de nombre `color.knob.*` y `color.text.*`.
- La anulación del contenedor `applet/pudu` permite anulaciones de color por applet, como el color de primer plano ámbar PooDoo que se usa cuando el botón de radio del modo Even está activo.
- Las etiquetas de los recuadros tanto en el applet como en el editor usan `{{color.text.primary}}` del tema para una apariencia consistente.

## Edición de Valores en Línea

A partir de la versión 26.5.2, puede escribir un valor exacto directamente en cualquier perilla en lugar de arrastrar:

1. Haga clic en el texto del valor debajo de cualquier perilla para revelar un editor en línea.
2. Escriba un número y presione Enter o haga clic en otro lugar para confirmar.
3. El valor se ajusta automáticamente al rango válido.
4. Presione Escape para cancelar la edición y revertir al valor anterior.

## Persistencia Automática de Configuraciones

Todos los valores de control se guardan automáticamente por lado (TX/RX) y persisten entre sesiones. Las claves de configuración siguen el patrón `ClientPudu{Type}{Side}{Parameter}`, donde type es Tx o Rx.

## Añadir Aire con Doo Harmonics

Use la perilla **Doo / Air** para añadir excitación armónica y presencia a la banda de alta frecuencia. Esto eleva la percepción de "aire" en TX para que su señal se destaque, o en RX para mejorar la inteligibilidad del audio entrante.

### Pasos

1. Localice el recuadro del grupo **Clarity** — las tres perillas en el lado derecho del applet, debajo de la etiqueta del recuadro "Clarity".
2. Gire la perilla **Air** para ajustar la cantidad de contenido armónico añadido en la banda de alta frecuencia. El valor se muestra en dB debajo de la perilla.
3. Observe cómo el pulso del logo AetherVoice aumenta a medida que sube el nivel de la señal húmeda. Úselo como un indicador aproximado de cuánto procesamiento se está aplicando.
4. Si el resultado es demasiado agresivo, reduzca **Air** o baje **Doo / Mix** para mezclar el efecto con la señal seca.

Las configuraciones se guardan automáticamente. El valor persiste en `ClientPuduTxDooHarmonicsDb` (TX) o `ClientPuduRxDooHarmonicsDb` (RX).

### Consejos

- Comience con **Air** en 6.0 dB (valor predeterminado) y **Doo / Mix** al 30% (valor predeterminado), luego aumente **Air** gradualmente mientras escucha el efecto en el material de programa.
- La perilla **Doo / Tune** centra la banda donde se añaden armónicos. Ajústela para que coincida con el pico de presencia de su micrófono en TX, o con el rango de inteligibilidad del audio entrante en RX. Consulte [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad de RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md) para ese procedimiento.
- El modo Even (linaje Aphex) produce armónicos pares más cálidos; el modo Odd (linaje Behringer) produce armónicos impares más brillantes. El carácter de **Air** difiere entre ambos. Consulte [Elegir modo Even vs Odd](pick-aphex-even-vs-behringer-odd-character.md).
- Use la edición en línea para establecer rápidamente valores precisos: haga clic en el valor mostrado, escriba el número con unidades si lo desea y presione Enter.

### Solución de Problemas

- **La perilla Air no tiene efecto audible** — La etapa PUDU puede estar desviada. Cuando la etapa está desviada, todo el mosaico del applet se atenúa con opacidad reducida. Verifique que la etapa esté habilitada en el widget CHAIN. Consulte [Desviar PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md).
- **El efecto suena áspero con valores moderados de Air** — Baje **Doo / Mix** para reducir la mezcla húmeda en lugar de eliminar **Air** por completo. Consulte [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md).

## Relacionados

- [Resumen de Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
- [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad de RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir modo Even vs Odd](pick-aphex-even-vs-behringer-odd-character.md)
- [Desviar PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md)

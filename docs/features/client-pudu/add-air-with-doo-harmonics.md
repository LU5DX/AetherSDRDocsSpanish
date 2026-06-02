# Procesador de Voz de Transmisión Aetherial / Aetherial RX Poodoo™ — Descripción General

## Propósito

El excitador PUDU es la pieza central de la cadena de audio Aetherial. Aplica procesamiento de tipo Aphex Aural Exciter + Big Bottom (modo Even) o conformación tanh tipo Behringer + compresión de graves (modo Odd) para dar forma y mejorar el audio. Existen dos instancias independientes: una para transmisión ("Aetherial TX Voice Processor") y otra para recepción ("Aetherial RX Poodoo™"), cada una con estado completamente independiente.

## Abrir el Applet

- Abra el applet Aetherial TX Voice Processor o Aetherial RX Poodoo™ en el Panel de Applets.
- Alternativamente, haga doble clic en la etapa PUDU en el widget CHAIN para abrir un editor flotante titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".

## Descripción General de Controles

El applet está dividido en dos secciones principales de procesamiento:

### Grupo Body (Procesador de Bajas Frecuencias)

Controla la conformación y saturación de las frecuencias bajas. Tres perillas debajo de la etiqueta del grupo "Body":

| Control        | Valor Predeterminado | Rango Válido  | Clave de Ajuste                | Comportamiento                                               |
|----------------|----------------------|---------------|--------------------------------|--------------------------------------------------------------|
| Poo / Drive    | 6.0 dB               | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb`       | Mapeo lineal. Exige más al saturador/compresor de baja frecuencia. |
| Poo / Tune     | 100 Hz               | 50 a 160 Hz   | `ClientPuduTxPooTuneHz`        | Mapeo lineal. Centra la banda de enfoque de baja frecuencia.     |
| Poo / Mix      | 30 %                 | 0.0 a 1.0     | `ClientPuduTxPooMix`           | Mapeo lineal. Mezcla la banda baja procesada con la señal seca.  |

### Grupo Clarity (Procesador de Altas Frecuencias)

Controla la excitación armónica y presencia en altas frecuencias. Tres perillas debajo de la etiqueta del grupo "Clarity":

| Control        | Valor Predeterminado | Rango Válido      | Clave de Ajuste                    | Comportamiento                                                    |
|----------------|----------------------|-------------------|------------------------------------|-------------------------------------------------------------------|
| Doo / Tune     | 5000 Hz              | 1000 a 10000 Hz   | `ClientPuduTxDooTuneHz`            | Mapeo logarítmico (1000 * 10^n). Centra la banda de excitación de alta frecuencia. |
| Doo / Air      | 6.0 dB               | 0.0 a 24.0 dB     | `ClientPuduTxDooHarmonicsDb`       | Mapeo lineal. Cantidad de armónicos/'aire' añadidos en la banda alta. |
| Doo / Mix      | 30 %                 | 0.0 a 1.0         | `ClientPuduTxDooMix`               | Mapeo lineal. Mezcla las altas frecuencias excitadas con la señal seca. |

### Selección de Modo

| Control | Clave de Ajuste       | Comportamiento                                                                  |
|---------|-----------------------|---------------------------------------------------------------------------------|
| Even    | `ClientPuduTxMode`    | Selecciona la conformación asimétrica de linaje Aphex —armónicos predominantemente pares, más cálidos, con saturación LF Big Bottom. Color ámbar PooDoo cuando está seleccionado. Excluyente con Odd. |
| Odd     | `ClientPuduTxMode`    | Selecciona la conformación tanh simétrica de linaje Behringer —armónicos impares puros, más brillantes, con un compresor de graves feed-forward. Excluyente con Even. |

### Indicador

El **logotipo AetherVoice** es un logotipo animado que pulsa con el RMS de la señal procesada. Muestra la marca "AetherVoice™" y tiene una altura mínima de 40 píxeles.

## Soporte de Temas (v26.6.1)

A partir de la versión 26.6.1, el applet PUDU y su editor flotante son compatibles completamente con los colores del tema:

- Los componentes de las perillas (anillo de fondo, arco de valor, manecilla indicadora, texto de etiqueta, texto de valor) leen los colores del sistema de temas mediante los espacios de nombre `color.knob.*` y `color.text.*`.
- La anulación de contenedor `applet/pudu` permite anulaciones de color por applet, como el color de primer plano ámbar PooDoo que se usa cuando el botón de radio del modo Even está activo.
- Las etiquetas de los grupos tanto en el applet como en el editor usan `{{color.text.primary}}` del tema para una apariencia consistente.

## Edición de Valor en Línea

A partir de la versión 26.5.2, puede escribir un valor exacto directamente en cualquier perilla en lugar de arrastrarla:

1. Haga clic en el texto del valor debajo de cualquier perilla para abrir un editor en línea.
2. Escriba un número y presione Enter o haga clic en otro lugar para confirmar.
3. El valor se ajusta automáticamente al rango válido.
4. Presione Escape para cancelar la edición y volver al valor anterior.

## Persistencia Automática de Ajustes

Todos los valores de control se guardan automáticamente por lado (TX/RX) y persisten entre sesiones. Las claves de ajuste siguen el patrón `ClientPudu{Type}{Side}{Parameter}`, donde Type es Tx o Rx.

## Añadir Aire con Doo Harmonics

Use la perilla **Doo / Air** para añadir excitación armónica y presencia a la banda de alta frecuencia. Esto aumenta el "aire" percibido en TX para que su señal se destaque, o en RX para mejorar la inteligibilidad del audio entrante.

### Pasos

1. Localice el grupo **Clarity** — las tres perillas en el lado derecho del applet, debajo de la etiqueta "Clarity".
2. Gire la perilla **Air** para ajustar la cantidad de contenido armónico añadido en la banda de alta frecuencia. El valor se muestra en dB debajo de la perilla.
3. Observe cómo el pulso del logotipo AetherVoice aumenta a medida que sube el nivel de la señal procesada. Úselo como un indicador aproximado de cuánto procesamiento se está aplicando.
4. Si el resultado es demasiado agresivo, reduzca **Air** o baje **Doo / Mix** para mezclar el efecto con la señal seca.

Los ajustes se guardan automáticamente. El valor persiste en `ClientPuduTxDooHarmonicsDb` (TX) o `ClientPuduRxDooHarmonicsDb` (RX).

### Consejos

- Comience con **Air** en 6.0 dB (predeterminado) y **Doo / Mix** en 30 % (predeterminado), luego aumente **Air** gradualmente mientras escucha el efecto en el material de programa.
- La perilla **Doo / Tune** centra la banda donde se añaden los armónicos. Ajústela para que coincida con el pico de presencia de su micrófono en TX, o con el rango de inteligibilidad del audio entrante en RX. Consulte [Centrar Doo en la banda de presencia para su micrófono (TX) o para la inteligibilidad de RX](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md) para ese procedimiento.
- El modo Even (linaje Aphex) produce armónicos pares más cálidos; el modo Odd (linaje Behringer) produce armónicos impares más brillantes. El carácter de **Air** difiere entre ambos. Consulte [Elegir modo Even vs Odd](pick-aphex-even-vs-behringer-odd-character.md).
- Use la edición en línea para establecer valores precisos rápidamente: haga clic en el valor mostrado, escriba el número con unidades si lo desea y presione Enter.

### Solución de Problemas

- **La perilla Air no tiene efecto audible** — La etapa PUDU puede estar omitida. Cuando la etapa está omitida, todo el mosaico del applet se atenúa con opacidad reducida. Verifique que la etapa esté habilitada en el widget CHAIN. Consulte [Omitir PUDU desde cualquier cadena](bypass-pudu-from-either-chain.md).
- **El efecto suena áspero con valores moderados de Air** — Baje **Doo / Mix** para reducir la mezcla de señal procesada en lugar de cortar **Air** por completo. Consulte [Mezclar la excitación Doo con Mix](blend-the-doo-excitement-with-mix.md).

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Centre Doo on the presence band for your mic (TX) or for RX intelligibility](centre-doo-on-the-presence-band-for-your-mic-tx-or-for-rx-intelligibility.md)
- [Blend the Doo excitement with Mix](blend-the-doo-excitement-with-mix.md)
- [Pick Even vs Odd mode](pick-aphex-even-vs-behringer-odd-character.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)

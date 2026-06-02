# Sintonice el Cuerpo a la fundamental de su voz (TX) o para resaltar los bajos del programa (RX)

El mando **Cuerpo / Sintonía** establece la frecuencia central de la banda de saturación de baja frecuencia. En TX, diríjalo hacia la fundamental de su voz para agregar cuerpo y calidez en el tono correcto. En RX, muévalo hacia el contenido dominante de baja frecuencia del audio entrante para resaltar los bajos del programa.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena de Audio Aetherial. Si el applet Poodoo no está visible, habilite la etapa PUDU mediante el widget CHAIN en el lado TX o RX.
- Decida si está ajustando la cadena TX ("Procesador de Voz Aetherial TX") o la cadena RX ("Poodoo™ RX Aetherial") — tienen configuraciones completamente independientes.

## Pasos

1. Abra el editor PUDU para el lado que desea ajustar: haga doble clic en la etapa PUDU en el widget CHAIN. Se abrirá el editor sin marco titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".
2. Localice el grupo **Cuerpo** — los tres mandos bajo la etiqueta "Body" en la mitad izquierda de la fila de mandos.
3. Gire el mando **Drive** (el primer mando del grupo Cuerpo) para establecer el nivel de excitación del procesador de baja frecuencia.
4. Gire el mando **Sintonía** (el mando central del grupo Cuerpo) hasta la frecuencia objetivo.
   - Para TX: comience cerca de la fundamental de su voz. Una fundamental de voz masculina típica es 85–180 Hz; una fundamental de voz femenina típica es 165–255 Hz. El valor predeterminado es 100 Hz.
   - Para RX: barra hacia el contenido de baja frecuencia dominante del programa que desea enfatizar.
5. Gire el mando **Mezcla** (el tercer mando del grupo Cuerpo) para combinar el resultado a su gusto. Los ajustes se guardan automáticamente.
6. Monitorice el logotipo de AetherVoice: su brillo late con el RMS de la señal procesada, proporcionando retroalimentación en tiempo real mientras ajusta la frecuencia.
7. Puede escribir un valor directamente en la pantalla de valor de cualquier mando: haga clic en el valor mostrado, escriba un número y presione Enter o haga clic fuera para confirmar. El editor acepta formatos decimales según la configuración regional (por ejemplo, "12,5" en configuraciones regionales de coma decimal) y elimina el texto de unidad final.

## Qué hace cada control

| Control (grupo Cuerpo) | Predeterminado | Rango válido   | Notas                                              |
|------------------------|----------------|----------------|----------------------------------------------------|
| **Drive**              | 6.0 dB         | 0.0 a 24.0 dB  | Excita el saturizador/compresor de baja frecuencia |
| **Sintonía**           | 100 Hz         | 50 a 160 Hz    | Mapeo lineal; centra la banda de enfoque de baja frecuencia |
| **Mezcla**             | 30 %           | 0.0 a 1.0      | Combina la banda baja mejorada con la señal seca   |

| Control (grupo Claridad) | Predeterminado | Rango válido     | Notas                                              |
|--------------------------|----------------|------------------|----------------------------------------------------|
| **Sintonía**             | 5000 Hz        | 1000 a 10000 Hz  | Mapeo logarítmico; centra la banda de excitación de alta frecuencia |
| **Aire**                 | 6.0 dB         | 0.0 a 24.0 dB    | Cantidad de armónicos/aire añadidos en la banda alta |
| **Mezcla**               | 30 %           | 0.0 a 1.0        | Combina las altas frecuencias excitadas con la señal seca |

| Control             | Predeterminado | Rango válido | Comportamiento                                               |
|---------------------|----------------|--------------|--------------------------------------------------------------|
| **Even**            | —              | —            | Botón de radio; selecciona la conformación asimétrica de la línea Aphex |
| **Odd**             | —              | —            | Botón de radio; selecciona la conformación simétrica de la línea Behringer |
| Logotipo AetherVoice | —              | —            | Logotipo animado que late con el RMS de la señal procesada    |

El mando **Cuerpo / Sintonía** utiliza un mapeo lineal en su rango de 50–160 Hz. La pantalla muestra el valor en hercios enteros (por ejemplo, "100 Hz").

El mando **Claridad / Sintonía** utiliza un mapeo logarítmico (1000 * 10^n). La pantalla muestra el valor en kilohercios por encima de 1 kHz (por ejemplo, "5.0 kHz") o en hercios por debajo.

## Consejos

- La banda de Cuerpo es intencionadamente estrecha. Si oye poco efecto después de sintonizar, aumente primero **Drive**, luego vuelva a barrer **Sintonía** hasta que oiga que la saturación se activa.
- En el modo **Even**, la etapa de Cuerpo utiliza saturación Big Bottom de baja frecuencia; en el modo **Odd**, utiliza un compresor de graves feed-forward. La frecuencia de sintonía óptima puede diferir ligeramente entre modos — vuelva a comprobarlo después de cambiar.
- Mantenga **Mezcla** por debajo del 50 % en TX para evitar que la señal transmitida se vuelva turbia. Comience con el valor predeterminado del 30 % y auméntelo solo si la mejora es inaudible.
- El control **Aire** de Claridad añade presencia y brillo. Auméntelo con precaución en TX para evitar aspereza.
- Utilice el editor en línea en cualquier mando para escribir valores exactos. Haga clic en el valor mostrado, introduzca el número y presione Enter.
- Cuando la etapa PUDU está puenteada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esto es solo un indicador visual — no se pierde ningún ajuste.
- En v26.6.1, los colores de los mandos ahora se obtienen del tema. El applet PUDU utiliza un contenedor temático dedicado (`applet/pudu`) que puede anular los colores del anillo, arco y puntero del mando de forma independiente. Si ha creado un tema personalizado, asegúrese de que las claves `color.knob.*` y `color.text.*` estén definidas para el contenedor PUDU; de lo contrario, se aplicarán los colores del tema predeterminado.

## Solución de problemas

- **Girar Sintonía no tiene efecto audible** — confirme que la etapa PUDU está habilitada (el widget CHAIN controla el bypass). También verifique que **Drive** esté por encima de 0.0 dB y **Mezcla** esté por encima del 0 %; ambos en su mínimo silenciarán la banda de Cuerpo independientemente del ajuste de Sintonía.
- **Los mandos del grupo Cuerpo no son visibles** — el applet PUDU está oculto hasta que la etapa PUDU se habilita a través del widget CHAIN o del editor flotante.
- **Los valores escritos no son aceptados** — asegúrese de que está utilizando un separador decimal apropiado para su configuración regional. El editor acepta números y elimina el texto de unidad final (por ejemplo, "100 Hz" se convierte en 100).
- **Los colores de los mandos parecen incorrectos** — la nueva representación temática en v26.6.1 lee los colores de `color.knob.background`, `color.knob.foreground` y `color.knob.handle` en el tema. Si faltan estas claves o están mal configuradas, los gráficos de los mandos pueden recurrir a valores inesperados. Contacte con el desarrollador de su tema o restablezca el tema predeterminado.

## Relacionados

- [Descripción general del Procesador de Voz Aetherial TX / Poodoo RX Aetherial](overview.md)
- Dial Drive para el grosor de baja frecuencia
- Combine la mejora de Cuerpo con Mezcla
- [Elija el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- Añada presencia con Aire de Claridad

# Sintonice el Cuerpo a la fundamental de su voz (TX) o realce los graves del programa en RX

El mando **Body / Tune** establece la frecuencia central de la banda de saturación de baja frecuencia. En TX, apúntelo a la fundamental de su voz para añadir cuerpo y calidez en el tono adecuado. En RX, desplacelo hacia el contenido dominante de baja frecuencia del audio entrante para resaltar los graves del programa.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena Aetherial Audio. Si el applet Poodoo no está visible, habilite la etapa PUDU mediante el widget CHAIN en el lado TX o RX.
- Decida si está ajustando la cadena de TX ("Aetherial TX Voice Processor") o la cadena de RX ("Aetherial RX Poodoo™") — tienen ajustes totalmente independientes.

## Pasos

1. Abra el editor PUDU para el lado que desea ajustar: haga doble clic en la etapa PUDU en el widget CHAIN. Se abrirá el editor sin marco titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".
2. Localice el grupo **Body** — los tres mandos bajo la etiqueta "Body" en la mitad izquierda de la fila de mandos.
3. Gire el mando **Drive** (el primer mando del grupo Body) para establecer el nivel de excitación del procesador de baja frecuencia.
4. Gire el mando **Tune** (el mando central del grupo Body) a la frecuencia deseada.
   - Para TX: comience cerca de la fundamental de su voz. Una fundamental de voz masculina típica es 85–180 Hz; una fundamental de voz femenina típica es 165–255 Hz. El valor predeterminado es 100 Hz.
   - Para RX: barra hacia el contenido de baja frecuencia dominante del programa que desea enfatizar.
5. Gire el mando **Mix** (el tercer mando del grupo Body) para mezclar el resultado al gusto. Los ajustes se guardan automáticamente.
6. Supervise el logotipo AetherVoice: su brillo pulsa con el RMS de la señal procesada, proporcionando retroalimentación en tiempo real mientras ajusta la frecuencia.
7. Puede escribir un valor directamente en la pantalla de valor de cualquier mando: haga clic en el valor mostrado, escriba un número y presione Enter o haga clic fuera para confirmar. El editor acepta formatos decimales según la configuración regional (por ejemplo, "12,5" en locales con coma decimal) y elimina el texto de unidad final.

## Qué hace cada control

| Control (grupo Body) | Predeterminado | Rango válido    | Notas                                          |
|----------------------|----------------|-----------------|------------------------------------------------|
| **Drive**            | 6.0 dB         | 0.0 a 24.0 dB   | Excitación del saturación/compresor de baja frecuencia |
| **Tune**             | 100 Hz         | 50 a 160 Hz     | Mapeo lineal; centra la banda de enfoque de BF  |
| **Mix**              | 30 %           | 0.0 a 1.0       | Mezcla la banda baja realzada con la señal seca |

| Control (grupo Clarity) | Predeterminado | Rango válido      | Notas                                           |
|-------------------------|----------------|-------------------|-------------------------------------------------|
| **Tune**                | 5000 Hz        | 1000 a 10000 Hz   | Mapeo logarítmico; centra la banda de excitación de AF |
| **Air**                 | 6.0 dB         | 0.0 a 24.0 dB     | Cantidad de armónicos/aire añadido en la banda alta |
| **Mix**                 | 30 %           | 0.0 a 1.0         | Mezcla las altas frecuencias excitadas con la señal seca |

| Control             | Predeterminado | Rango válido | Comportamiento                                                |
|---------------------|----------------|--------------|---------------------------------------------------------------|
| **Even**            | —              | —            | Botón de opción; selecciona el modelado asimétrico de la línea Aphex |
| **Odd**             | —              | —            | Botón de opción; selecciona el modelado simétrico de la línea Behringer |
| Logotipo AetherVoice| —              | —            | Logotipo animado que pulsa con el RMS de la señal procesada   |

El mando **Body / Tune** utiliza mapeo lineal en su rango de 50–160 Hz. La pantalla muestra el valor en hercios enteros (por ejemplo, "100 Hz").

El mando **Clarity / Tune** utiliza mapeo logarítmico (1000 * 10^n). La pantalla muestra el valor en kilohercios por encima de 1 kHz (por ejemplo, "5.0 kHz") o en hercios por debajo.

## Consejos

- La banda Body es intencionadamente estrecha. Si escucha poco efecto después de sintonizar, aumente primero **Drive**, luego vuelva a barrer **Tune** hasta que escuche la saturación activarse.
- En modo **Even**, la etapa Body utiliza saturación de baja frecuencia Big Bottom; en modo **Odd**, utiliza un compresor de graves feed-forward. La frecuencia de sintonía óptima puede diferir ligeramente entre modos — vuelva a comprobarla después de cambiar.
- Mantenga **Mix** por debajo del 50 % en TX para evitar que la señal transmitida se vuelva turbia. Comience con el valor predeterminado del 30 % y aumente solo si el realce es inaudible.
- El control **Air** de Clarity añade presencia y brillo. Auméntelo con precaución en TX para evitar aspereza.
- Utilice el editor en línea de cualquier mando para escribir valores exactos. Haga clic en el valor mostrado, ingrese el número y presione Enter.
- Cuando la etapa PUDU está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esto es solo un indicador visual — no se pierde ningún ajuste.

## Solución de problemas

- **Girar Tune no tiene efecto audible** — confirme que la etapa PUDU está habilitada (el widget CHAIN controla el bypass). También verifique que **Drive** esté por encima de 0.0 dB y **Mix** esté por encima del 0 %; ambos en sus valores mínimos silenciarán la banda Body independientemente del ajuste de Tune.
- **Los mandos del grupo Body no son visibles** — el applet PUDU está oculto hasta que la etapa PUDU se habilite mediante el widget CHAIN o el editor flotante.
- **Los valores escritos no se aceptan** — asegúrese de usar un separador decimal apropiado para su configuración regional. El editor acepta números y elimina el texto de unidad final (por ejemplo, "100 Hz" se convierte en 100).

## Relacionado

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Dial Drive for LF thickness](dial-drive-for-lf-thickness.md)
- [Blend the Body enhancement with Mix](blend-the-body-enhancement-with-mix.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Add presence with Clarity Air](add-presence-with-clarity-air.md)

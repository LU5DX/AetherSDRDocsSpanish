# Ajuste del Body a la frecuencia fundamental de su voz (TX) o para realzar las frecuencias bajas del programa (RX)

La perilla **Body / Tune** establece la frecuencia central de la banda de saturación de baja frecuencia. En TX, diríjala a la frecuencia fundamental de su voz para agregar cuerpo y calidez en el tono adecuado. En RX, muévala hacia el contenido dominante de baja frecuencia del audio entrante para realzar las frecuencias bajas del programa.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena Aetherial Audio. Si el applet Poodoo no es visible, habilite la etapa PUDU a través del widget CHAIN en el lado TX o RX.
- Decida si está ajustando la cadena TX ("Aetherial TX Voice Processor") o la cadena RX ("Aetherial RX Poodoo™") — tienen configuraciones completamente independientes.

## Pasos

1. Abra el editor PUDU para el lado que desea ajustar: haga doble clic en la etapa PUDU en el widget CHAIN. Se abrirá el editor sin marco titulado "Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX".
2. Localice el grupo **Body** — las tres perillas debajo de la etiqueta "Body" en la mitad izquierda de la fila de perillas.
3. Gire la perilla **Drive** (la primera perilla en el grupo Body) para establecer el nivel de excitación del procesador de baja frecuencia.
4. Gire la perilla **Tune** (la perilla central en el grupo Body) a la frecuencia objetivo.
   - Para TX: comience cerca de la frecuencia fundamental de su voz. Una frecuencia fundamental masculina típica es de 85–180 Hz; una frecuencia fundamental femenina típica es de 165–255 Hz. El valor predeterminado es 100 Hz.
   - Para RX: barra hacia el contenido de baja frecuencia del programa que desea enfatizar.
5. Gire la perilla **Mix** (la tercera perilla en el grupo Body) para mezclar el resultado al gusto. Los ajustes se guardan automáticamente.
6. Supervise el logo AetherVoice: su brillo pulsa con la RMS de la señal procesada, proporcionando retroalimentación en tiempo real mientras ajusta la frecuencia.
7. Puede escribir un valor directamente en la pantalla de cualquier perilla: haga clic en el valor mostrado, escriba un número y presione Enter o haga clic fuera para confirmar. El editor acepta formatos decimales según la configuración regional (por ejemplo, "12,5" en regiones con coma decimal) y elimina el texto de unidad final.

## Qué hace cada control

| Control (grupo Body) | Valor predeterminado | Rango válido    | Notas                                               |
|----------------------|----------------------|-----------------|-----------------------------------------------------|
| **Drive**            | 6.0 dB               | 0.0 a 24.0 dB   | Excita el saturator/compresor de baja frecuencia    |
| **Tune**             | 100 Hz               | 50 a 160 Hz     | Mapeo lineal; centra la banda de enfoque de baja frecuencia |
| **Mix**              | 30 %                 | 0.0 a 1.0       | Mezcla la banda baja realzada con la señal seca     |

| Control (grupo Clarity) | Valor predeterminado | Rango válido     | Notas                                                 |
|-------------------------|----------------------|------------------|-------------------------------------------------------|
| **Tune**                | 5000 Hz              | 1000 a 10000 Hz  | Mapeo logarítmico; centra la banda de excitación de alta frecuencia |
| **Air**                 | 6.0 dB               | 0.0 a 24.0 dB    | Cantidad de armónicos/aire agregada en la banda alta  |
| **Mix**                 | 30 %                 | 0.0 a 1.0        | Mezcla las altas frecuencias excitadas con la señal seca |

| Control             | Valor predeterminado | Rango válido | Comportamiento                                              |
|---------------------|----------------------|--------------|-------------------------------------------------------------|
| **Even**            | —                    | —            | Botón de radio; selecciona el modelado asimétrico de la línea Aphex |
| **Odd**             | —                    | —            | Botón de radio; selecciona el modelado simétrico de la línea Behringer |
| Logo AetherVoice    | —                    | —            | Logotipo animado que pulsa con la RMS de la señal procesada |

La perilla **Body / Tune** utiliza mapeo lineal en su rango de 50–160 Hz. La pantalla muestra en hercios enteros (por ejemplo, "100 Hz").

La perilla **Clarity / Tune** utiliza mapeo logarítmico (1000 * 10^n). La pantalla muestra en kilohercios por encima de 1 kHz (por ejemplo, "5.0 kHz") o en hercios por debajo.

## Consejos

- La banda Body es intencionalmente estrecha. Si escucha poco efecto después del ajuste, primero suba **Drive**, luego vuelva a barrer **Tune** hasta que escuche que la saturación se activa.
- En el modo **Even**, la etapa Body utiliza saturación Big Bottom de baja frecuencia; en el modo **Odd**, utiliza un compresor de graves feed-forward. La frecuencia de ajuste óptima puede diferir ligeramente entre modos — vuelva a verificarla después de cambiar.
- Mantenga **Mix** por debajo del 50 % en TX para evitar que la señal transmitida se vuelva pastosa. Comience con el valor predeterminado del 30 % y auméntelo solo si la mejora es inaudible.
- El control **Air** de Clarity agrega presencia y brillo. Auméntelo con precaución en TX para evitar aspereza.
- Use el editor en línea en cualquier perilla para escribir valores exactos. Haga clic en el valor mostrado, ingrese el número y presione Enter.
- Cuando la etapa PUDU está desviada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esto es solo un indicador visual — no se pierde ninguna configuración.
- En v26.6.1, los colores de las perillas ahora provienen del tema. El applet PUDU utiliza un contenedor temático dedicado (`applet/pudu`) que puede anular los colores del anillo, arco y puntero de las perillas de forma independiente. Si ha creado un tema personalizado, asegúrese de que las claves `color.knob.*` y `color.text.*` estén definidas para el contenedor PUDU; de lo contrario, se aplican los colores del tema predeterminado.
- En v26.7.4, el editor PUDU ya no utiliza un estilo dedicado para sus botones. Todos los botones del editor ahora siguen el estilo global del tema de manera consistente.

## Solución de problemas

- **Girar Tune no tiene efecto audible** — confirme que la etapa PUDU esté habilitada (el widget CHAIN controla la desviación). También verifique que **Drive** esté por encima de 0.0 dB y **Mix** esté por encima del 0 %; ambos en sus mínimos silenciarán la banda Body independientemente de la configuración de Tune.
- **Las perillas del grupo Body no son visibles** — el applet PUDU está oculto hasta que la etapa PUDU se habilite a través del widget CHAIN o del editor flotante.
- **Los valores escritos no se aceptan** — asegúrese de utilizar un separador decimal apropiado para su configuración regional. El editor acepta números y elimina el texto de unidad final (por ejemplo, "100 Hz" se convierte en 100).
- **Los colores de las perillas parecen incorrectos** — la nueva representación temática en v26.6.1 lee los colores de `color.knob.background`, `color.knob.foreground` y `color.knob.handle` en el tema. Si estas claves faltan o están mal configuradas, la apariencia de las perillas puede retroceder inesperadamente. Contacte al desarrollador de su tema o restablezca el tema predeterminado.

## Relacionado

- [Descripción general de Aetherial TX Voice Processor / Aetherial RX Poodoo](overview.md)
- Dial Drive para espesor de baja frecuencia
- Mezcle la mejora de Body con Mix
- [Seleccione el carácter Aphex (Even) vs Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- Agregue presencia con Clarity Air

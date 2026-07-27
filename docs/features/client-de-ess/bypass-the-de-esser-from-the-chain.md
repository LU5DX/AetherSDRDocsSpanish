# De-Eser Aetherial

El De-Eser Aetherial controla la sibilancia áspera de las letras 'S' y 'T' atenuando una banda estrecha cuando supera un umbral de cadena lateral. Utiliza procesamiento de bandas divididas: solo se atenúa la salida del filtro paso banda de sibilancia, dejando intactos los graves y medios. Esto corrige el error de atenuación de banda ancha que anteriormente causaba una pérdida de aproximadamente 30 W de potencia de transmisión. El panel muestra la respuesta del filtro paso banda de la cadena lateral, un medidor de reducción de ganancia de 24 dB, seis perillas de ajuste (Freq, Q, Thresh, Amount, Attack, Release) y una pendiente de cascada seleccionable por el usuario (12/24/36/48 dB/oct).

**Instancias del applet:**
- **Instancia TX**: "Aetherial De-Esser" (se muestra en el Panel de Applet acoplado)
- **Instancia RX**: "Aetherial De-Esser — RX" (accesible a través de la Tira de Canal de Audio Aetherial)

## Antes de comenzar

- AetherSDR debe estar abierto y la cadena de procesamiento de Audio Aetherial (TXDSP o RXDSP) debe estar visible.
- La etapa DESS ya debe existir en el widget CHAIN. Si el de-eser nunca se ha habilitado, es posible que la etapa DESS no esté presente.
- El de-eser está disponible tanto en las rutas de audio de TX como de RX. Cada ruta tiene su propia instancia independiente del De-Eser Aetherial.

## Bypass del de-eser desde la cadena

Elimine el De-Eser Aetherial de su ruta de audio de TX o RX sin cambiar ninguna de sus configuraciones. El bypass es útil cuando desea comparar el audio procesado y el no procesado, o deshabilitar temporalmente el de-essing para una sesión en particular.

### Pasos para el bypass del de-eser de TX

1. Localice el widget CHAIN en el contenedor de Audio Aetherial (TXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para alternar el bypass activado o desactivado.

### Pasos para el bypass del de-eser de RX

1. Localice el widget CHAIN en el contenedor de Audio Aetherial (RXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para alternar el bypass activado o desactivado.

Cuando está en bypass, el mosaico completo del de-eser se renderiza con opacidad reducida (55% de lo normal). Al hacer clic una vez de nuevo, se reactiva y restaura la opacidad completa del mosaico. Los ajustes `ClientDeEssTxEnabled` y `ClientDeEssRxEnabled` se actualizan inmediatamente.

## Abrir el panel de ajustes del de-eser

El panel de ajustes del de-eser tiene dos instancias:
- **Instancia TX**: "Aetherial De-Esser — TX" (accesible desde la ruta TX de la Tira de Canal de Audio Aetherial)
- **Instancia RX**: "Aetherial De-Esser — RX" (accesible desde la ruta RX de la Tira de Canal de Audio Aetherial)

Para abrir la instancia adecuada:
1. Abra la Tira de Canal de Audio Aetherial.
2. Haga clic en la etapa **DESS** para abrir el panel de ajustes del de-eser para esa ruta (TX o RX).
3. La barra de título del panel muestra "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX" según la ruta que haya accedido.

## Controles del de-eser

El panel del De-Eser Aetherial contiene los siguientes controles:

| Etiqueta                   | Tipo        | Valor predeterminado |
|----------------------------|-------------|----------------------|
| Curva de respuesta de cadena lateral | indicador   | —                    |
| Barra de reducción de ganancia       | medidor     | —                    |
| Freq                       | perilla     | 6000 Hz              |
| Q                          | perilla     | 2.00                 |
| Thresh                     | perilla     | -30.0 dB             |
| Amount                     | perilla     | -6.0 dB              |
| Attack                     | perilla     | 1.0 ms               |
| Release                    | perilla     | 100 ms               |
| Slope                      | botón       | 24 dB/oct (2 etapas) |

### Detalles de los controles

- **Freq** (mapeo logarítmico, 1000 a 12000 Hz): Establece la frecuencia central de la banda de sibilancia. Las etiquetas muestran "N kHz" por encima de 1 kHz, "N Hz" por debajo.
- **Q** (mapeo lineal, 0.5 a 5.0): Establece el ancho de banda de la banda de sibilancia — un Q más alto significa un ancho de banda más estrecho. Las etiquetas muestran "X.XX".
- **Thresh** (mapeo lineal, -60.0 a 0.0 dB): Nivel por encima del cual el de-eser comienza a atenuar la banda.
- **Amount** (mapeo lineal, -24.0 a 0.0 dB): Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción.
- **Attack** (mapeo exponencial, 0.1 a 30.0 ms): Establece la rapidez con la que responde el de-eser una vez que la sibilancia supera el umbral. Presente en el StripDeEssPanel de la Tira de Canal (RX y TX). El ClientDeEssApplet acoplado omite esta perilla.
- **Release** (mapeo exponencial, 10.0 a 500.0 ms): Establece la rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Presente en el StripDeEssPanel de la Tira de Canal (RX y TX). El ClientDeEssApplet acoplado omite esta perilla.
- **Slope** (cicla entre 12/24/36/48 dB/oct): Establece el conteo de cascada del filtro paso banda de la cadena lateral. Cada etapa añade 12 dB/oct de atenuación fuera de la banda de sibilancia. Una pendiente más alta equivale a una muesca efectiva más estrecha y menos daño colateral en las bandas medias en frases con muchas 'S'. Presente en el StripDeEssPanel flotante (columna izquierda, parte inferior). La etiqueta muestra "N dB/oct". Presente para ambas rutas TX y RX. Se persiste como `ClientDeEssTxSlopeStages` / `ClientDeEssRxSlopeStages`.

## Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Bola de frecuencia central | en reposo sobre el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Barra de reducción de ganancia | vacía, relleno rojo suave | Atenuación actual aplicada a la banda de sibilancia. El medidor es una barra horizontal roja suave, rellena desde la derecha. La escala máxima es 24 dB; una marca indica la cantidad típica de -6 dB. Se actualiza a aproximadamente 30 Hz. |

## Edición de valor en línea en las perillas

Las perillas del de-eser (Freq, Q, Thresh, Amount, Attack, Release) admiten la edición de valor en línea. En lugar de arrastrar la perilla, puede escribir un valor directamente.

### Para editar un valor de perilla usando la edición en línea

1. Haga clic en el texto del valor debajo de cualquier perilla del de-eser. Aparece un pequeño campo de texto, delineado en cian cuando está enfocado.
2. Escriba el nuevo valor. Puede incluir unidades (por ejemplo, "6 kHz", "-24.0 dB", "100 ms") o solo el número (por ejemplo, "6000", "2.0", "0.1").
3. Presione **Enter** o haga clic en cualquier otro lugar del panel para confirmar el valor.
4. Para cancelar la edición, presione **Escape** — se restaura el valor anterior.

El valor se limita automáticamente al rango válido de la perilla. Se admite el análisis con reconocimiento de configuración regional (por ejemplo, "12,5" funciona en configuraciones regionales con coma decimal).

## Tematización y colores de las perillas

En v26.6.1, los colores del componente de perilla ahora provienen del espacio de nombres `color.knob.*` del administrador de temas:
- `color.knob.background` — el fondo del anillo de la perilla
- `color.knob.foreground` — el arco del valor de la perilla
- `color.knob.handle` — el indicador de puntero de la perilla

El contenedor del applet de-eser está registrado como `applet/deess`, lo que permite anulaciones por contenedor de applet (por ejemplo, el de-eser puede tener un color de primer plano de perilla ámbar mientras que otros applets usan un color diferente). El texto de la etiqueta y el valor debajo de la perilla continúan usando `color.text.secondary` y `color.text.primary` respectivamente.

El widget de curva de respuesta de la cadena lateral también obtiene sus colores de las claves del tema:
- `color.background.0` — fondo de la curva
- `color.background.1` — líneas de la cuadrícula
- `color.text.label` — etiquetas de los ejes
- `color.accent.danger` — la curva de la banda de sibilancia (rojo suave)
- `color.accent.dim` — línea indicadora del umbral

## Consejos

- El bypass no restablece ningún valor de las perillas. Freq, Q, Thresh, Amount, Attack, Release y Slope conservan todos sus ajustes actuales cuando vuelve a habilitar la etapa.
- Las instancias del de-eser de TX y RX son independientes. Cambiar la configuración en una no afecta a la otra.
- La curva de respuesta de la cadena lateral y el medidor de reducción de ganancia reflejan la instancia actualmente activa (TX o RX) en la barra de título del panel.
- Puede usar la edición de valor en línea para ingresar valores exactos sin arrastrar las perillas. Esto es especialmente útil para ajustes finos o cuando sabe la configuración precisa que necesita.
- El botón Slope cicla a través de 12 → 24 → 36 → 48 dB/oct al hacer clic. Use una pendiente más pronunciada para un filtrado más estrecho alrededor de la frecuencia sibilante y reducir la atenuación colateral en el habla de rango medio.
- El contenedor del de-eser (`applet/deess`) permite a los autores de temas personalizar los colores de las perillas específicamente para el panel del de-eser sin afectar otras perillas de comp.
- En v26.7.4, el medidor de reducción de ganancia se actualiza en cada fotograma para una respuesta visual más suave durante transitorios de sibilancia rápidos, a costa de un uso de CPU ligeramente mayor durante pasajes dinámicos.

## Relacionados

- [Descripción general del De-Eser Aetherial](overview.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Establecer el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)

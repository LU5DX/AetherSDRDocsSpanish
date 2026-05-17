# Aetherial De-Esser

El Aetherial De-Esser domestica la sibilancia áspera de las letras 'S' y 'T' atenuando una banda estrecha cuando esta supera un umbral de cadena lateral. Muestra la respuesta del filtro de paso de banda de la cadena lateral, un medidor de reducción de ganancia de 24 dB y seis perillas de ajuste (Freq, Q, Thresh, Amount, Attack, Release).

**Instancias del applet:**
- **Instancia TX**: "Aetherial De-Esser" (se muestra en el Applet Panel acoplado)
- **Instancia RX**: "Aetherial De-Esser — RX" (accesible a través de la tira de canal de audio Aetherial Audio Channel Strip)

## Antes de comenzar

- AetherSDR debe estar abierto y la cadena de procesamiento Aetherial Audio (TXDSP o RXDSP) debe ser visible.
- La etapa DESS debe existir en el widget CHAIN. Si el de-esser nunca se ha habilitado, es posible que la etapa DESS no esté presente.
- El de-esser está disponible tanto en la ruta de audio TX como en la RX. Cada ruta tiene su propia instancia independiente del Aetherial De-Esser.

## Inhabilitar el de-esser desde la cadena

Elimine el Aetherial De-Esser de su ruta de audio TX o RX sin cambiar ninguna de sus configuraciones. Inhabilitar es útil cuando desea comparar audio tratado y no tratado, o deshabilitar temporalmente el de-essing para una sesión específica.

### Pasos para inhabilitar el de-esser en TX

1. Localice el widget CHAIN en el contenedor Aetherial Audio (TXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para activar o desactivar la inhabilitación.

### Pasos para inhabilitar el de-esser en RX

1. Localice el widget CHAIN en el contenedor Aetherial Audio (RXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para activar o desactivar la inhabilitación.

Cuando está inhabilitado, todo el mosaico del de-esser se muestra con opacidad reducida (55 % de lo normal). Al hacer clic una vez nuevamente, se rehabilita y restaura el mosaico a su opacidad completa. Las configuraciones `ClientDeEssTxEnabled` y `ClientDeEssRxEnabled` se actualizan de inmediato.

## Abrir el panel de configuración del de-esser

El panel de configuración del de-esser tiene dos instancias:
- **Instancia TX**: "Aetherial De-Esser — TX" (accesible desde la ruta TX de la tira de canal de audio Aetherial Audio Channel Strip)
- **Instancia RX**: "Aetherial De-Esser — RX" (accesible desde la ruta RX de la tira de canal de audio Aetherial Audio Channel Strip)

Para abrir la instancia adecuada:
1. Abra la tira de canal de audio Aetherial Audio Channel Strip.
2. Haga clic en la etapa **DESS** para abrir el panel de configuración del de-esser para esa ruta (TX o RX).
3. La barra de título del panel muestra "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX" según la ruta a la que accedió.

## Controles del de-esser

El panel del Aetherial De-Esser contiene los siguientes controles:

| Etiqueta | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Notas |
|---|---|---|---|---|---|
| Curva de respuesta de cadena lateral | indicador | — | — | — | ClientDeEssCurveWidget en modo compacto. Dibuja la respuesta del filtro de paso de banda con un punto móvil en la frecuencia central actual. |
| Barra de reducción de ganancia | medidor | — | 0 a 24 dB GR | — | Barra horizontal rojo suave, relleno desde la derecha. Escala máxima en 24 dB; una marca indica la cantidad típica de -6 dB. Se actualiza a ~30 Hz desde `ClientDeEss::gainReductionDb()`. |
| Freq | perilla | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` o `ClientDeEssRxFrequencyHz` | Mapeo logarítmico (1000 * 12^n). Establece la frecuencia central de la banda de sibilancia. Etiqueta '6.0 kHz' por encima de 1 kHz, 'N Hz' por debajo. |
| Q | perilla | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` o `ClientDeEssRxQ` | Mapeo lineal. Establece el ancho de banda de la banda de sibilancia — Q más alto = más estrecho. Etiqueta 'X.XX'. |
| Thresh | perilla | -30.0 dB | -60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` o `ClientDeEssRxThresholdDb` | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar la banda. |
| Amount | perilla | -6.0 dB | -24.0 a 0.0 dB | `ClientDeEssTxAmountDb` o `ClientDeEssRxAmountDb` | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción. |
| Attack | perilla | 1.0 ms | 0.1 a 30.0 ms | `ClientDeEssTxAttackMs` o `ClientDeEssRxAttackMs` | Mapeo exponencial (0.1 * 300^n). Establece la rapidez con la que el de-esser responde una vez que la sibilancia supera el umbral. Presente en la tira de canal StripDeEssPanel (RX y TX). El ClientDeEssApplet acoplado omite esta perilla. |
| Release | perilla | 100 ms | 10.0 a 500.0 ms | `ClientDeEssTxReleaseMs` o `ClientDeEssRxReleaseMs` | Mapeo exponencial (10 * 50^n). Establece la rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Presente en la tira de canal StripDeEssPanel (RX y TX). El ClientDeEssApplet acoplado omite esta perilla. |

## Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Punto de frecuencia central | fijo en el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Barra de reducción de ganancia | vacía, relleno rojo suave | Atenuación actual aplicada a la banda de sibilancia. |

## Edición de valores en línea en las perillas

Las perillas del de-esser (Freq, Q, Thresh, Amount, Attack, Release) admiten la edición de valores en línea desde la versión v26.5.2.1. En lugar de arrastrar la perilla, puede escribir un valor directamente.

### Para editar un valor de perilla mediante la edición en línea

1. Haga clic en el texto del valor debajo de cualquier perilla del de-esser. Aparece un pequeño campo de texto, delineado en cian cuando está enfocado.
2. Escriba el nuevo valor. Puede incluir unidades (por ejemplo, "6 kHz", "-24.0 dB", "100 ms") o solo el número (por ejemplo, "6000", "2.0", "0.1").
3. Presione **Enter** o haga clic en cualquier otro lugar del panel para confirmar el valor.
4. Para cancelar la edición, presione **Escape** — se restaura el valor anterior.

El valor se limita automáticamente al rango válido de la perilla. Se admite el análisis sensible a la configuración regional (por ejemplo, "12,5" funciona en configuraciones regionales con coma decimal).

## Consejos

- Inhabilitar no restablece ningún valor de perilla. Freq, Q, Thresh y Amount conservan su configuración actual cuando vuelve a habilitar la etapa.
- Las instancias del de-esser en TX y RX son independientes. Cambiar la configuración en una no afecta a la otra.
- La curva de respuesta de la cadena lateral y el medidor de reducción de ganancia reflejan la instancia actualmente activa (TX o RX) en la barra de título del panel.
- Puede usar la edición de valores en línea para ingresar valores exactos sin arrastrar las perillas. Esto es especialmente útil para ajustes precisos o cuando conoce la configuración exacta que necesita.

## Relacionados

- [Descripción general del Aetherial De-Esser](overview.md)
- [Barrer la frecuencia para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Establecer el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)

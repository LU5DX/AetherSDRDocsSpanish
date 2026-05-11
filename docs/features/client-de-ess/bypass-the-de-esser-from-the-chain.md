# Desescuchador Aetherial

El Desescuchador Aetherial doma la sibilancia áspera de las 'S' y 'T' atenuando una banda estrecha cuando supera un umbral de cadena lateral. Muestra la respuesta del filtro de paso de banda de la cadena lateral, un medidor de reducción de ganancia de 24 dB y seis perillas de ajuste (Freq, Q, Thresh, Amount, Attack, Release).

**Instancias del applet:**
- **Instancia TX**: "Aetherial De-Esser" (se muestra en el Applet Panel acoplado)
- **Instancia RX**: "Aetherial De-Esser — RX" (accesible a través del Aetherial Audio Channel Strip)

## Antes de comenzar

- AetherSDR debe estar abierto y la cadena de procesamiento de Aetherial Audio (TXDSP o RXDSP) debe estar visible.
- La etapa DESS debe existir en el widget CHAIN. Si el desescuchador nunca se ha habilitado, la etapa DESS puede no estar presente.
- El desescuchador está disponible tanto en las rutas de audio TX como RX. Cada ruta tiene su propia instancia independiente del Desescuchador Aetherial.

## Bypass del desescuchador desde la cadena

Elimine el Desescuchador Aetherial de su ruta de audio TX o RX sin cambiar ninguno de sus ajustes. El bypass es útil cuando desea comparar audio tratado y no tratado, o deshabilitar temporalmente el desescuchado para una sesión en particular.

### Pasos para el bypass del desescuchador TX

1. Localice el widget CHAIN en el contenedor de Aetherial Audio (TXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga un solo clic en la etapa **DESS** para activar o desactivar el bypass.

### Pasos para el bypass del desescuchador RX

1. Localice el widget CHAIN en el contenedor de Aetherial Audio (RXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga un solo clic en la etapa **DESS** para activar o desactivar el bypass.

Cuando está en bypass, todo el mosaico del desescuchador se renderiza con opacidad reducida (55 % de lo normal). Al hacer clic nuevamente se rehabilita y restaura la opacidad completa del mosaico. Los ajustes `ClientDeEssTxEnabled` y `ClientDeEssRxEnabled` se actualizan de inmediato.

## Apertura del panel de ajustes del desescuchador

El panel de ajustes del desescuchador tiene dos instancias:
- **Instancia TX**: "Aetherial De-Esser — TX" (accesible desde la ruta TX del Aetherial Audio Channel Strip)
- **Instancia RX**: "Aetherial De-Esser — RX" (accesible desde la ruta RX del Aetherial Audio Channel Strip)

Para abrir la instancia adecuada:
1. Abra el Aetherial Audio Channel Strip.
2. Haga clic en la etapa **DESS** para abrir el panel de ajustes del desescuchador para esa ruta (TX o RX).
3. La barra de título del panel muestra "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX" según la ruta a la que accedió.

## Controles del desescuchador

El panel del Desescuchador Aetherial contiene los siguientes controles:

| Etiqueta | Tipo | Valor predeterminado | Rango válido | Clave de ajuste | Notas |
|---|---|---|---|---|---|
| Curva de respuesta de cadena lateral | indicador | — | — | — | ClientDeEssCurveWidget en modo compacto. Dibuja la respuesta del filtro de paso de banda con un punto móvil en la frecuencia central actual. Las etiquetas del eje de frecuencia se renderizan como QStaticText para mejorar el rendimiento. |
| Barra de reducción de ganancia | medidor | — | 0 a 24 dB GR | — | Franja horizontal rojo suave, rellena desde la derecha. Escala máxima en 24 dB; una marca indica el valor típico de -6 dB. Se actualiza a ~30 Hz desde `ClientDeEss::gainReductionDb()`. |
| Freq | perilla | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` o `ClientDeEssRxFrequencyHz` | Mapeo logarítmico (1000 * 12^n). Establece la frecuencia central de la banda de sibilancia. Etiqueta '6.0 kHz' por encima de 1 kHz, 'N Hz' por debajo. |
| Q | perilla | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` o `ClientDeEssRxQ` | Mapeo lineal. Establece el ancho de banda de la banda de sibilancia — Q más alto = más estrecho. Etiqueta 'X.XX'. |
| Thresh | perilla | -30.0 dB | -60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` o `ClientDeEssRxThresholdDb` | Mapeo lineal. Nivel por encima del cual el desescuchador comienza a atenuar la banda. |
| Amount | perilla | -6.0 dB | -24.0 a 0.0 dB | `ClientDeEssTxAmountDb` o `ClientDeEssRxAmountDb` | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción. |
| Attack | perilla | 1.0 ms | 0.1 a 30.0 ms | `ClientDeEssTxAttackMs` o `ClientDeEssRxAttackMs` | Mapeo exponencial (0.1 * 300^n). Establece qué tan rápido responde el desescuchador una vez que la sibilancia supera el umbral. Presente en el StripDeEssPanel del Channel Strip (RX y TX). El ClientDeEssApplet acoplado omite esta perilla. |
| Release | perilla | 100 ms | 10.0 a 500.0 ms | `ClientDeEssTxReleaseMs` o `ClientDeEssRxReleaseMs` | Mapeo exponencial (10 * 50^n). Establece qué tan rápido regresa la ganancia después de que la sibilancia cae por debajo del umbral. Presente en el StripDeEssPanel del Channel Strip (RX y TX). El ClientDeEssApplet acoplado omite esta perilla. |

## Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Punto de frecuencia central | en reposo sobre el pico de la curva | Marca la frecuencia central de sibilancia actualmente sintonizada en la curva de respuesta. |
| Franja de reducción de ganancia | vacía, relleno rojo suave | Atenuación actual aplicada a la banda de sibilancia. |

## Consejos

- El bypass no restablece ningún valor de las perillas. Freq, Q, Thresh y Amount conservan sus ajustes actuales cuando vuelve a habilitar la etapa.
- Las instancias del desescuchador TX y RX son independientes. Cambiar los ajustes en una no afecta a la otra.
- La curva de respuesta de la cadena lateral y el medidor de reducción de ganancia reflejan la instancia actualmente activa (TX o RX) en la barra de título del panel.
- Las etiquetas del eje de frecuencia en la curva de respuesta de la cadena lateral utilizan QStaticText almacenado en caché para mejorar el rendimiento de renderizado.

## Relacionado

- [Descripción general del Desescuchador Aetherial](overview.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el desescuchado más transparente](dial-amount-for-the-most-transparent-de-essing.md)

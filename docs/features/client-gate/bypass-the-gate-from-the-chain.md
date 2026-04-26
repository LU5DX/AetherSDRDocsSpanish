# Omitir la puerta en la cadena

El widget CHAIN controla si la etapa Gate está activa u omitida en las rutas de audio TX y RX. Al omitirla, la puerta se elimina del procesamiento de señal sin modificar ninguno de sus parámetros ajustados.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión con una radio para omitir la puerta, pero la etapa Gate ya debe estar habilitada en el widget CHAIN para que la omisión tenga sentido.
- Ubique el widget CHAIN del lado que desea omitir (TX o RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Encuentre el widget CHAIN correspondiente a la ruta que desea modificar — TX o RX.
2. Haga clic simple en la etapa **GATE** del widget CHAIN.
   - Un clic simple alterna el estado de omisión de esa etapa. Cuando está omitida, la puerta se elimina de la cadena; `ClientGateTxEnabled` (TX) o `ClientGateRxEnabled` (RX) se establece como deshabilitado según corresponda.
3. Para volver a habilitar la puerta, haga clic simple en la etapa **GATE** nuevamente.

## Consejos

- Omitir la puerta mediante el widget CHAIN deja sin cambios los cinco valores de los controles — Thresh, Ratio, Attack, Release y Floor —. Su configuración se conserva y surte efecto de inmediato al volver a habilitar la etapa.
- Hacer doble clic en la etapa **GATE** del widget CHAIN abre el editor flotante de la puerta ("Aetherial Gate — TX" o "Aetherial Gate — RX") en lugar de alternar la omisión. Use únicamente el clic simple para omitir.
- Los subcontenedores "Aetherial TX Gate" y "Aetherial AGC-T" se ocultan cuando la etapa Gate no está habilitada. Si el subcontenedor desaparece tras la omisión, este es el comportamiento esperado.

## Relacionado

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Monitorear la GR en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)

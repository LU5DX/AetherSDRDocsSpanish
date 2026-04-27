# Habilitar APD para linealizar el transmisor

APD (Adaptive Pre-Distortion, predistorsión adaptativa) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al amplificador de potencia. Actívelo para mejorar la pureza espectral, especialmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. APD es una función del lado del radio y requiere una conexión activa.
- Abra el applet TX Controls. Si no está visible, haga clic en el botón TX tray en la barra lateral derecha.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD para activar la predistorsión adaptativa. El fondo del botón cambia a verde cuando está habilitado.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se ilumina en verde mientras el radio recopila datos de calibración.
   - **Avail** se ilumina en verde cuando la calibración está completa pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado apagado y los tres indicadores se atenúan.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado |
|---------|------|----------------|----------------|
| APD | Botón de alternancia | Habilita o deshabilita la predistorsión adaptativa en el radio. Verde cuando está activo, apagado cuando está inactivo. | Off |
| Active | Indicador | Se ilumina en verde cuando APD está activo y el ecualizador se aplica a la señal. | Dim |
| Cal | Indicador | Se ilumina en verde cuando APD está activo y el radio aún está calibrando. | Dim |
| Avail | Indicador | Se ilumina en verde cuando APD está activo y hay un resultado de calibración disponible pero aún no aplicado. | Dim |

La progresión normal después de habilitar APD es: Cal → Avail → Active.

## Consejos

- La calibración de APD se realiza automáticamente tras habilitarlo. No es necesario transmitir manualmente para activarla; espere a que los indicadores avancen por la secuencia Cal → Avail → Active.
- Si deshabilita y vuelve a habilitar APD, la secuencia de calibración se reinicia desde Cal.

## Temas relacionados

- [Descripción general de TX Controls](overview.md)
- [Ejecutar una prueba de dos tonos](run-a-two-tone-tune.md)
- [Ajustar la potencia de salida RF](set-rf-output-power.md)

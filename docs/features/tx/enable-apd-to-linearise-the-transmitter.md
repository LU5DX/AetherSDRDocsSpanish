# Habilitar APD para linealizar el transmisor

APD (Adaptive Pre-Distortion, predistorsión adaptativa) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al amplificador de potencia. Habilítelo para mejorar la pureza espectral, especialmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. APD es una función del lado del equipo y requiere una conexión activa.
- Abra el applet TX Controls. Si no está visible, haga clic en el botón TX del panel lateral derecho.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD para activar la predistorsión adaptativa. El fondo del botón cambia a verde cuando está habilitado.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se ilumina en verde mientras el equipo recopila datos de calibración.
   - **Avail** se ilumina en verde cuando la calibración se ha completado pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado apagado y los tres indicadores se oscurecen.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| APD | Botón de alternancia | Habilita o deshabilita la predistorsión adaptativa en el equipo. Verde cuando está activo, apagado cuando está inactivo. |
| Active | Indicador | Se ilumina en verde cuando APD está activo y el ecualizador se aplica a la señal. |
| Cal | Indicador | Se ilumina en verde cuando APD está activo y el equipo aún está calibrando. |
| Avail | Indicador | Se ilumina en verde cuando APD está activo y hay una calibración disponible pero no aplicada. |

La secuencia normal tras habilitar APD es: Cal → Avail → Active.

## Consejos

- La calibración de APD se realiza automáticamente después de habilitarlo. No es necesario transmitir manualmente para activarla; espere a que los indicadores avancen por la secuencia Cal → Avail → Active.
- Si deshabilita y vuelve a habilitar APD, la secuencia de calibración reinicia desde Cal.

## Comportamiento del botón ATU

A partir de la versión v0.9.5.1, el botón ATU utiliza una alternancia por frecuencia que refleja el comportamiento de SmartSDR:

- **Primer clic** (o cualquier clic tras un cambio de frecuencia): inicia un nuevo ciclo de sintonización del ATU.
- **Segundo clic en la misma frecuencia**, cuando el ATU informa una coincidencia exitosa: pone el sintonizador en modo bypass.
- **Clic tras cualquier cambio de frecuencia**: siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior era exitoso.

El estado de bypass se borra automáticamente cuando cambia la frecuencia de transmisión, por lo que el siguiente clic iniciará una nueva sintonización en lugar de activar el bypass. No hay cambios en la etiqueta ni en la apariencia del botón ATU; los indicadores **Success**, **Byp** y **Mem** situados debajo del botón continúan reflejando el estado del ATU como antes.

| Indicador | Tipo | Comportamiento |
|-----------|------|----------------|
| Success | Indicador | Se ilumina en verde cuando el ATU informa una coincidencia exitosa o correcta. |
| Byp | Indicador | Se ilumina en naranja cuando el ATU está en bypass o bypass manual. |
| Mem | Indicador | Se ilumina en verde cuando el ATU utiliza una memoria almacenada. |

## Temas relacionados

- [Descripción general de TX Controls](overview.md)
- [Ejecutar una sintonización de dos tonos](run-a-two-tone-tune.md)
- [Ajustar la potencia de salida RF](set-rf-output-power.md)

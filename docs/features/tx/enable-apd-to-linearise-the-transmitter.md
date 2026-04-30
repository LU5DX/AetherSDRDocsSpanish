# Habilitar APD para Linearizar el Transmisor

APD (Adaptive Pre-Distortion) reduce la no-linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al PA. Habilítelo para mejorar la pureza espectral, particularmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. APD es una función del lado de la radio y requiere una conexión activa.
- Abra el applet TX Controls. Si no es visible, haga clic en el botón TX tray en la barra lateral derecha.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD para activar la pre-distorsión adaptativa. El fondo del botón cambia a verde cuando está habilitado.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se ilumina en verde mientras la radio recopila datos de calibración.
   - **Avail** se ilumina en verde cuando la calibración está completa pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado apagado y los tres indicadores se oscurecen.

## Qué hace cada control

| Control | Tipo                                                                                                                                               | Comportamiento                                                                                                                                                                                   |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| APD     | Botón de alternancia                                                                                                                                      | Habilita o deshabilita la pre-distorsión adaptativa en la radio. Verde cuando está activado, apagado cuando está desactivado.                                                                                                   |
| Active  | Indicador                                                                                                                                          | Se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente a la señal.                                                                                                              |
| Cal     | Se ilumina cuando APD está activado, el ecualizador aún no está activo y la radio reporta apdConfigurable=0 (calibración aún en progreso).                      | v0.9.3: lógica del indicador actualizada — Cal se ilumina cuando apdOn && !eqActive && !apdConfigurable.                                                                                                  |
| Avail   | Se ilumina cuando APD está activado, el ecualizador aún no está activo y la radio reporta apdConfigurable=1 (calibración disponible y en espera de aplicación). | v0.9.3: lógica del indicador actualizada — Avail se ilumina cuando apdOn && !eqActive && apdConfigurable. Los usuarios de APD externo (FLEX-8x00, fw 4.2.18+) configuran el puerto del muestreador en Radio Setup > APD tab. |

La progresión normal después de habilitar APD es: Cal → Avail → Active.

## Consejos

- La calibración de APD se realiza automáticamente después de habilitarlo. No es necesario transmitir manualmente para activarla; espere a que los indicadores pasen por Cal → Avail → Active.
- Si deshabilita y vuelve a habilitar APD, la secuencia de calibración se reinicia desde Cal.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Ejecutar un Tune de Dos Tonos](run-a-two-tone-tune.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)

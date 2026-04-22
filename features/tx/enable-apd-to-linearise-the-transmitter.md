# Activar APD para linealizar el transmisor

APD (Predistorsión Adaptativa) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal de salida. Actívelo cuando desee mejorar la calidad de la señal y reducir los productos de IMD en el aire.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. APD es una función del lado del radio y requiere una conexión activa.
- El applet TX debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón TX del panel lateral derecho.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD. El fondo del botón se vuelve verde cuando APD está activado.
3. Observe los indicadores de estado a la derecha de APD:
   - **Cal** se ilumina en verde mientras el radio recopila datos de calibración.
   - **Avail** se ilumina en verde cuando una calibración está lista pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador está aplicado y APD está completamente operativo.
4. Espere a que **Active** se ilumine. No se requiere ninguna acción adicional.

Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado apagado y los tres indicadores se atenúan.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| APD | Botón alternante | Activa o desactiva la Predistorsión Adaptativa en el radio. Verde cuando está encendido, apagado cuando está desactivado. | Desactivado |
| Active | Indicador | Se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente a la señal de transmisión. | Apagado |
| Cal | Indicador | Se ilumina en verde cuando APD está activado y el radio aún recopila datos de calibración. | Apagado |
| Avail | Indicador | Se ilumina en verde cuando APD está activado y un resultado de calibración está disponible pero aún no se ha aplicado. | Apagado |

La progresión normal tras activar APD es: **Cal** → **Avail** → **Active**.

## Consejos

- Si **Cal** permanece iluminado durante un tiempo prolongado, transmitir (aunque sea brevemente con MOX o TUNE) proporciona al radio datos de señal para completar la calibración más rápido.
- El estado de APD se controla a nivel del radio. Si se desconecta y vuelve a conectar, AetherSDR reflejará el estado de APD que el radio tenga en ese momento.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Iniciar una portadora de ajuste para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)

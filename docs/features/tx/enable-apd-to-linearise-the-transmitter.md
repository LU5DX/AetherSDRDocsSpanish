# Activar APD para linealizar el transmisor

APD (Adaptive Pre-Distortion) reduce la no linealidad del transmisor calibrando y aplicando un ecualizador a la salida del excitador. Actívelo cuando desee mejorar la calidad de la señal y reducir las emisiones espurias en transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. APD requiere una conexión de radio activa.
- El applet TX debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón TX del panel lateral derecho.

## Pasos

1. En el Panel de Applets, localice la fila en la parte inferior del applet TX Controls que contiene el botón APD.
2. Haga clic en APD. El fondo del botón se vuelve verde cuando APD está activado.
3. Observe los indicadores de estado a la derecha de APD:
   - **Cal** se ilumina en verde mientras el radio está calibrando.
   - **Avail** se ilumina en verde cuando una calibración ha finalizado pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador está aplicado y la predistorsión está en funcionamiento.

No se requiere ninguna acción adicional. El radio avanza de Cal a Avail a Active de forma automática.

Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado predeterminado (apagado) y los tres indicadores se apagan.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado |
|---|---|---|---|
| APD | Botón de alternancia | Activa o desactiva la predistorsión adaptativa en el radio. Fondo verde cuando está activado. | Off |
| Active | Indicador | Se ilumina en verde cuando APD está activado y el ecualizador está aplicado activamente. | Apagado |
| Cal | Indicador | Se ilumina en verde cuando APD está activado y aún está calibrando. | Apagado |
| Avail | Indicador | Se ilumina en verde cuando APD está activado y hay un resultado de calibración disponible pero aún no aplicado. | Apagado |

## Consejos

- Los tres indicadores muestran la progresión en orden: Cal → Avail → Active. Si el indicador permanece en Cal durante un período prolongado, es posible que el radio aún esté recopilando datos de transmisiones en curso.
- APD opera sobre la salida del excitador. Verifique los medidores RF Pwr y SWR durante el funcionamiento normal para confirmar que el transmisor opera dentro del rango esperado antes de activar APD.

## Temas relacionados

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia de salida de RF](set-rf-output-power.md)
- [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)

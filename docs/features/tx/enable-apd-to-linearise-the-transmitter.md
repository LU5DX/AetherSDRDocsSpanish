# Habilitar APD para Linealizar el Transmisor

APD (Predistorsión Adaptativa) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al PA. Actívelo para mejorar la pureza espectral, particularmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. APD es una función del lado de la radio y requiere una conexión activa.
- Abra el applet TX Controls. Si no está visible, haga clic en el botón de la bandeja TX en la barra lateral derecha.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD para activar la predistorsión adaptativa. El fondo del botón se vuelve verde cuando está habilitado.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se ilumina en verde mientras la radio recopila datos de calibración.
   - **Avail** se ilumina en verde cuando una calibración está completa pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado apagado y los tres indicadores se atenúan.

## Qué hace cada control

| Control | Tipo           | Comportamiento                                                                                      |
|---------|----------------|-----------------------------------------------------------------------------------------------------|
| APD     | Botón de alternancia | Activa o desactiva la predistorsión adaptativa en la radio. Verde cuando está activado, apagado cuando no. |
| Active  | Indicador      | Iluminado en verde cuando APD está activado y el ecualizador se aplica activamente a la señal.      |
| Cal     | Indicador      | Iluminado en verde cuando APD está activado y la radio aún está calibrando.                         |
| Avail   | Indicador      | Iluminado en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.  |

La progresión normal después de habilitar APD es: Cal → Avail → Active.

## Consejos

- La calibración APD se realiza automáticamente después de habilitarla. No necesita transmitir manualmente para activarla; espere a que los indicadores avancen por Cal → Avail → Active.
- Si desactiva y vuelve a activar APD, la secuencia de calibración se reinicia desde Cal.

## Comportamiento del botón ATU

A partir de la v0.9.5.1, el botón ATU utiliza una alternancia por frecuencia que refleja el comportamiento de SmartSDR:

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonización ATU.
- **Segundo clic en la misma frecuencia**, cuando el ATU informa una coincidencia exitosa: cambia el sintonizador a bypass.
- **Clic después de cualquier cambio de frecuencia**: siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior fue exitoso.

El estado de bypass se borra automáticamente cuando cambia la frecuencia de transmisión, por lo que el siguiente clic iniciará una nueva sintonización en lugar de hacer bypass. No hay cambios en la etiqueta o apariencia del botón ATU; los indicadores **Success**, **Byp** y **Mem** debajo del botón continúan reflejando el estado del ATU como antes.

| Indicador | Tipo      | Comportamiento                                                            |
|-----------|-----------|---------------------------------------------------------------------------|
| Success   | Indicador | Se ilumina en verde cuando el ATU informa una coincidencia exitosa o OK.  |
| Byp       | Indicador | Se ilumina en naranja cuando el ATU está en bypass o bypass manual.       |
| Mem       | Indicador | Se ilumina en verde cuando el ATU está usando una memoria almacenada.     |

## Botón MOX y tonos Quindar (v0.9.7)

En v0.9.7, hacer clic en MOX se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Esto significa:

- **Activar (clic en MOX encendido):** si Quindar está habilitado en la tira de canales de audio y el slice TX activo está en un modo telefónico, el tono K se reproduce antes de que el transmisor active la transmisión.
- **Desactivar (clic en MOX apagado):** el tono BK se reproduce después de que el transmisor desactive la transmisión.
- Si Quindar está deshabilitado, o el slice TX activo no está en un modo telefónico, MOX se comporta como antes y activa el transmisor inmediatamente.

La apariencia del botón no cambia: el botón MOX se vuelve rojo mientras el transmisor está activo y vuelve a su estado apagado cuando el transmisor está desactivado.

| Control | Tipo           | Comportamiento                                                                                                                                                                   |
|---------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MOX     | Botón de alternancia | Alterna la transmisión manual. En v0.9.7, se enruta a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar PTT en modos telefónicos cuando Quindar está habilitado. El botón se vuelve rojo mientras TX está activo. |

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Ejecutar una sintonización de dos tonos](run-a-two-tone-tune.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)

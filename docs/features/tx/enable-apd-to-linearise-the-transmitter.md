# Activar la APD para linealizar el transmisor

La APD (predistorsión adaptativa) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al PA. Actívela para mejorar la pureza espectral, particularmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La APD es una función del lado de la radio y requiere una conexión activa.
- Abra el applet TX Controls. Si no está visible, haga clic en el botón de la bandeja TX en la barra lateral derecha.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD para activar la predistorsión adaptativa. El fondo del botón cambia a verde cuando está activada.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se ilumina en verde mientras la radio recopila datos de calibración.
   - **Avail** se ilumina en verde cuando la calibración está completa pero aún no se ha aplicado.
   - **Active** se ilumina en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar la APD, haga clic en APD nuevamente. El botón vuelve a su estado apagado y los tres indicadores se atenúan.

## Qué hace cada control

| Control | Tipo            | Comportamiento                                                                                              |
|---------|-----------------|-------------------------------------------------------------------------------------------------------------|
| APD     | Botón de alternancia | Activa o desactiva la predistorsión adaptativa en la radio. Verde cuando está activada, apagado cuando no. |
| Active  | Indicador       | Iluminado en verde cuando la APD está activada y el ecualizador se aplica activamente a la señal.          |
| Cal     | Indicador       | Iluminado en verde cuando la APD está activada y la radio aún está calibrando.                              |
| Avail   | Indicador       | Iluminado en verde cuando la APD está activada y hay una calibración disponible pero aún no aplicada.      |

La progresión normal después de activar la APD es: Cal → Avail → Active.

## Consejos

- La calibración de la APD se realiza automáticamente después de activarla. No necesita transmitir manualmente para iniciarla; espere a que los indicadores avancen por Cal → Avail → Active.
- Si desactiva y vuelve a activar la APD, la secuencia de calibración se reinicia desde Cal.

## Comportamiento del botón ATU

El botón ATU utiliza una alternancia por frecuencia que refleja el comportamiento de SmartSDR:

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonización del ATU.
- **Segundo clic en la misma frecuencia**, cuando el ATU informa una coincidencia exitosa: cambia el sintonizador a bypass.
- **Clic después de cualquier cambio de frecuencia**: siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior fue exitoso.

El estado de bypass se borra automáticamente cuando cambia la frecuencia de transmisión, por lo que el siguiente clic iniciará una nueva sintonización en lugar de un bypass. No hay cambio en la etiqueta o apariencia del botón ATU; los indicadores **Success**, **Byp** y **Mem** debajo del botón continúan reflejando el estado del ATU como antes.

| Indicador | Tipo      | Comportamiento                                                        |
|-----------|-----------|-----------------------------------------------------------------------|
| Success   | Indicador | Se ilumina en verde cuando el ATU informa una coincidencia exitosa u OK. |
| Byp       | Indicador | Se ilumina en naranja cuando el ATU está en bypass o bypass manual.   |
| Mem       | Indicador | Se ilumina en verde cuando el ATU está usando una memoria almacenada. |

### Menú contextual del botón ATU

Haga clic derecho en el botón ATU para abrir un menú contextual con dos acciones:

| Acción                      | Comportamiento                                                                                                         |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------|
| Pre-tune bands…             | Abre el cuadro de diálogo Pre-Tune del ATU para barrer y almacenar configuraciones del sintonizador en todas las bandas. Habilitado solo cuando MEM está activado. |
| Clear ATU memories…         | Borra todas las memorias del ATU almacenadas en la radio. Aparece un cuadro de diálogo de confirmación antes de borrar. |

## Comportamiento del botón TUNE

Haga clic en TUNE para iniciar o detener una portadora de sintonización. La etiqueta del botón cambia a **TUNING...** con un fondo rojo mientras la portadora está activa.

### Menú contextual del botón TUNE

Haga clic derecho en el botón TUNE para elegir la forma de la portadora para el próximo ciclo de sintonización:

| Acción      | Comportamiento                                                         |
|-------------|------------------------------------------------------------------------|
| Mono Tone   | Establece la portadora de sintonización a un solo tono. Marcado si este es el modo actual. |
| Two Tone    | Establece la portadora de sintonización a dos tonos. Marcado si este es el modo actual. |

La selección es transitoria de un solo uso: el modo de sintonización de la radio vuelve a un solo tono tras los ciclos de encendido. AetherSDR no persiste la elección en AppSettings.

## Deslizadores RF Power / Tune Power

| Control    | Tipo        | Comportamiento                                                                                                                                |
|------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Deslizador  | Establece el nivel de potencia de RF de transmisión como porcentaje del máximo (0–100 %). Valor predeterminado: 100 %. Durante el arrastre, muestra el valor actual como "XX %" sobre el control. |
| Tune Pwr   | Deslizador  | Establece el nivel de potencia de la portadora de sintonización como porcentaje del máximo (0–100 %). Valor predeterminado: 10 %. Durante el arrastre, muestra el valor actual como "XX %" sobre el control. |

## Selector de perfil TX

Seleccione un perfil TX del cuadro combinado para cargarlo en la radio. Los perfiles se obtienen de la lista de perfiles de la radio.

## Medidores RF Pwr y SWR

La potencia directa se muestra como un indicador de barra horizontal. La escala cambia según el modelo de radio (sin amplificador 0–120 W, o Aurora 500W 0–600 W). El indicador se vuelve rojo por encima de 100 W (sin amplificador) o 500 W (Aurora).

Pico sostenido PEP: un valor pico se mantiene durante 2 segundos y luego decae suavemente al valor actual. El pico se borra inmediatamente cuando el transmisor se desactiva para evitar lecturas persistentes en los sobres.

La ROE se muestra como un indicador de barra horizontal. Rango 1.0–3.0. El indicador se vuelve rojo por encima de 2.5.

## Botón MOX y tonos Quindar

Al hacer clic en MOX, se enruta a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Esto significa:

- **Activar (clic en MOX encendido):** si Quindar está habilitado en Audio Channel Strip y el slice TX activo está en un modo de telefonía, el tono K suena antes de que el transmisor se active.
- **Desactivar (clic en MOX apagado):** el tono BK suena después de que el transmisor se desactiva.
- Si Quindar está deshabilitado, o el slice TX activo no está en un modo de telefonía, MOX se comporta como antes y activa el transmisor inmediatamente.

La apariencia del botón no cambia: el botón MOX se vuelve rojo mientras el transmisor está activado y vuelve a su estado apagado cuando el transmisor está desactivado.

| Control | Tipo            | Comportamiento                                                                                                                                                         |
|---------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MOX     | Botón de alternancia | Alterna la transmisión manual. Se enruta a través del coordinador de tonos Quindar para que los tonos K/BK suenen al activar/desactivar PTT en modos de telefonía cuando Quindar está habilitado. El botón se pone rojo mientras TX está activado. |

## Botón ATU MEM

| Control | Tipo            | Comportamiento                                                             |
|---------|-----------------|----------------------------------------------------------------------------|
| MEM     | Botón de alternancia | Alterna la recuperación de memoria del ATU encendido/apagado. Deshabilitado cuando TGXL está en modo OPERATE. |

## Soporte de temas

A partir de la versión v26.6.1, el applet TX Controls utiliza colores conscientes del tema para todos los controles e indicadores. El relleno del deslizador, los colores de las etiquetas y los estados de los indicadores se adaptan al tema activo. Si usa un tema personalizado, estos controles respetarán el ámbito `applet/tx` en la definición del tema.

## Relacionado

- [Resumen de TX Controls](overview.md)
- [Ejecutar una sintonización de dos tonos](run-a-two-tone-tune.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)

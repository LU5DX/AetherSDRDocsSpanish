# Habilitar APD para Linealizar el Transmisor

APD (Adaptive Pre-Distortion) reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al PA. Actívelo para mejorar la pureza espectral, particularmente en SSB y modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. APD es una función del lado de la radio y requiere una conexión activa.
- Abra el applet TX Controls. Si no está visible, haga clic en el botón de la bandeja TX en la barra lateral derecha.

## Pasos

1. Localice el botón APD en la parte inferior del applet TX Controls.
2. Haga clic en APD para activar la predistorsión adaptativa. El fondo del botón cambia a verde cuando está habilitado.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se enciende en verde mientras la radio recopila datos de calibración.
   - **Avail** se enciende en verde cuando la calibración está completa pero aún no se ha aplicado.
   - **Active** se enciende en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar APD, haga clic en APD nuevamente. El botón vuelve a su estado sin iluminación y los tres indicadores se apagan.

## Qué hace cada control

| Control | Tipo           | Comportamiento                                                                                                  |
|---------|----------------|-----------------------------------------------------------------------------------------------------------------|
| APD     | Botón de alternancia | Activa o desactiva la predistorsión adaptativa en la radio. Verde cuando está activado, sin luz cuando está desactivado. |
| Active  | Indicador      | Se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente a la señal.                 |
| Cal     | Indicador      | Se ilumina en verde cuando APD está activado y la radio aún está calibrando.                                   |
| Avail   | Indicador      | Se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.             |

La progresión normal después de activar APD es: Cal → Avail → Active.

## Consejos

- La calibración APD se realiza automáticamente después de activarla. No necesita transmitir manualmente para activarla; espere a que los indicadores avancen por Cal → Avail → Active.
- Si desactiva y vuelve a activar APD, la secuencia de calibración se reinicia desde Cal.

## Comportamiento del botón ATU

El botón ATU utiliza una alternancia por frecuencia que refleja el comportamiento de SmartSDR:

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonización ATU.
- **Segundo clic en la misma frecuencia**, cuando el ATU informa una coincidencia exitosa: cambia el sintonizador a bypass.
- **Clic después de cualquier cambio de frecuencia**: siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior fue exitoso.

El estado de bypass se limpia automáticamente cuando cambia la frecuencia de transmisión, por lo que el siguiente clic iniciará una nueva sintonización en lugar de un bypass. No hay cambios en la etiqueta o apariencia del botón ATU; los indicadores **Success**, **Byp** y **Mem** debajo del botón continúan reflejando el estado del ATU como antes.

| Indicador | Tipo      | Comportamiento                                                         |
|-----------|-----------|------------------------------------------------------------------------|
| Success   | Indicador | Se ilumina en verde cuando el ATU informa una coincidencia exitosa u OK. |
| Byp       | Indicador | Se ilumina en naranja cuando el ATU está en bypass o bypass manual.      |
| Mem       | Indicador | Se ilumina en verde cuando el ATU utiliza una memoria almacenada.        |

### Menú contextual del botón ATU

Haga clic derecho en el botón ATU para abrir un menú contextual con dos acciones:

| Acción                        | Comportamiento                                                                                                          |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Pre-tune bands…               | Abre el diálogo ATU Pre-Tune para barrer y almacenar configuraciones del sintonizador en todas las bandas. Habilitado solo cuando MEM está activado. |
| Clear ATU memories…           | Elimina todas las memorias ATU almacenadas en la radio. Aparece un diálogo de confirmación antes de borrar.             |

## Comportamiento del botón TUNE

Haga clic en TUNE para iniciar o detener una portadora de sintonía. La etiqueta del botón cambia a **TUNING...** con un fondo rojo mientras la portadora está activa.

### Menú contextual del botón TUNE

Haga clic derecho en el botón TUNE para elegir la forma de la portadora para el próximo ciclo de sintonía:

| Acción      | Comportamiento                                                                                        |
|-------------|-------------------------------------------------------------------------------------------------------|
| Mono Tone   | Establece la portadora de sintonía en un solo tono. Marcado si este es el modo actual.                |
| Two Tone    | Establece la portadora de sintonía en dos tonos. Marcado si este es el modo actual.                   |

La selección es transitoria de un solo uso; el modo de sintonía de la radio vuelve al tono único después de ciclos de encendido. AetherSDR no persiste la elección en AppSettings.

## Deslizadores RF Power / Tune Power

| Control    | Tipo      | Comportamiento                                                                                                                                                                                                                                                                           |
|------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Deslizador | Establece el nivel de potencia de RF de transmisión como un porcentaje del máximo (0–100%). Predeterminado: 100%. Durante el arrastre, muestra el valor actual como "XX%" sobre el asa del deslizador. El valor se ajusta a la última posición establecida después de soltarlo.             |
| Tune Pwr   | Deslizador | Establece el nivel de potencia de la portadora de sintonía como un porcentaje del máximo (0–100%). Predeterminado: 10%. Durante el arrastre, muestra el valor actual como "XX%" sobre el asa del deslizador. El valor se ajusta a la última posición establecida después de soltarlo.       |

Cuando suelta cualquiera de los deslizadores, el valor se sincroniza desde el modelo de la radio, asegurando que el valor mostrado coincida con el estado real de la radio incluso si la radio rechazó el valor intermedio durante el arrastre.

## Selector de perfil TX

Seleccione un perfil TX del cuadro combinado para cargarlo en la radio. Los perfiles se toman de la lista de perfiles de la radio.

## Medidores RF Pwr y SWR

La potencia directa se muestra como un indicador de barra horizontal. La escala cambia según el modelo de la radio (básico 0–120 W, o Aurora 500W 0–600 W). El indicador se vuelve rojo por encima de 100 W (básico) o 500 W (Aurora).

Retención de pico PEP: la lectura máxima se mantiene durante 2 segundos, luego disminuye suavemente al valor actual. El pico se borra inmediatamente cuando el transmisor se desactiva para evitar lecturas persistentes entre transmisiones.

Pase el mouse sobre el indicador de RF Pwr para ver la lectura de potencia exacta en vatios (p. ej., "45 W").

El SWR se muestra como un indicador de barra horizontal. Rango 1.0–3.0. El indicador se vuelve rojo por encima de 2.5.

Pase el mouse sobre el indicador de SWR para ver la relación exacta en forma convencional (p. ej., "1.52:1").

## Botón MOX y tonos Quindar

Hacer clic en MOX pasa a través del coordinador de tonos Quindar en lugar de activar el transmisor directamente. Esto significa:

- **Activar (clic en MOX encendido):** si Quindar está habilitado en la tira de canales de audio (Audio Channel Strip) y la porción TX activa está en un modo de teléfono, el tono K se reproduce antes de que el transmisor se active.
- **Desactivar (clic en MOX apagado):** el tono BK se reproduce después de que el transmisor se desactiva.
- Si Quindar está deshabilitado, o la porción TX activa no está en un modo de teléfono, MOX se comporta como antes y activa el transmisor inmediatamente.

El botón MOX tiene una apariencia distintiva incluso cuando está inactivo (borde y texto en ámbar) para distinguirlo de los botones TUNE/ATU/MEM. El botón se vuelve rojo mientras el transmisor está activado y vuelve a su acento ámbar cuando el transmisor está apagado. Los colores de acento se pueden editar mediante temas con los tokens `color.tx.mox.*`.

| Control | Tipo           | Comportamiento                                                                                                                                                                     |
|---------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MOX     | Botón de alternancia | Activa/desactiva la transmisión manual. Pasa a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar PTT en modos de teléfono cuando Quindar está habilitado. El botón se vuelve rojo mientras TX está activado, acento ámbar cuando está inactivo. |

## Botón ATU MEM

| Control | Tipo           | Comportamiento                                                                   |
|---------|----------------|----------------------------------------------------------------------------------|
| MEM     | Botón de alternancia | Activa/desactiva la recuperación de memoria ATU. Deshabilitado cuando TGXL está en modo OPERATE. |

## Soporte de temas

A partir de la versión 26.6.1, el applet TX Controls utiliza colores adaptables al tema para todos los controles e indicadores. El relleno del deslizador, los colores de las etiquetas y los estados de los indicadores se adaptan al tema activo. Si utiliza un tema personalizado, estos controles respetarán el ámbito `applet/tx` en la definición del tema.

El botón MOX y los indicadores RF Pwr/SWR también admiten tokens de tema. El botón MOX utiliza `color.tx.mox.border`, `color.tx.mox.text`, `color.tx.mox.border.hover` y `color.tx.mox.text.hover` para su coloración de acento inactivo. Los tooltips al pasar el mouse sobre los indicadores utilizan el estilo de tooltip predeterminado del tema.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Ejecutar una sintonía de dos tonos](run-a-two-tone-tune.md)
- [Establecer la potencia de salida de RF](set-rf-output-power.md)

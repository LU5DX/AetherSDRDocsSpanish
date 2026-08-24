# Configurar la potencia de salida de RF

Use el control deslizante **RF Power** en el applet TX Controls para establecer el nivel de potencia de transmisión enviado a su antena. Ajustar esto antes de transmitir evita sobrecargar su amplificador o violar los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón de bandeja **TX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls. Aparece debajo del medidor **SWR**.
2. Arrastre el control deslizante hacia la izquierda o derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control deslizante se actualiza inmediatamente, mostrando el formato "XX%".
3. Confirme que el valor mostrado en la lectura es el que desea. El medidor **RF Pwr** reflejará la potencia directa real una vez que transmita.
4. Coloque el cursor del mouse sobre el medidor **RF Pwr** o **SWR** para ver la lectura numérica exacta en una información sobre herramientas emergente. La información emergente de **RF Pwr** muestra el valor en vatios (p. ej., "45 W"), y la de **SWR** muestra la relación en formato convencional (p. ej., "1.42:1"). Esto es útil para lecturas precisas entre marcas de escala.

## Qué hace cada control

| Control                  | Descripción                                                                          | Predeterminado |
|--------------------------|--------------------------------------------------------------------------------------|---------|
| Control deslizante **RF Power**      | Establece el nivel de potencia de RF de transmisión (0-100% del máximo). El valor arrastrado muestra el formato "XX%". | 100     |
| Control deslizante **Tune Pwr**      | Establece el nivel de potencia de la portadora de sintonía (0-100% del máximo). El valor arrastrado muestra el formato "XX%".    | 10      |
| Medidor **RF Pwr**         | Muestra la potencia directa real en la salida del excitador con retención de pico PEP. Coloque el cursor para ver el vataje exacto. | —       |
| Medidor **SWR**            | Muestra la relación de onda estacionaria en el excitador. Coloque el cursor para ver la relación exacta en formato N.N:1.  | —       |
| Cuadro combinado **TX Profile** | Selecciona un perfil de transmisión (p. ej., SSB, Digital) de los disponibles en la radio.    | —       |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W. Con el amplificador Aurora 500W, la zona roja comienza por encima de 500 W y la escala se extiende hasta 600 W.
- Puede establecer límites de potencia por banda independientemente de este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de sintonía y los ajustes de inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no un amplificador separado. Si está utilizando un amplificador externo, establezca este control deslizante al nivel de excitación que su amplificador espera.
- El medidor **RF Pwr** incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos y luego decae suavemente hacia el nivel de potencia actual. El pico se limpia inmediatamente a cero cuando el transmisor desactiva la transmisión.
- Los controles deslizantes de potencia ahora muestran valores como porcentajes (0-100%) de la potencia máxima para su modelo de radio, en lugar de vatios.
- Colocar el cursor sobre el medidor **RF Pwr** o **SWR** muestra una lectura numérica exacta en una información sobre herramientas emergente, eliminando la necesidad de estimar entre marcas de escala durante la transmisión.

## Uso del botón TUNE

El botón **TUNE** inicia o detiene una portadora de sintonía. Mientras está activo, el texto del botón cambia a "TUNING..." con un fondo rojo.

### Comportamiento del medidor durante TUNE

Cuando el transmisor no está activado, tanto el medidor **RF Pwr** como el **SWR** regresan inmediatamente a sus posiciones de reposo (0 W y 1.0:1 respectivamente). Esto evita que lecturas obsoletas permanezcan en la pantalla entre transmisiones.

### Menú contextual del botón TUNE

Al hacer clic derecho en el botón **TUNE** se abre un menú contextual para seleccionar la forma de la portadora para el siguiente ciclo de sintonía. Hay dos opciones disponibles:

- **Mono Tone** — Una única portadora de tono.
- **Two Tone** — Dos portadoras de tono simultáneas.

Seleccionar cualquiera de las opciones es un ajuste de una sola vez. El modo de sintonía de la radio se almacena en estado volátil y AetherSDR no conserva esta elección entre reinicios. El modo actualmente activo se muestra con una marca de verificación.

## Uso del botón MOX

El botón **MOX** activa manualmente el transmisor. El botón tiene un estilo visual distintivo: un borde y texto ámbar cuando está inactivo (modo de recepción) para identificarlo claramente como el botón de transmisión, y se vuelve rojo con un borde rojo brillante cuando está activo (modo de transmisión). Este color de acento se puede editar en el Theme Editor bajo los tokens `color.tx.mox.*`.

Cuando está activo, el botón se vuelve rojo ("QPushButton { background: #cc2222; border: 1px solid #ff4444; ...}").

En v0.9.7, hacer clic en **MOX** enruta la solicitud de PTT a través del coordinador de tono Quindar en lugar de activar la radio directamente. Esto significa:

- En modos de teléfono (SSB, AM, FM, etc.), si el chip **QUIN** está habilitado en la tira de canal de audio, el tono K se reproduce al activar MOX y el tono BK se reproduce al desactivarlo.
- Si Quindar está deshabilitado, o la slice de TX activa no está en un modo de teléfono, el comportamiento es idéntico a versiones anteriores: la radio se activa y desactiva inmediatamente.

No se requiere ningún cambio en la forma de operar el botón. Los tonos Quindar están controlados completamente por el ajuste **QUIN** en la tira de canal de audio.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en v0.9.5.1 para reflejar la alternancia por frecuencia que se encuentra en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonía ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya reporta una coincidencia exitosa (el indicador **Success** está encendido) y no ha cambiado de frecuencia desde la última sintonía, hacer clic en **ATU** nuevamente cambia el sintonizador a bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de frecuencia sintonizada se limpia automáticamente. El siguiente clic siempre inicia un nuevo ciclo de sintonía, incluso si el estado anterior fue exitoso.

El indicador **Byp** se enciende en naranja cuando el sintonizador está en bypass. El indicador **Success** se enciende en verde cuando hay una coincidencia activa. El indicador **Mem** se enciende en verde cuando el sintonizador utiliza una memoria almacenada.

| Escenario | Resultado del botón ATU |
|---|---|
| Sin sintonía previa, o la frecuencia ha cambiado | Inicia ciclo de sintonía |
| Coincidencia exitosa/OK, misma frecuencia que la última sintonía | Cambia a bypass |
| Bypass activo | Inicia un nuevo ciclo de sintonía en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transvertidor TGXL está en modo OPERATE, o cuando la radio no tiene sintonizador de antena instalado.

### Menú contextual del botón ATU

Al hacer clic derecho en el botón **ATU** se abre un menú contextual con dos opciones adicionales:

- **Pre-tune bands…** — Abre un diálogo para ejecutar un barrido de pre-sintonía en una o más bandas. Esta opción solo está disponible cuando las memorias ATU están habilitadas (el botón **MEM** está activado).
- **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias ATU almacenadas en la radio.

## Uso del botón de alternancia MEM

El botón **MEM** activa o desactiva la recuperación de memoria ATU. Cuando está habilitado, el sintonizador puede usar datos de sintonía almacenados para frecuencias previamente sintonizadas. Este botón está deshabilitado cuando el transvertidor TGXL está en modo OPERATE, o cuando la radio no tiene sintonizador de antena instalado.

## Uso del grupo APD (Adaptive Pre-Distortion)

El botón de alternancia **APD** habilita o deshabilita la pre-distorsión adaptativa en la radio. Cuando APD está activado, tres indicadores de estado muestran el progreso:

- **Cal** (verde) — APD está activado y aún calibrando.
- **Avail** (verde) — Hay una calibración disponible pero aún no aplicada.
- **Active** (verde) — El ecualizador está aplicado activamente.

La progresión típica es Cal → Avail → Active. Cuando APD está desactivado, los tres indicadores están atenuados.

Los controles APD solo se muestran cuando la radio admite pre-distorsión adaptativa. En radios sin esta función, todo el grupo APD está oculto.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio está realmente activada. Verifique que MOX esté activo (el botón **MOX** está rojo) o que su línea de PTT esté afirmada. También verifique que el control deslizante **RF Power** no esté en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — La conexión de la radio puede haberse interrumpido. Verifique el estado de la conexión y vuelva a conectarse mediante `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia una nueva sintonía aunque Success estaba encendido** — Confirme que no ha cambiado la frecuencia de transmisión desde la última sintonía. Cualquier cambio de frecuencia borra el registro de frecuencia sintonizada almacenado y fuerza un nuevo ciclo de sintonía.
- **Los tonos Quindar no se reproducen al usar MOX** — Confirme que la slice activa está en un modo de teléfono y que el chip **QUIN** está habilitado en la tira de canal de audio. Los tonos Quindar se suprimen en modos que no son de teléfono independientemente del ajuste QUIN.
- **Los botones ATU y MEM están deshabilitados** — La radio puede no tener sintonizador de antena instalado, o el transvertidor TGXL está en modo OPERATE. Coloque el cursor sobre el botón deshabilitado para ver el motivo en una información sobre herramientas.

## Relacionado

- [Descripción general de TX Controls](overview.md)
- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonía para verificar la SWR](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)

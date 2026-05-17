# Configurar la potencia de salida de RF

Use el control deslizante **RF Power** en el applet TX Controls para ajustar el nivel de potencia de transmisión enviado a su antena. Ajustarlo antes de transmitir evita sobrecargar su amplificador o violar los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet TX Controls debe estar visible. Si no lo está, haga clic en el botón **TX** en la bandeja de la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet TX Controls. Aparece debajo del medidor **SWR**.
2. Arrastre el control deslizante hacia la izquierda o la derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control deslizante se actualiza inmediatamente.
3. Confirme que el valor mostrado en la lectura sea el que desea. El medidor **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control             | Descripción                                          | Valor predeterminado |
|---------------------|------------------------------------------------------|---------|
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión enviado a la radio. | 100     |
| Medidor **RF Pwr**             | Muestra la potencia directa real en la salida del excitador. | —       |
| Medidor **SWR**                | Muestra la relación de onda estacionaria en el excitador. | —       |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda independientemente de este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de sintonización y los ajustes de inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no un amplificador separado. Si está utilizando un amplificador externo, ajuste este control deslizante al nivel de excitación que espera su amplificador.
- El medidor **RF Pwr** incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos, luego decae suavemente hacia el nivel de potencia actual. El pico se borra inmediatamente a cero cuando el transmisor desactiva la clave.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en v0.9.5.1 para reflejar la conmutación por frecuencia que se encuentra en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonización ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya informa una coincidencia exitosa (el indicador **Success** está encendido) y no ha cambiado de frecuencia desde la última sintonización, hacer clic en **ATU** nuevamente cambia el sintonizador a bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de frecuencia sintonizada se borra automáticamente. El siguiente clic siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior fue exitoso.

El indicador **Byp** se ilumina en naranja cuando el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando una coincidencia está activa. El indicador **Mem** se ilumina en verde cuando el sintonizador está usando una memoria almacenada.

| Escenario | Resultado del botón ATU |
|---|---|
| Sin sintonización previa, o la frecuencia ha cambiado | Inicia el ciclo de sintonización |
| Coincidencia Success/OK, misma frecuencia que la última sintonización | Cambia a bypass |
| Bypass activo | Inicia un nuevo ciclo de sintonización en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transvertidor TGXL está en modo OPERATE.

### Menú contextual del botón ATU

Hacer clic derecho en el botón **ATU** abre un menú contextual con dos opciones adicionales:

- **Pre-tune bands…** — Abre un diálogo para ejecutar un barrido de pre-sintonización en una o más bandas. Esta opción solo está disponible cuando las memorias ATU están habilitadas (el botón **MEM** está encendido).
- **Clear ATU memories…** — Solicita confirmación, luego borra todas las memorias ATU almacenadas en la radio.

## Uso del menú contextual del botón TUNE

Hacer clic derecho en el botón **TUNE** abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonización. Hay dos opciones disponibles:

- **Mono Tone** — Un único tono portador.
- **Two Tone** — Dos tonos portadores simultáneos.

Seleccionar cualquiera de las opciones es un ajuste de una sola vez. El modo de sintonización de la radio se almacena en un estado volátil y AetherSDR no conserva esta elección entre reinicios. El modo actualmente activo se muestra con una marca de verificación.

## Uso del botón MOX

El botón **MOX** activa manualmente el transmisor. Cuando está activo, el botón se vuelve rojo.

En v0.9.7, hacer clic en **MOX** enruta la solicitud PTT a través del coordinador de tonos Quindar en lugar de activar la radio directamente. Esto significa:

- En modos de teléfono (SSB, AM, FM, etc.), si el chip **QUIN** está habilitado en la Audio Channel Strip, el tono K se reproduce cuando activa MOX y el tono BK se reproduce cuando lo desactiva.
- Si Quindar está deshabilitado, o la tajada TX activa no está en un modo de teléfono, el comportamiento es idéntico a versiones anteriores: la radio activa y desactiva la clave inmediatamente.

No se requiere ningún cambio en la forma de operar el botón. Los tonos Quindar se controlan completamente mediante el ajuste **QUIN** en la Audio Channel Strip.

## Uso del grupo APD (Pre-Distorsión Adaptativa)

El botón de conmutación **APD** habilita o deshabilita la pre-distorsión adaptativa en la radio. Cuando APD está activado, tres indicadores de estado muestran el progreso:

- **Cal** (verde) — APD está activado y aún está calibrando.
- **Avail** (verde) — Hay una calibración disponible pero aún no se ha aplicado.
- **Active** (verde) — El ecualizador está aplicado activamente.

La progresión típica es Cal → Avail → Active. Cuando APD está desactivado, los tres indicadores están atenuados.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio esté realmente activada. Verifique que MOX esté activo (el botón **MOX** está rojo) o que su línea PTT esté activada. También verifique que el control deslizante **RF Power** no esté configurado en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — Es posible que la conexión de la radio se haya perdido. Verifique el estado de la conexión y vuelva a conectarse a través de `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia una nueva sintonización aunque Success estuviera encendido** — Confirme que no ha cambiado la frecuencia de transmisión desde la última sintonización. Cualquier cambio de frecuencia borra el registro de frecuencia sintonizada almacenado y fuerza un nuevo ciclo de sintonización.
- **Los tonos Quindar no se reproducen al usar MOX** — Confirme que la tajada activa esté configurada en un modo de teléfono y que el chip **QUIN** esté habilitado en la Audio Channel Strip. Los tonos Quindar se suprimen en modos que no son de teléfono, independientemente de la configuración QUIN.

## Relacionado

- [Resumen de TX Controls](overview.md)
- [Configurar la potencia de la portadora de sintonización](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonización para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)

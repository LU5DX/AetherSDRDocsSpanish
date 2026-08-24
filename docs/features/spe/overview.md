# Descripción general del amplificador SPE Expert

El applet del amplificador SPE Expert supervisa y controla un amplificador lineal SPE Expert (1.3K-FA, 1.5K-FA, 2K-FA) conectado mediante serie o ser2net TCP, directamente desde el panel de applets de AetherSDR. Muestra la potencia directa en tiempo real, la ROE de la antena, la ROE del ATU, la tensión/corriente de alimentación y la temperatura del disipador en indicadores y lecturas de texto, y refleja las teclas del panel frontal del amplificador como botones.

## Antes de comenzar

- Conecte un amplificador SPE Expert compatible a su radio mediante serie o ser2net TCP y verifique que la conexión funcione en la configuración de la radio.
- Conéctese a una radio FLEX-8600. El applet requiere una conexión de radio activa.

## Cómo funciona

El applet se abre desde **Panel de applets > Mosaico SPE**. Realiza consultas al amplificador a través del enlace serie o TCP y actualiza los indicadores y las lecturas en tiempo real (el texto de las etiquetas se actualiza a 10 Hz). El applet detecta el modelo del amplificador en la primera consulta y ajusta la escala del indicador de potencia directa en consecuencia (escala predeterminada de 0–1600 W para el 1.3K-FA, el 1.5K-FA y el 2K-FA).

### Lecturas de estado

| Control | Comportamiento |
|---|---|
| **Indicador de potencia directa** | Potencia directa en tiempo real. La inercia del medidor suaviza la lectura. El pico se mantiene durante 2,5 s antes de borrarse. |
| **Indicador de ROE de antena** | ROE en tiempo real en la antena. La escala va de 1.0:1 a 3.0:1, con una marca de advertencia en 2.0:1. |
| **Indicador de ROE del ATU** | ROE en tiempo real en la entrada del ATU. La escala va de 1.0:1 a 3.0:1, con una marca de advertencia en 2.0:1. |
| **Texto TEMP / V / I** | Temperatura del disipador (en la unidad en la que esté configurada la pantalla del propio amplificador — C o F, sin conmutador C/F), tensión de alimentación y corriente de alimentación. |
| **Píldora de estado** | Muestra uno de **OPR · TX**, **OPR · RX**, **STANDBY**, o un banner de fallo debajo de las lecturas. |

### Botones de control

La fila de botones refleja las teclas del panel frontal del amplificador:

| Botón | Comportamiento |
|---|---|
| **ON** | Envía pulsos a las líneas de control serie para encender el amplificador. A través de la red, esto requiere un puerto ser2net con rfc2217 habilitado. Permanece habilitado mientras el amplificador está en silencio. |
| **OPER** | Alterna entre Standby y Operate (tecla OPERATE del panel frontal). Deshabilitado cuando el amplificador está en silencio. |
| **PWR** | Muestra el nivel de potencia actual (LOW/MID/HIGH) una vez conocido; al hacer clic, cambia al siguiente nivel, reflejando la tecla POWER del amplificador. Deshabilitado cuando el amplificador está en silencio. |
| **TUNE** | Inicia la sintonización del ATU (tecla TUNE del panel frontal). Esto activa la transmisión con excitación de RF. Deshabilitado cuando el amplificador está en silencio. |
| **OFF** | Apaga el amplificador. Use **ON** para volver a encenderlo. Deshabilitado cuando el amplificador está en silencio. |
| **INPUT** | Alterna entre el puerto de entrada 1 y 2. Deshabilitado cuando el amplificador está en silencio. |
| **ANT** | Cambia la antena de TX para la banda actual. Deshabilitado cuando el amplificador está en silencio. |
| **▼ / ▲** | Reduce/aumenta la potencia de excitación que el amplificador solicita a la radio a través de CAT (teclas de flecha del panel frontal). Deshabilitado cuando el amplificador está en silencio. |

Un **banner de fallo** aparece en rojo a lo ancho completo cuando el amplificador reporta un fallo; la píldora de estado muestra **Fault** durante este estado. Los botones que no funcionarían mientras el amplificador está en silencio se deshabilitan para evitar enviar comandos no válidos.

## Relacionado

- [Supervise la potencia directa y la ROE en el amplificador SPE Expert](monitor-forward-power-and-swr-on-the-spe-expert-amplifier.md)
- [Ponga el amplificador SPE Expert en Operate o Standby](put-the-spe-expert-amplifier-in-operate-or-standby.md)
- [Cambie el nivel de potencia del SPE Expert (Low, Mid, High)](cycle-the-spe-expert-power-level-low-mid-high.md)
- [Sintonice el amplificador SPE Expert](tune-the-spe-expert-amplifier.md)

# Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado

La insignia TX de la barra de estado le ofrece un solo clic para sacar el transmisor del estado TX, útil cuando MOX está atascado, una portadora de sintonía sigue activa, o cualquier otra condición ha dejado la radio keyed y el applet de Controles TX no está a la mano.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La insignia TX solo aparece en la barra de estado cuando hay una conexión activa con la radio.
- La radio debe estar actualmente en estado de transmisión (MOX activado o portadora de sintonía activa) para que la insignia sea accionable.

## Pasos

1. Localice la insignia TX en la barra de estado de AetherSDR en la parte inferior de la ventana principal. La insignia es visible y está iluminada cuando la radio está transmitiendo.
2. Haga clic una vez en la insignia TX.
3. Confirme que la radio ha vuelto a recepción: el indicador de Potencia RF en el applet de Controles TX baja a cero, el botón MOX vuelve a su estado apagado (azul) y la etiqueta del botón TUNE vuelve a "TUNE" si había una portadora de sintonía activa.

## Consejos

- Si el applet de Controles TX está visible, también puede hacer clic en MOX para desactivar la transmisión, o hacer clic en TUNE para detener una portadora de sintonía activa (el botón muestra "TUNING..." mientras está activa). La insignia TX de la barra de estado es la vía más rápida cuando el applet está contraído o fuera de la vista.
- Si MOX fue activado por un comando CAT o TCI externo, al hacer clic en la insignia TX se envía el mismo comando de desactivación. La fuente original del PTT no importa.

## Solución de problemas

- **Al hacer clic en la insignia TX no se detiene la transmisión** — La radio puede estar keyed por PTT de hardware (pedal o línea PTT del micrófono). Libere primero el PTT de hardware; los comandos de software no pueden anular una línea PTT de hardware mantenida activa.
- **La insignia TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en Modo Mínimo (`View > Minimal Mode`). Desactivar el Modo Mínimo restaura la barra de estado.

## Relacionado

- [Alternar MOX para keyear manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de Controles TX](overview.md)

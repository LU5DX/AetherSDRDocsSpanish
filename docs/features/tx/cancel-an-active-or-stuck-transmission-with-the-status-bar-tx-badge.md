# Cancelar una transmisión activa o bloqueada con el indicador TX de la barra de estado

El indicador TX de la barra de estado permite detener el transmisor con un solo clic — útil cuando MOX queda activo, hay una portadora de ajuste en curso, o cualquier otra condición ha dejado el equipo en transmisión y el applet TX Controls no está a la vista de inmediato.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El indicador TX solo aparece en la barra de estado cuando hay una conexión de radio activa.
- El equipo debe encontrarse en estado de transmisión (MOX activado o portadora de ajuste en curso) para que el indicador sea accionable.

## Pasos

1. Localice el indicador TX en la barra de estado de AetherSDR, en la parte inferior de la ventana principal. El indicador es visible y se ilumina cuando el equipo está transmitiendo.
2. Haga clic una vez en el indicador TX.
3. Confirme que el equipo ha vuelto a recepción: el medidor RF Pwr en el applet TX Controls cae a cero, el botón MOX regresa a su estado apagado (azul) y la etiqueta del botón TUNE vuelve a "TUNE" si había una portadora de ajuste activa.

## Consejos

- Si el applet TX Controls está visible, también puede hacer clic en MOX para desactivar la transmisión, o en TUNE para detener una portadora de ajuste activa (el botón muestra "TUNING..." mientras está en curso). El indicador TX de la barra de estado es el camino más rápido cuando el applet está contraído o fuera de la vista.
- Si MOX fue activado por un comando externo de CAT o TCI, hacer clic en el indicador TX envía el mismo comando de desactivación. El origen del PTT original no importa.

## Solución de problemas

- **Hacer clic en el indicador TX no detiene la transmisión** — Es posible que el equipo esté activado por PTT de hardware (pedal o línea PTT del micrófono). Suelte primero el PTT de hardware; los comandos de software no pueden anular una línea de PTT de hardware retenida.
- **El indicador TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en Minimal Mode (`View > Minimal Mode`). Desactivar Minimal Mode restaura la barra de estado.

## Temas relacionados

- [Activar MOX para transmitir manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de ajuste para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de TX Controls](overview.md)

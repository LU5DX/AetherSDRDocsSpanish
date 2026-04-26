# Configurar el retardo de break-in en CW

Configure cuánto tiempo espera el radio después de la última pulsación de tecla antes de volver a recepción. Un retardo mayor evita conmutaciones bruscas de RX durante el envío rápido; un retardo menor (o QSK completo) minimiza el tiempo muerto de recepción.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel de CW cuando se selecciona el modo CW; el control deslizante Delay solo es visible en ese subpanel.

## Pasos

1. Si el applet Phone/CW no está visible, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.
2. Confirme que el subpanel de CW esté mostrándose. Si ve controles de micrófono y procesador en su lugar, el slice activo no está en modo CW — cambie primero el modo del slice.
3. Localice el control deslizante **Delay** en el subpanel de CW.
4. Arrastre el control deslizante **Delay** hacia la izquierda para reducir el retardo o hacia la derecha para aumentarlo. El valor se actualiza en el radio en tiempo real.
5. Para usar break-in completo (QSK) sin retardo, haga clic en **Breakin** para activarlo. Cuando **Breakin** está activo, el radio conmuta a recepción inmediatamente después de cada elemento.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Configuración persistente |
|---|---|---|---|---|
| **Delay** | Control deslizante | — | 0–2000 ms, paso 10 | ninguna |
| **Breakin** | Botón de alternancia | — | On / Off | ninguna |

**Delay** — Establece el retardo de break-in en CW en milisegundos. A 0 ms el radio intenta volver a recepción lo más rápido posible entre elementos. A 2000 ms el radio mantiene la transmisión durante dos segundos completos después del último evento de tecla.

**Breakin** — Habilita la operación QSK completa. Cuando está activado, el radio conmuta entre transmisión y recepción dentro de cada intervalo entre elementos.

## Consejos

- Delay y Breakin funcionan en conjunto. Si **Breakin** está desactivado, el valor de **Delay** determina el tiempo de retención. Si **Breakin** está activado, el radio ignora el retardo y opera en QSK completo.
- Si el ruido de conmutación de relés o la secuenciación del amplificador son una preocupación, establezca un retardo mayor en lugar de habilitar **Breakin**.

## Relacionado

- [Configurar la velocidad de tecleo en CW en PPM](set-cw-keying-speed-in-wpm.md)
- [Habilitar el tecleo con paleta iámbica](enable-iambic-paddle-keying.md)
- [Cambiar el tono de CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Habilitar el sidetone local de baja latencia (Local STn) para trabajo rápido con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)

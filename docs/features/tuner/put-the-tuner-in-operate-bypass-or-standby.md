# Poner el sintonizador en OPERATE, BYPASS o STANDBY

Use el botón OPERATE en el applet del sintonizador para recorrer los tres estados de relé del 4O3A Tuner Genius XL: OPERATE, BYPASS y STANDBY.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet del sintonizador está oculto hasta que se detecte un Tuner Genius XL.
- El botón TUN en la bandeja debe estar disponible en la barra lateral derecha, lo que indica que se ha detectado el TGXL.

## Pasos

1. Haga clic en el botón TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Localice el botón OPERATE en el área inferior derecha del applet.
3. Haga clic en OPERATE para avanzar al siguiente estado. Cada clic avanza un paso:
   - OPERATE → BYPASS
   - BYPASS → STANDBY
   - STANDBY → OPERATE

## Qué hace cada control

| Botón | Color cuando está activo | Significado |
|---|---|---|
| OPERATE | Verde | Los relés del sintonizador están en el circuito y activos. |
| BYPASS | Naranja | El sintonizador está energizado pero la red de adaptación está puenteada. |
| STANDBY | Predeterminado (depende del tema) | El sintonizador no está operando. |

La etiqueta y el color del botón se actualizan inmediatamente cuando el TGXL confirma el cambio de estado.

## Consejos

- El botón siempre muestra el estado **actual**, no el siguiente. Una etiqueta verde OPERATE significa que el sintonizador ya está en OPERATE.
- Al hacer clic una vez desde STANDBY, el sintonizador vuelve a OPERATE y restablece el color verde. No es necesario pasar por BYPASS para regresar a OPERATE.

## Solución de problemas

- **El botón TUN en la bandeja no es visible** — El applet del sintonizador está oculto hasta que se detecte un Tuner Genius XL en la red. Verifique que el TGXL esté encendido y conectado. Consulte [Descripción general del sintonizador](overview.md).
- **La etiqueta del botón no cambia después de hacer clic** — La etiqueta se actualiza solo cuando el TGXL confirma el nuevo estado. Si la etiqueta permanece igual, verifique la conexión entre AetherSDR y el TGXL.

## Relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)

---

# Monitorizar la potencia directa y la ROE en el applet del sintonizador

El applet del sintonizador muestra medidores de potencia directa y ROE reportados por el 4O3A Tuner Genius XL.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio y el TGXL debe estar detectado en la red.

## Pasos

1. Haga clic en el botón TUN en la barra lateral derecha para abrir el applet del sintonizador.
2. Localice el medidor **Fwd Pwr** en la parte superior del applet. Muestra la potencia directa en vatios.
3. Localice el medidor **SWR** debajo de él. Muestra la relación de ROE.

## Escala de los medidores

La escala del medidor de potencia directa depende de la configuración de su hardware:

| Configuración | Rango de escala |
|---|---|
| Solo equipo base (sin amplificador) | 0–200 W |
| Amplificador Aurora | 0–600 W |
| Amplificador PGXL | 0–2000 W |

El medidor de ROE varía de 1.0 a 3.0. Los valores superiores a 2.5 se muestran en rojo para indicar una condición de ROE alta.

## Cambios importantes en el comportamiento en v26.6.3

- **El medidor de ROE ahora se restablece a 1.0 cuando la potencia directa es inferior a 5 W.** El TGXL reporta una ROE de 99.9 en reposo cuando no hay una señal incidente presente. Para evitar que esto desborde el medidor, la barra de ROE se restablece a 1.0 cada vez que la potencia directa cae por debajo de 5 W. Esto coincide con el umbral utilizado para la visualización de la etiqueta de ROE.
- **Nombres accesibles añadidos** para compatibilidad con lectores de pantalla: "Forward power", "SWR", "Tuner capacitor C1", "Tuner inductor L", "Tuner capacitor C2".

## Solución de problemas

- **El medidor de ROE muestra 1.0 incluso al transmitir** — Verifique que la potencia directa supere los 5 W. El medidor de ROE solo muestra el valor medido cuando la potencia directa es de al menos 5 W.

## Relacionados

- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](#)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)

---

# Ejecutar un autoajuste en el TGXL externo

Use el botón TUNE en el applet del sintonizador para iniciar un ciclo de ajuste automático en el 4O3A Tuner Genius XL.

## Antes de comenzar

- El applet del sintonizador debe estar abierto. El TGXL debe estar detectado en la red.
- Asegúrese de que su radio esté transmitiendo a un nivel de potencia adecuado para el ajuste (normalmente 5–100 W).

## Pasos

1. Haga clic en el botón **TUNE** en el applet del sintonizador.
2. La etiqueta del botón cambia a **TUNING...** y se vuelve roja mientras el ciclo de ajuste está en progreso.
3. Cuando el ajuste se completa, la etiqueta del botón parpadea mostrando **SWR x.xx** durante aproximadamente 2.5 segundos, indicando la ROE posterior al ajuste.
4. Después del parpadeo, el botón vuelve a su etiqueta **TUNE** predeterminada.

## Comportamiento de la conexión directa (v0.9.2.1 y posteriores)

Cuando se configura una conexión directa al TGXL (puerto 9010) en Configuración de Radio → Sintonizador, el comando de autoajuste se envía directamente al TGXL, omitiendo la ruta del firmware de la radio. Esto resuelve problemas de ajuste que algunos usuarios experimentaron con el firmware FlexRadio 4.2.

Cuando no se configura una conexión directa, el comando de autoajuste se enruta a través de la ruta del firmware de la radio.

Configure la conexión directa en **Configuración de Radio → Sintonizador**.

## Consejos

- El botón TUNE no responderá si el sintonizador está en modo BYPASS o STANDBY. Configure el sintonizador en OPERATE primero.
- El parpadeo de la ROE posterior al ajuste le permite leer la ROE final inmediatamente después del ajuste sin tener que mirar un medidor separado.

## Solución de problemas

- **El botón TUNE permanece rojo y no vuelve a TUNE** — El ciclo de ajuste puede haber sido interrumpido. Haga clic en TUNE nuevamente o verifique la conexión con el TGXL.
- **TUNE está atenuado o no responde** — Verifique que el sintonizador esté en modo OPERATE y que el TGXL esté detectado.

## Relacionados

- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](#)

---

# Ajustar finamente los relés C1/L/C2 con la rueda del ratón

Ajuste las posiciones individuales de los bancos de relés en el 4O3A Tuner Genius XL usando la rueda del ratón sobre las barras de relés C1, L y C2.

## Antes de comenzar

- Una conexión directa al TGXL (puerto 9010) debe estar activa. Las barras de relés solo se pueden ajustar cuando AetherSDR tiene una conexión directa al TGXL.
- El applet del sintonizador debe estar abierto.

## Pasos

1. Coloque el cursor del ratón sobre la barra de relé **C1**, **L** o **C2** en el applet del sintonizador.
2. Desplace la rueda del ratón hacia arriba para aumentar la posición del relé, o hacia abajo para disminuirla.
3. La barra de relé se actualiza inmediatamente para mostrar la nueva posición.

## Rangos de los relés

| Relé | Rango | Descripción |
|---|---|---|
| C1 | 0–255 | Banco de condensadores 1 |
| L | 0–255 | Banco de inductancias |
| C2 | 0–255 | Banco de condensadores 2 |

## Cuándo el desplazamiento está deshabilitado

El desplazamiento con la rueda del ratón solo está habilitado cuando hay una conexión directa al TGXL activa. Si está utilizando la ruta del firmware de la radio para comunicarse con el sintonizador, las barras de relés muestran los valores actuales pero no se pueden ajustar con la rueda del ratón.

## Consejos

- El ajuste fino de los relés es útil para optimizar una adaptación después de un autoajuste, o para ajustar manualmente el sintonizador a una impedancia específica.
- Los valores de los relés se envían inmediatamente al TGXL en cada evento de desplazamiento.

## Relacionados

- [Descripción general del sintonizador](overview.md)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)

---

# Descripción general del sintonizador

El applet del sintonizador proporciona control y monitorización para el sintonizador de antena externo 4O3A Tuner Genius XL.

## Requisitos previos

- Debe haber un 4O3A Tuner Genius XL presente en su red.
- El TGXL debe ser detectado por AetherSDR automáticamente o configurado manualmente.

## Acceso al applet del sintonizador

Haga clic en el botón **TUN** en la barra lateral derecha para abrir o cerrar el applet del sintonizador. El applet está oculto hasta que se detecte un TGXL.

## Diseño del applet

El applet del sintonizador contiene:

- **Medidor de potencia directa** (Fwd Pwr) — muestra la potencia directa en vatios
- **Medidor de ROE** (SWR) — muestra la relación de ROE (1.0–3.0)
- **Barras de relés** (C1, L, C2) — muestran las posiciones actuales de los bancos de relés
- **Botón TUNE** — inicia un ciclo de autoajuste
- **Botón OPERATE/BYPASS/STANDBY** — recorre los modos del sintonizador
- **Botones ANT 1/2/3** — selección del puerto de antena (solo visibles cuando la conexión directa al TGXL está activa)

## Conexiones de red

El Tuner Genius XL puede conectarse a AetherSDR a través de dos rutas:

1. **Ruta del firmware de la radio** — El TGXL se comunica a través de la conexión de red del FlexRadio. Esta es la opción predeterminada.
2. **Conexión directa (puerto 9010)** — AetherSDR se conecta directamente al TGXL. Esto habilita:
   - Ajuste con la rueda del ratón de los relés C1/L/C2
   - Selección del conmutador de antena ANT 1/2/3
   - Omisión de la ruta del firmware de la radio para comandos de autoajuste

Configure la conexión en **Configuración de Radio → Sintonizador**.

## Páginas relacionadas

- [Poner el sintonizador en OPERATE, BYPASS o STANDBY](#)
- [Monitorizar la potencia directa y la ROE en el applet del sintonizador](#)
- [Ejecutar un autoajuste en el TGXL externo](run-an-autotune-on-the-external-tgxl.md)
- [Leer la ROE inmediatamente después de un ajuste](read-swr-immediately-after-a-tune.md)
- [Ajustar finamente los relés C1/L/C2 con la rueda del ratón](fine-tune-the-c1-l-c2-relays-with-the-mousewheel.md)

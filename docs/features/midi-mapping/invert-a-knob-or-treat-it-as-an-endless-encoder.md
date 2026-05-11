# Invertir un potenciómetro o tratarlo como un codificador sin fin

Después de crear una vinculación MIDI, puede invertir su dirección con Invertir o indicarle a AetherSDR que trate el control como un codificador sin fin con Relativo. Ambas opciones se configuran por vinculación en la tabla de Vinculaciones.

## Antes de comenzar

- Debe haber un controlador MIDI conectado y al menos una vinculación existente. Consulte [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md) y [Grabar una nueva vinculación con modo Aprendizaje](record-a-new-binding-with-learn-mode.md).
- Abra `Settings > MIDI Mapping...` para acceder al cuadro de diálogo de Mapeo de controladores MIDI.

## Pasos

1. Abra `Settings > MIDI Mapping...`.
2. Localice la vinculación que desea cambiar en la tabla de Vinculaciones.
3. Para invertir la dirección del control, marque la casilla Invertir en la fila de esa vinculación.
4. Para tratar el control como un codificador sin fin, marque la casilla Relativo en la fila de esa vinculación.
5. Cualquiera de las casillas puede marcarse o desmarcarse de forma independiente. Los cambios surten efecto de inmediato.
6. Haga clic en Cerrar cuando haya terminado.

## Función de cada control

| Control  | Columna en la tabla de Vinculaciones | Comportamiento                                                                                                                                    |
|----------|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| Invertir | Invertir                             | Invierte la dirección del control para esa vinculación. Girar en sentido horario disminuye, en sentido antihorario aumenta, o viceversa.          |
| Relativo | Relativo                             | Trata el control como un codificador sin fin. Utilícelo cuando su potenciómetro de hardware envíe valores incrementales (relativos) en lugar de posiciones absolutas (0–127). |

## Filtro de categoría

El cuadro combinado Categoría sobre la tabla de Vinculaciones filtra el cuadro combinado Parámetro a una categoría de control específica. En v26.5.1, las categorías disponibles son:

- All (Todas)
- RX
- TX
- Phone/CW (Teléfono/CW)
- EQ
- Global (Global)
- Mode (Modo)
- Band (Banda)
- Filter (Filtro)
- Slice (Rebanada)
- Display (Pantalla)
- Frequency (Frecuencia)

Seleccione una categoría para reducir la lista de parámetros mostrados al crear una nueva vinculación.

## Consejos

- Use Relativo cuando su potenciómetro envíe valores pequeños de incremento/decremento en lugar de una posición absoluta. Si un potenciómetro salta erráticamente al girarlo, activar Relativo suele corregirlo.
- Invertir y Relativo pueden combinarse en la misma vinculación. Por ejemplo, un codificador Relativo que incrementa en la dirección incorrecta puede tener ambas opciones marcadas.
- Los cambios en Invertir y Relativo se guardan automáticamente al guardar un perfil. Use Guardar en Perfil: para preservarlos.

## Solución de problemas

- **Marcar Relativo hace que un potenciómetro deje de responder** — El potenciómetro puede estar enviando valores absolutos (0–127). Desmarque Relativo y deje la vinculación en modo absoluto.
- **El control aún se mueve en la dirección incorrecta después de marcar Invertir** — Confirme que marcó Invertir en la fila correcta. Cada fila de vinculación tiene su propia casilla Invertir; desplácese horizontalmente si la columna no es visible.

## Relacionado

- [Grabar una nueva vinculación con modo Aprendizaje](record-a-new-binding-with-learn-mode.md)
- [Eliminar una vinculación](delete-a-binding.md)
- [Guardar el mapeo actual como un perfil con nombre](save-the-current-mapping-as-a-named-profile.md)
- [Conectar un controlador MIDI](../../getting-started/setup/connect-a-midi-controller.md)

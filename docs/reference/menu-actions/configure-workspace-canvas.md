# Configurar el lienzo del espacio de trabajo

Active o desactive el lienzo del espacio de trabajo para mover panadápters y applets a ventanas de colocación libre, y recupere diseños con nombre mediante el conmutador Workspaces. El lienzo está desactivado por defecto y es opcional.

## Antes de comenzar

- AetherSDR v26.8.4 o posterior (lienzo del espacio de trabajo multiventana, fase 7).

## Pasos

1. Abra **View > Workspace Canvas**.
2. Haga clic en **Enabled** para activar el lienzo del espacio de trabajo. AetherSDR migra el diseño actual a un espacio de trabajo llamado "Classic".
3. (Opcional) Haga clic en **Edit Layout** para armar la colocación de panadápters y applets.
4. (Opcional) Use el conmutador **Workspaces** para recuperar diseños con nombre.
5. (Opcional) Abra el submenú **Canvas Windows** para enumerar ventanas adicionales del lienzo del espacio de trabajo.
6. Para volver al shell normal, abra **View > Workspace Canvas** y haga clic en **Enabled** nuevamente para desmarcar la casilla.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Enabled** | Marcable. Activa o desactiva el shell del lienzo del espacio de trabajo (desactivado por defecto). Al activarlo, migra el diseño actual a un espacio de trabajo "Classic"; al desactivarlo, restaura el shell normal. |
| **Edit Layout** | Marcable. Arma la colocación de panadápters y applets. |
| **Workspaces** | Conmutador que recupera diseños con nombre. |
| **Canvas Windows** | Submenú que enumera ventanas adicionales del lienzo del espacio de trabajo. |

## Consejos

- Active **Edit Layout** antes de intentar mover panadápters o applets; sin él, la colocación no está armada.

## Relacionados

- [Comprensión del panel de applets de AetherSDR](../../getting-started/concepts/understanding-applets.md)
- [Habilitar el modo minimalista](enable-minimal-mode.md)
- [Habilitar ventana sin marco](enable-frameless-window.md)

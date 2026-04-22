# Documentación de usuario de AetherSDR (Español)

Documentación para usuarios de [AetherSDR](https://github.com/ten9876/AetherSDR),
un cliente nativo Linux escrito en Qt6 compatible con SmartSDR para radios
FlexRadio FLEX-8600.

## Estructura

```
/
├── getting-started/   Instalación, primera conexión, primer QSO, conceptos
├── features/          Una carpeta por función (applet, diálogo, panel) con
│                      página de descripción general y páginas de tareas
├── operating/         Guías de operación (modos digitales, operación remota)
├── reference/         Referencia de menús, claves de configuración
└── troubleshooting/   Problemas comunes y soluciones
```

## Nota sobre la interfaz

La interfaz de AetherSDR está en inglés. Estos documentos mantienen los
nombres de botones, menús y diálogos en inglés tal como aparecen en la
aplicación, y traducen únicamente el texto explicativo al español.

Por ejemplo: "Para activar TCI, haga clic en el botón **Enable** del applet
TCI" — "Enable" queda en inglés porque así aparece en la pantalla.

## Generación

Estos archivos se generan automáticamente a partir de la versión en inglés
mediante el pipeline en el repositorio
[AetherSDRDocsEnglish](../AetherSDRDocsEnglish). Para regenerarlos:

```bash
cd ../AetherSDRDocsEnglish/_generator
python translate_docs.py
```

No edite estos archivos a mano — los cambios se sobreescribirán en la
siguiente regeneración. Para cambios permanentes, modifique la versión en
inglés y vuelva a ejecutar el traductor.

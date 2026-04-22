# Documentación de usuario de AetherSDR (Español)

Fuente del manual de usuario en
**https://lu5dx.github.io/AetherSDRDocsSpanish/** (cuando se habilite Pages).

Construido con [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).
Espejo en inglés: [AetherSDRDocsEnglish](https://github.com/LU5DX/AetherSDRDocsEnglish).

## Nota sobre la interfaz

La interfaz de AetherSDR está en inglés. Estos documentos mantienen los
nombres de botones, menús y diálogos en inglés tal como aparecen en la
aplicación, y traducen únicamente el texto explicativo al español.

Por ejemplo: "Para activar TCI, haga clic en el botón **Enable** del applet
TCI" — "Enable" queda en inglés porque así aparece en la pantalla.

## Estructura

```
/
├── mkdocs.yml              Configuración de MkDocs Material
├── overrides/              Plantilla personalizada de inicio
├── docs/                   Árbol de documentación (servido por MkDocs)
│   ├── index.md            Página de inicio (usa overrides/home.html)
│   ├── stylesheets/        CSS personalizado (hero con paralaje)
│   ├── javascripts/        Paralaje en scroll
│   ├── assets/             Arte del hero (SVG provisionales)
│   ├── getting-started/    Instalación, primera conexión, primer QSO
│   ├── features/           Una carpeta por applet/diálogo/panel
│   ├── operating/          Guías de operación transversales
│   ├── reference/          Referencia de menús y ajustes
│   └── troubleshooting/    Problemas comunes y soluciones
└── .github/workflows/      Workflow de despliegue a GitHub Pages
```

## Vista previa local

```bash
pip install mkdocs-material
mkdocs serve     # http://127.0.0.1:8000
```

## Generación

Estos archivos se traducen automáticamente desde el repositorio en inglés
mediante el pipeline en
[AetherSDRDocsEnglish/_generator/translate_docs.py](https://github.com/LU5DX/AetherSDRDocsEnglish/blob/main/_generator/translate_docs.py).
No edite estos archivos a mano — los cambios se sobreescribirán en la
siguiente regeneración. Para cambios permanentes, modifique la versión en
inglés y vuelva a ejecutar el traductor.

## Hospedaje

El workflow incluido publica en GitHub Pages en cada push a `main`.
**Nota:** GitHub Pages en repositorios privados requiere GitHub Pro o
superior. En el plan gratuito, haga el repo público o cambie el job de
despliegue por Cloudflare Pages / Netlify / Vercel.

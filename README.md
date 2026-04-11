# 🗂️ Portafolio Comercial — Pablo Vesga

Repositorio público para compartir **propuestas, presentaciones y hoja de vida** con clientes y socios estratégicos.

Todas las páginas están disponibles como HTML interactivo a través de **GitHub Pages**.

## 📁 Estructura

```
comercial/
├── index.html               ← Landing page principal
├── hoja-de-vida/
│   └── index.html           ← Hoja de vida interactiva (se actualiza automáticamente)
├── propuestas/
│   ├── index.html           ← Listado de propuestas activas
│   ├── template/            ← Plantilla base para nuevas propuestas
│   └── <nombre-cliente>/    ← Una carpeta por propuesta
│       ├── index.html       ← Propuesta en HTML
│       └── meta.json        ← Metadata: título, cliente, fecha, estado
├── presentaciones/
│   ├── index.html           ← Listado de presentaciones
│   └── template/            ← Plantilla base para nuevas presentaciones
└── .github/workflows/
    └── sync-propuestas.yml  ← Actualiza la HV cuando se agrega una propuesta
```

## 🔄 Flujo de trabajo

1. **Nueva propuesta:** Copia `propuestas/template/` a `propuestas/<cliente>/`, edita el HTML y el `meta.json`.
2. **Push a `main`:** El workflow de GitHub Actions detecta el cambio y actualiza automáticamente la sección de propuestas en la hoja de vida.
3. **Compartir:** Envía el link `https://pablovesga.github.io/comercial/propuestas/<cliente>/` al cliente.

## 🚀 GitHub Pages

Activado en la rama `main`, carpeta raíz.  
URL base: **https://pablovesga.github.io/comercial/**

| Sección | URL |
|---|---|
| Inicio | `/` |
| Hoja de vida | `/hoja-de-vida/` |
| Propuestas | `/propuestas/` |
| Presentaciones | `/presentaciones/` |

## 🔗 Otros repositorios

Los proyectos pueden enviar sus propuestas y presentaciones a este repositorio mediante GitHub Actions configuradas en sus propios repos. Ver workflow `sync-propuestas.yml` como referencia.

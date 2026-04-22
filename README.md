# Portafolio Comercial — Juan Pablo Vesga Rosas

Repositorio público para compartir **propuestas, presentaciones y hoja de vida** con clientes y socios.

URL base: **https://pablovesga.github.io/comercial/**

---

## Estructura

```
comercial/
├── index.html               ← Landing page principal
├── hoja-de-vida/
│   └── index.html           ← Hoja de vida interactiva (se actualiza automáticamente)
├── propuestas/
│   ├── index.html           ← Listado de propuestas activas
│   ├── index.json           ← Índice generado automáticamente (no editar)
│   ├── template/            ← Plantilla base — no borrar
│   └── <nombre-cliente>/    ← Una carpeta por propuesta
│       ├── index.html       ← Propuesta en HTML
│       └── meta.json        ← Metadata: título, cliente, fecha, estado
├── presentaciones/
│   └── index.html           ← Listado de presentaciones
└── .github/workflows/
    ├── sync-propuestas.yml  ← Auto-actualiza el índice y la HV al detectar cambios
    └── recibir-propuesta.yml ← Recibe propuestas desde otros repos vía GitHub Actions
```

---

## Cómo agregar o actualizar contenido

### Opción A — Desde GitHub (sin clonar el repo)

Esta es la forma más fácil si no tienes el repo en tu computador.

**Agregar una nueva propuesta:**

1. Ve a `propuestas/template/` en GitHub
2. Copia los dos archivos (`index.html` y `meta.json`) a una nueva carpeta llamada `propuestas/nombre-cliente/`
3. Edita `meta.json` con los datos reales:

```json
{
  "slug": "nombre-cliente-2026",
  "titulo": "Nombre del proyecto",
  "cliente": "Nombre del cliente",
  "fecha": "2026-04-21",
  "estado": "activa",
  "descripcion": "Descripción breve que aparece en el listado"
}
```

Estados válidos: `activa` · `enviada` · `ganada` · `cerrada`

4. Edita `index.html` con el contenido de la propuesta
5. Haz commit en `main` → el workflow se encarga de todo lo demás automáticamente

**Actualizar una propuesta existente:**

1. Ve a `propuestas/nombre-cliente/` en GitHub
2. Edita `index.html` o `meta.json` directamente
3. Haz commit → el índice y la hoja de vida se actualizan solos

---

### Opción B — Desde tu computador (flujo completo)

```bash
# 1. Clonar (solo la primera vez)
git clone https://github.com/pablovesga/comercial.git
cd comercial

# 2. Copiar plantilla
cp -r propuestas/template propuestas/nombre-cliente

# 3. Editar los archivos
# - propuestas/nombre-cliente/meta.json  → metadata
# - propuestas/nombre-cliente/index.html → contenido

# 4. Subir cambios
git add propuestas/nombre-cliente/
git commit -m "feat: propuesta nombre-cliente"
git push
```

El workflow detecta el cambio y actualiza `propuestas/index.json` y `hoja-de-vida/index.html` automáticamente en ~30 segundos.

---

### Opción C — Desde otro repositorio (automatizado)

Otros repos pueden enviar propuestas usando el `_kit-comercial`. Ver `_kit-comercial/README.md`.

---

## Agregar una presentación

1. Crea la presentación como HTML en `presentaciones/nombre-presentacion/index.html`
2. Crea `presentaciones/nombre-presentacion/meta.json`:

```json
{
  "slug": "nombre-presentacion",
  "titulo": "Título de la presentación",
  "fecha": "2026-04-21",
  "descripcion": "Descripción breve"
}
```

3. Haz push → aparece automáticamente en el listado

---

## Flujo automático (qué hace GitHub Actions)

```
Tu push a main
    ↓
sync-propuestas.yml detecta cambios en propuestas/**/meta.json o index.html
    ↓
Genera propuestas/index.json con todas las propuestas ordenadas
    ↓
Inyecta las propuestas en hoja-de-vida/index.html
    ↓
Hace commit automático "[skip ci]" → GitHub Pages publica en ~1 min
```

---

## Disparar el sync manualmente

Si algo no se actualizó, puedes forzar el sync:

1. Ve a **Actions** en GitHub
2. Selecciona "Sincronizar Propuestas → Hoja de Vida"
3. Clic en "Run workflow" → "Run workflow"

---

## URLs

| Sección | URL |
|---|---|
| Inicio | `https://pablovesga.github.io/comercial/` |
| Hoja de vida | `https://pablovesga.github.io/comercial/hoja-de-vida/` |
| Propuestas | `https://pablovesga.github.io/comercial/propuestas/` |
| Presentaciones | `https://pablovesga.github.io/comercial/presentaciones/` |
| Una propuesta | `https://pablovesga.github.io/comercial/propuestas/nombre-cliente/` |

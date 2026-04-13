# Kit Comercial — Enviar Propuesta a pablovesga/comercial

Este kit permite que cualquier repositorio de Pablo Vesga publique automáticamente
una propuesta o presentación en el portafolio comercial en GitHub Pages.

## Requisitos

1. Tener un **Personal Access Token (PAT)** con scope `repo` guardado como secret
   en tu repositorio con el nombre `COMERCIAL_TOKEN`.
   
   > Crearlo en: GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens
   > Permisos necesarios: `Contents: write` en el repo `pablovesga/comercial`

2. Copiar el archivo `enviar-propuesta.yml` a `.github/workflows/` de tu repositorio.

## Uso

### Opción A: Manualmente desde GitHub UI

1. Ve a tu repo → Actions → "Enviar Propuesta a Portafolio Comercial"
2. Click en "Run workflow"
3. Llena los campos: slug, título, cliente, estado, descripción

### Opción B: Desde otro workflow (automático)

```yaml
- name: Publicar propuesta en portafolio
  uses: peter-evans/repository-dispatch@v3
  with:
    token: ${{ secrets.COMERCIAL_TOKEN }}
    repository: pablovesga/comercial
    event-type: nueva-propuesta
    client-payload: |
      {
        "slug": "cliente-proyecto-2026",
        "titulo": "Mi Propuesta",
        "cliente": "Nombre Cliente",
        "fecha": "2026-04-11",
        "estado": "activa",
        "descripcion": "Descripción breve para el listado."
      }
```

### Opción C: Enviar con HTML personalizado

Si tu repo tiene una propuesta en HTML, agrega el campo `html_url` en el payload:

```yaml
client-payload: |
  {
    "slug": "mi-propuesta",
    "titulo": "Propuesta Visual",
    "cliente": "Cliente S.A.S",
    "html_url": "https://pablovesga.github.io/mi-repo/propuesta/",
    ...
  }
```
La propuesta en el portafolio mostrará tu HTML embebido en un iframe.

## Estados válidos

| Estado | Significado |
|---|---|
| `activa` | En preparación, no enviada aún |
| `enviada` | Enviada al cliente, esperando respuesta |
| `ganada` | Cliente aprobó el proyecto |
| `cerrada` | No avanzó |

## Resultado

Después de correr el workflow:
- La propuesta aparece en: `https://pablovesga.github.io/comercial/propuestas/<slug>/`
- El índice se actualiza automáticamente
- La hoja de vida se actualiza con la nueva propuesta

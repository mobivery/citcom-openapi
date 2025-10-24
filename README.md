# Citcom Peritaje API Documentation

Documentación interactiva de las APIs del sistema Citcom Peritaje utilizando Swagger UI.

## 📚 APIs Disponibles

Este proyecto incluye la documentación de 3 APIs:

1. **App API** (`openapi.yml`) - API REST para la aplicación móvil de ciudadanos
2. **CMS API** (`openapi-cms.yml`) - API REST para el sistema de gestión de contenidos
3. **AI Service API** (`openapi-ai-docs.yml`) - Servicio externo de generación de informes con IA

## 🚀 Despliegue en GitHub Pages

### Opción 1: Configuración Automática (Recomendada)

1. Sube los archivos del directorio `/docs` a tu repositorio en GitHub
2. Ve a la configuración del repositorio: **Settings → Pages**
3. En **Source**, selecciona:
   - Branch: `main` (o tu rama principal)
   - Folder: `/docs`
4. Haz clic en **Save**
5. GitHub Pages generará automáticamente una URL pública

Tu documentación estará disponible en:
```
https://mobivery.github.io/citcom-openapi/
```

### Opción 2: Usando GitHub Actions

Si prefieres automatizar el despliegue, puedes crear un workflow de GitHub Actions.

Crea el archivo `.github/workflows/deploy-docs.yml`:

```yaml
name: Deploy API Documentation

on:
  push:
    branches:
      - main
    paths:
      - 'docs/**'
      - 'api/**'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Copy API specs to docs
        run: |
          cp api/*.yml docs/

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
```

## 🧪 Prueba Local

Para probar la documentación localmente:

1. Instala un servidor HTTP simple:
   ```bash
   # Con Python 3
   python3 -m http.server 8000 --directory docs

   # O con Node.js (npx)
   npx http-server docs -p 8000
   ```

2. Abre tu navegador en: `http://localhost:8000`

## 📁 Estructura de Archivos

```
docs/
├── index.html              # Página principal con Swagger UI
├── openapi.yml            # Especificación App API
├── openapi-cms.yml        # Especificación CMS API
├── openapi-ai-docs.yml    # Especificación AI Service API
└── README.md              # Este archivo
```

## 🔄 Actualización de las APIs

Cuando actualices las especificaciones OpenAPI en `/api`:

1. Copia los archivos actualizados a `/docs`:
   ```bash
   cp api/*.yml docs/
   ```

2. Haz commit y push:
   ```bash
   git add docs/
   git commit -m "docs: update API specifications"
   git push
   ```

3. GitHub Pages se actualizará automáticamente (puede tardar unos minutos)

## 🎨 Personalización

Para personalizar la apariencia de Swagger UI, edita el archivo `docs/index.html`:

- **Colores**: Modifica el gradiente en la sección `.header`
- **Logo**: Agrega tu logo en el header
- **Tema**: Cambia el tema de sintaxis en `syntaxHighlight.theme`

## 🔗 Enlaces Útiles

- [Swagger UI Documentation](https://swagger.io/tools/swagger-ui/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [OpenAPI Specification](https://spec.openapis.org/oas/v3.0.3)

## 📝 Notas

- Esta solución es completamente estática y gratuita
- No requiere servidor backend
- Los archivos se sirven directamente desde GitHub Pages
- Compatible con todos los navegadores modernos

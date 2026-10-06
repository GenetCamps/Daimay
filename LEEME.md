# DaiPuntos en GitHub — Paquete B: GitHub Action

Subes **solo el Excel** a GitHub (desde el navegador) y la Action regenera y publica el marcador sola. No necesitas instalar nada en tu PC.

## Qué hay aquí
| Archivo | Para qué |
|---|---|
| `Excel/DaiPuntos_Evaluacion.xlsx` | Fuente de verdad. Es lo único que reemplazas. |
| `index.html` | El marcador (lee `data.json`). |
| `scripts/build_data.py` | Convierte el Excel en `data.json`. |
| `.github/workflows/publicar.yml` | La Action: se dispara al cambiar el Excel y publica en Pages. |
| `config.json` | Opciones (`base_url`, `incluir_nomina`, `etiqueta`). |

## Instalación (una sola vez)
1. Crea un repo en github.com/new (ej. `daipuntos`).
2. Sube TODO el contenido de esta carpeta, incluida `.github` (la web a veces omite carpetas ocultas; lo más seguro es **GitHub Desktop** o estos comandos):
   ```
   git init -b main
   git add .
   git commit -m "inicio"
   git remote add origin https://github.com/TU_USUARIO/daipuntos.git
   git push -u origin main
   ```
3. En GitHub: **Settings → Pages → Build and deployment → Source: GitHub Actions.**
4. Pestaña **Actions** → "Publicar marcador DaiPuntos" → *Run workflow* (la primera vez). Link: `https://TU_USUARIO.github.io/daipuntos/`.

## Cada actualización
1. Guarda tu Excel en Excel (Ctrl+G, para que queden los totales calculados).
2. En GitHub: carpeta `Excel` → **Add file → Upload files** → arrastra tu `DaiPuntos_Evaluacion.xlsx` (con el **mismo nombre**) → *Commit changes*.
3. La Action corre sola (1–2 min, pestaña Actions). Si falla con "filas sin valor calculado", guarda el Excel en Excel y súbelo de nuevo.

## Variante 100 % automática (opcional)
Un flujo de Power Automate que copie el Excel de SharePoint a `Excel/` del repo cada día (acción *HTTP* con la API de GitHub, o conector de GitHub). Con eso ya no subes nada a mano.

## Link al archivo de cada Kaizen
Pon en `config.json` → `"base_url"` la URL de la carpeta de SharePoint con los archivos; cada Kaizen mostrará "Abrir archivo". Si no abre por ruta, queda "Copiar nombre".

## Antes de publicar
- **El Excel completo vive en el repo.** Si el repo es público, cualquiera ve toda la evaluación (incluidas las notas internas de la columna *Revisar*). Los repos privados con Pages requieren plan de pago (Team/Enterprise). Si no lo tienes, usa el Paquete A, que sube solo `data.json`, o quita antes las notas internas.
- **Nóminas:** `"incluir_nomina": false` las quita de la página.
- **Validaciones y meta:** se guardan solo en el navegador de cada persona.

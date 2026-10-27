# skill-find-jobs-apify

Skill de Claude Code para buscar empleos en LinkedIn, Indeed, Glassdoor, Computrabajo y 20+ portales usando [Apify](https://apify.com). Junta las ofertas, saca duplicados y ofertas fantasma, y las rankea contra tu CV.

La skill es `apify-jobs-data` de [apify/awesome-skills](https://github.com/apify/awesome-skills) y está en [.claude/skills/apify-jobs-data](.claude/skills/apify-jobs-data). Como vive dentro del repo, Claude Code la carga sola cuando abrís esta carpeta.

## Requisitos

- [Claude Code](https://claude.com/claude-code) (CLI, app de escritorio o extensión de VS Code)
- Una cuenta de Apify (el plan gratis alcanza para probar: cada corrida cuesta centavos)

## 1. Clonar el repo

```bash
git clone https://github.com/ValenCMz/skill-find-jobs-apify.git
```

## 2. Sacar tu token de Apify

1. Creá una cuenta en https://console.apify.com/sign-up
2. Andá a **Settings → API & Integrations**: https://console.apify.com/settings/integrations
3. Copiá el **Personal API token** (empieza con `apify_api_...`)

> El token es como una contraseña: no lo subas al repo ni lo compartas. Las corridas se cobran a tu cuenta.

## 3. Configurar el token

El repo trae un [.mcp.json](.mcp.json) que conecta Claude Code con el servidor MCP de Apify y lee el token de la variable de entorno `APIFY_TOKEN`. Solo tenés que definirla.

**macOS / Linux (zsh):** agregalo a tu `~/.zshrc` (o `~/.bashrc` si usás bash):

```bash
echo 'export APIFY_TOKEN="apify_api_TU_TOKEN"' >> ~/.zshrc
```

Después abrí una terminal nueva (o corré `source ~/.zshrc`).

**Windows (PowerShell):**

```powershell
setx APIFY_TOKEN "apify_api_TU_TOKEN"
```

Cerrá y volvé a abrir la terminal.

Para chequear que quedó:

```bash
echo $APIFY_TOKEN
```

> Si usás la app de escritorio de Claude, cerrala del todo y volvé a abrirla después de setear la variable, para que la tome.

## 4. Abrir Claude Code en la carpeta

```bash
cd skill-find-jobs-apify
claude
```

La primera vez te va a preguntar si confiás en el servidor MCP `apify` del proyecto: aceptá. Para verificar que está conectado, escribí `/mcp` y fijate que `apify` figure como conectado.

## 5. Usarlo

Poné tu CV en la carpeta como `cv.md` (o PDF) y pedile a Claude algo como:

```
Buscame ofertas de full stack developer remoto en Argentina y España de las últimas 2 semanas
y rankealas contra mi cv.md
```

Otros ejemplos:

- `¿Qué skills piden más para backend engineer en Buenos Aires?`
- `Rango salarial de data engineer remoto en España`
- `Exportame a CSV las ofertas de React en LinkedIn de la última semana`

Antes de correr, Claude te muestra los parámetros (rol, ubicación, portales, cantidad) y una estimación de costo. Arrancá con pocos resultados (10–15 por portal) y escalá si hace falta.

## Tus datos quedan locales

El [.gitignore](.gitignore) excluye `cv.md`, los PDF, los `empleos-resultados-*.md` y la carpeta `jobs/`, así que tu CV y tus resultados no se suben si hacés commit.

## Problemas comunes

- **`apify` no aparece en `/mcp` o falla la conexión:** la variable `APIFY_TOKEN` no está seteada en la terminal desde donde abriste `claude`. Revisá el paso 3 y abrí una terminal nueva.
- **Error 401 / unauthorized:** el token está mal copiado o lo regeneraste. Volvé a copiarlo de la consola de Apify.
- **Claude no usa la skill:** asegurate de abrir `claude` dentro de la carpeta del repo, o mencioná la skill directamente: `usá la skill apify-jobs-data para...`.

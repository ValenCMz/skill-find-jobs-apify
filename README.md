# skill-find-jobs-apify

Skill para [OpenCode](https://opencode.ai) que busca empleos en LinkedIn, Indeed, Glassdoor, Computrabajo y 20+ portales usando [Apify](https://apify.com). Junta las ofertas, saca duplicados y ofertas fantasma, y las rankea contra tu CV.

La skill es `apify-jobs-data` de [apify/awesome-skills](https://github.com/apify/awesome-skills) y está en [.opencode/skills/apify-jobs-data](.opencode/skills/apify-jobs-data). Como vive dentro del repo, OpenCode la detecta sola cuando lo abrís en esta carpeta.

## Requisitos

- [OpenCode](https://opencode.ai/docs/) instalado y con un modelo configurado
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

El repo trae un [opencode.json](opencode.json) que conecta OpenCode con el servidor MCP de Apify y lee el token de la variable de entorno `APIFY_TOKEN` (`{env:APIFY_TOKEN}`). Solo tenés que definirla.

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

## 4. Verificar la conexión

Desde la carpeta del repo:

```bash
cd skill-find-jobs-apify
opencode mcp list
```

`apify` tiene que aparecer como conectado. Si falla, `opencode mcp debug apify` muestra el detalle.

## 5. Usarlo

Abrí OpenCode en la carpeta:

```bash
opencode
```

Poné tu CV en la carpeta como `cv.md` (o PDF) y pedile algo como:

```
Usá la skill apify-jobs-data: buscame ofertas de full stack developer remoto en Argentina y España
de las últimas 2 semanas y rankealas contra mi cv.md
```

Otros ejemplos:

- `¿Qué skills piden más para backend engineer en Buenos Aires?`
- `Rango salarial de data engineer remoto en España`
- `Exportame a CSV las ofertas de React en LinkedIn de la última semana`

Antes de correr, el agente te muestra los parámetros (rol, ubicación, portales, cantidad) y una estimación de costo. Arrancá con pocos resultados (10–15 por portal) y escalá si hace falta.

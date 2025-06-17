## 🚀 Magento 2.4 - Ambiente Local com Warden

Este guia ajuda a configurar rapidamente um ambiente local Magento 2.4 usando [Warden](https://warden.dev/) e [Mutagen](https://mutagen.io/), ideal para desenvolvimento em sistemas baseados em macOS.

---

### ✅ Pré-requisitos

* macOS com [Homebrew](https://brew.sh/) instalado
* Docker e Docker Compose instalados e funcionando

---

### 🛠️ Instalação de dependências

1. **Instale o Mutagen (sincronização de arquivos eficiente):**

```bash
brew install mutagen-io/mutagen/mutagen
```

2. **Instale o Warden (gerenciador de ambientes Docker para Magento):**

```bash
brew install wardenenv/warden/warden
```

3. **Inicialize o Warden:**

```bash
warden svc up
```

> ⚠️ Rode este comando uma vez após instalar o Warden para ativar os serviços base (DNS, proxy, etc.).

---

### 📦 Subindo o ambiente do projeto

1. **Construa os containers do projeto (sem cache):**

```bash
warden env build --no-cache
```

2. **Suba o ambiente:**

```bash
warden env up
```

3. **Acesse o container PHP:**

```bash
warden shell
```

---

### 📓️ Importando o banco de dados

> Substitua `/path/to/dump.sql.gz` pelo caminho real do seu dump:

```bash
pv /path/to/dump.sql.gz | gunzip -c | warden db import
```

> 💡 Se o dump já estiver descompactado (`.sql`), use:
>
> ```bash
> warden db import < /path/to/dump.sql
> ```

---

### 🌐 Acessando a loja

Depois que o ambiente estiver no ar e o banco importado, acesse sua loja via:

```
https://<domínio-configurado>.test
```

> Exemplo: `https://dentalspeed.test`

Certifique-se de que o domínio esteja no seu `/etc/hosts` com:

```
127.0.0.1 dentalspeed.test
```

---

### 🧹 Comandos úteis no Magento

Dentro do container (`warden shell`):

```bash
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento cache:flush
bin/magento indexer:reindex
```

---

### 🚫 Parar o ambiente

```bash
warden env down
```

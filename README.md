# 📰 Coletor de Notícias - API News e BigQuery

Este projeto realiza **coleta automatizada de notícias** utilizando a **API News** e armazena os resultados no **Google BigQuery**. As buscas são realizadas com base em termos relevantes sobre **proteção de dados**, **cibersegurança** e **LGPD**.

## 📌 Funcionalidades

✅ Consulta de notícias por palavra-chave através da **News API**  
✅ Filtragem por **idioma (Português)** e **período de tempo**  
✅ Paginação diária para coletar até **100 notícias por termo por dia**  
✅ Armazenamento dos resultados no **Google BigQuery**  
✅ Remoção automática de **duplicatas** no banco de dados  

---

## 🛠 Tecnologias Utilizadas

- **Linguagem:** R  
- **Pacotes:** `httr`, `jsonlite`, `tidyverse`, `janitor`, `bigrquery`, `DBI`  
- **Fonte de dados:** [News API](https://newsapi.org/)  
- **Banco de Dados:** **Google BigQuery**  

---

## 📂 Estrutura do Código

```
📁 /  (Diretório Raiz)
├── main.R                 # Script principal para coleta e armazenamento de notícias
└── noticias_news_api.csv  # Arquivo de saída (caso seja salvo localmente)
```

---

## 🚀 Como Executar

### 1️⃣ **Instalar os pacotes necessários**

Se ainda não estiverem instalados, execute no R:

```r
install.packages(c("httr", "jsonlite", "tidyverse", "janitor", "bigrquery", "DBI"))
```

### 2️⃣ **Configurar Credenciais do Google BigQuery**

Antes de rodar o script, **baixe e configure** o arquivo JSON da conta de serviço do BigQuery. No script `main.R`, ajuste o caminho correto:

```r
bigrquery::bq_auth(path = "SEU_ARQUIVO_CREDENCIAIS.json")
```

### 3️⃣ **Definir Termos de Busca**

No script `main.R`, edite a variável `lista_termos` para adicionar novos termos de pesquisa:

```r
lista_termos <- c("LGPD", "ANPD", "Cibersegurança", "Proteção de Dados")
```

### 4️⃣ **Executar o Script**

Para rodar o script e coletar notícias:

```r
source("main.R")
```

Os resultados serão armazenados diretamente no **BigQuery**.

---

## 📊 Estrutura do Banco de Dados (`noticias_news_api`)

A tabela armazenada no **BigQuery** terá a seguinte estrutura:

| Título | Link | Fonte | Data Publicação | Trecho | Termo de Busca |
|--------|------|-------|----------------|--------|---------------|
| Título da Notícia | URL da Notícia | Nome da Fonte | Data `YYYY-MM-DD` | Resumo da Notícia | Palavra-chave usada na busca |

---

## 🛑 Possíveis Problemas e Soluções

### ⚠️ **Erro na API News (Chave de API Inválida)**
Se a **API News** não funcionar, verifique se a chave `api_key` foi corretamente definida no script `main.R`:

```r
api_key <- "SUA_CHAVE_AQUI"
```

### 🔑 **Erro no BigQuery**
Se houver erro ao autenticar no **Google BigQuery**, confirme se o arquivo JSON da credencial foi inserido corretamente:

```r
bigrquery::bq_auth(path = "SEU_ARQUIVO_CREDENCIAIS.json")
```

### ⏳ **A coleta parece lenta?**
Caso queira **diminuir o número de requisições**, reduza o período de coleta:

```r
from_date <- Sys.Date() - days(7)  # Buscar apenas os últimos 7 dias
```

---

## 👨‍💻 Autor

👤 **José Tenório Abs Junior**  
📧 [Seu Email]  
🏛 **IBPAD - Instituto Brasileiro de Pesquisa e Análise de Dados**  

🚀 **Agora você pode coletar notícias automaticamente!** Qualquer dúvida, me avise! 😊
